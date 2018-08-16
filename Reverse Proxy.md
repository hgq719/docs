# General
1. [What is a Reverse Proxy Server?](#what-is-a-reverse-proxy-server-)
2. [How to configure a Reverse Proxy Server?](#how-to-configure-a-reverse-proxy-server-)

## What is a Reverse Proxy Server?
  A proxy server is a go‑between or intermediary server that forwards requests for content from multiple clients to different servers across the Internet. A reverse proxy server is a type of proxy server that typically sits behind the firewall in a private network and directs client requests to the appropriate backend server. A reverse proxy provides an additional level of abstraction and control to ensure the smooth flow of network traffic between clients and servers.  

  Common uses for a reverse proxy server include:  

  - Load balancing – A reverse proxy server can act as a “traffic cop,” sitting in front of your backend servers and distributing client requests across a group of servers in a manner that maximizes speed and capacity utilization while ensuring no one server is overloaded, which can degrade performance. If a server goes down, the load balancer redirects traffic to the remaining online servers.
  - Web acceleration – Reverse proxies can compress inbound and outbound data, as well as cache commonly requested content, both of which speed up the flow of traffic between clients and servers. They can also perform additional tasks such as SSL encryption to take load off of your web servers, thereby boosting their performance.
  - Security and anonymity – By intercepting requests headed for your backend servers, a reverse proxy server protects their identities and acts as an additional defense against security attacks. It also ensures that multiple servers can be accessed from a single record locator or URL regardless of the structure of your local area network.

## How to configure a Reverse Proxy Server?
  Partners are authorized to sell Comm100's Products or Services in their regions.In most cases, partners would like to sell these product with their own branding and they hope that their custom can use the independent-domain to request the product or service.In the case, we need configure a reverse proxy server to finish the URL rewrite and application request routing.

  Next, we will guide you through how to configure the reverse proxy server in different web server in the windows environment.
- [Nginx](#nginx-as-a-web-server) 
- [IIS](#iis-as-a-web-server)
- [Tomcat](#tomcat-as-a-web-server)

### Nginx as a web server
  Nginx is one of the most popular open source web server.If you use the nginx as your web server or you want to use it,you can do as follows.
  - apply a independent-domain
  - install nginx
  - configure nginx
  - start nginx and test

#### Step 1 - Apply a independent-domain
  Firstly, you must apply a independent-domain which point to ip address of the reverse proxy and support ssl cert.Comm100 only allow request with `https`. Such as `https://loveapp.agx.com`.After that,you need download the SSL cert on the reverse proxy server for configuration.

#### Step 2 - Install Nginx
  If you have used the nginx, please skip this step. 
  You can download the nginx from [NGINX](http://nginx.org/en/download.html) according to the IT environment.
  Then install the nginx.

#### Step 3 - Configure Nginx
  Get the sub-domain(which is assigned for you as a partner of Comm100, e.g. `loveapp.platform.comm100.com`) of product from Comm100.
  Configuration Params:
  - independent_domain - Partner own independent-domain, e.g. `loveapp.agx.com`.
  - ssl_crt -relative path of the SSL certificate of the independent-domain ,e.g. `cert/loveapp.crt` means that the cert named `loveapp.crt` stores in the folder `conf\cert`.
  - ssl_crt_key - relative path of the SSL certificate key of the independent-domain ,e.g. `cert/loveapp.key` means that the cert key named `loveapp.key` stores in the folder `conf\cert`.
  - sub_domain - which is assigned for you as a partner of Comm100, e.g. `loveapp.platform.comm100.com`.
  - sub_domain_full_name -which is assigned for you as a partner of Comm100 e.g. `https://loveapp.platform.comm100.com`.
       
       
   Edit `/conf/nginx.conf` as follows(Use a real value to replace the {parm_name}):   

  ```javascript
  http {
    include       mime.types;
    default_type  application/octet-stream;

    sendfile        on;
    ssl_certificate      {ssl_crt}
    ssl_certificate_key  {ssl_crt_key}
    
    ssl_session_cache    shared:SSL:1m;
    ssl_session_timeout  5m;
    
    ssl_ciphers  HIGH:!aNULL:!MD5;
ssl_prefer_server_ciphers  on;

    keepalive_timeout  65;

    server {
        listen       443 ssl;
        server_name  {independent_domain};

        error_page   500 502 503 504  /50x.html;
        location = /50x.html {
            root   html;
        }
        location / {
            proxy_cookie_domain {sub_domain} {independent_domain}; 
            add_header 'Access-Control-Allow-Origin' '*';
            proxy_redirect off;
            proxy_set_header Host $host;
            proxy_set_header X-Real-IP $remote_addr;
            proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
            proxy_pass {sub_domain_full_name};
        }
    }
    }
}
  ```

#### Example

```javascript
http {
    include       mime.types;
    default_type  application/octet-stream;

    sendfile        on;
    ssl_certificate      cert/loveapp.crt; 
    ssl_certificate_key  cert/loveapp.key; 
    
    ssl_session_cache    shared:SSL:1m;
    ssl_session_timeout  5m;
    
    ssl_ciphers  HIGH:!aNULL:!MD5;
ssl_prefer_server_ciphers  on;

    keepalive_timeout  65;

    server {
        listen       443 ssl;
        server_name  loveapp.agx.com; 

        error_page   500 502 503 504  /50x.html;
        location = /50x.html {
            root   html;
        }
        location / {
            proxy_cookie_domain loveapp.platform.comm100.com loveapp.agx.com; 
            add_header 'Access-Control-Allow-Origin' '*';
            proxy_redirect off;
            proxy_set_header Host $host;
            proxy_set_header X-Real-IP $remote_addr;
            proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
            proxy_pass https://loveapp.platform.comm100.com;
        }
    }
    }
}
```

### Step 4 - Start nginx and test
Load the cmd to the nginx root path, e.g. `F:\nginx-1.15`. Type the command as the follows:
1. Start Nginx   
   `F:\nginx-1.15.2>start nginx`
2. Reload Nginx after updating the configuration.    
   `F:\nginx-1.15.2>nginx -s reload`
3. Quit Nginx    
   `F:\nginx-1.15.2>nginx -s quit`

After starting nginx successfully, Type the independent-domian in the brower, e.g. `https://loveapp.agx.com`. If everything is ok, the brower will lead you to the login page as follows:
`https://loveapp.agx.com/adminManage/login.aspx`.Then the custom of the partner can use the product and the service.