# How to visit comm100's white label & partner platform by using custom domain?
  Partner is authorized to sell Comm100's Products or Services in their regions. Most of the time, partners would like to sell this product with their own branding and they hope that their customers can use the custom domain to request the product or service. In the case, comm100 provide a solution to satisfy the needs. Comm100 allots a sub-domain for every partner. It's `https://{subdomain}.platform.comm100.com`. We suggest using a reverse proxy server to finish the URL rewrite and application request routing. The reverse proxy server will convert the request from the partner's custom domain into the request of the sub-domain.


1. [What is a Reverse Proxy Server?](#what-is-a-reverse-proxy-server-)
2. [How to configure a Reverse Proxy Server?](#how-to-configure-a-reverse-proxy-server-)

## What is a Reverse Proxy Server?
  A proxy server is a go‑between or intermediary server that forwards requests for content from multiple clients to different servers across the Internet. A reverse proxy server is a type of proxy server that typically sits behind the firewall in a private network and directs client requests to the appropriate backend server. A reverse proxy provides an additional level of abstraction and control to ensure the smooth flow of network traffic between clients and servers.  

  Common uses for a reverse proxy server include:  

  - Load balancing – A reverse proxy server can act as a “traffic cop,” sitting in front of your backend servers and distributing client requests across a group of servers in a manner that maximizes speed and capacity utilization while ensuring no one server is overloaded, which can degrade performance. If a server goes down, the load balancer redirects traffic to the remaining online servers.
  - Web acceleration – Reverse proxies can compress inbound and outbound data, as well as cache commonly requested content, both of which speed up the flow of traffic between clients and servers. They can also perform additional tasks such as SSL encryption to take load off of your web servers, thereby boosting their performance.
  - Security and anonymity – By intercepting requests headed for your backend servers, a reverse proxy server protects their identities and acts as an additional defense against security attacks. It also ensures that multiple servers can be accessed from a single record locator or URL regardless of the structure of your local area network.

## How to configure a Reverse Proxy Server?
  We will guide you through how to configure the reverse proxy server in different web server in the windows environment.
- [Nginx](#nginx-as-a-reverse-proxy-server) 
- [Apache](#apache-as-a-web-server)
- [IIS](https://github.com/hypnus1983/LivechatAPI/blob/master/arr.md)

### Nginx as a reverse proxy server
  Nginx is one of the most popular open source web server. If you use the Nginx as your web server or you want to use it, you can do as follows to set the Nginx as your reverse proxy server.
  - apply a custom domain
  - install nginx
  - configure nginx
  - start nginx and test

#### Step 1 - Apply a custom domain
  Firstly, you must apply a custom domain which points to the IP address of the reverse proxy and support SSL cert. Comm100 only allow request with `https`. Such as `https://loveapp.agx.com`.After that, you need download the SSL cert on the reverse proxy server for configuration.

#### Step 2 - Install Nginx
  If you have used the Nginx, please skip this step. 
  You can download the Nginx from **[NGINX](http://nginx.org/en/download.html)** according to the IT environment.
  Then install the Nginx.

#### Step 3 - Configure Nginx
  Get the sub-domain(which is assigned for you as a partner of Comm100, e.g. `loveapp.platform.comm100.com`) of product from Comm100.  
  
  Configuration Params:
  - **independent_domain** - Partner own custom domain, e.g. `loveapp.agx.com`.
  - **ssl_crt** -relative path of the SSL certificate of the custom domain ,e.g. `cert/loveapp.crt` means that the cert named `loveapp.crt` stores in the folder `conf\cert`.
  - **ssl_crt_key** - relative path of the SSL certificate key of the custom domain ,e.g. `cert/loveapp.key` means that the cert key named `loveapp.key` stores in the folder `conf\cert`.
  - **sub_domain** - which is assigned for you as a partner of Comm100, e.g. `loveapp.platform.comm100.com`.
  - **sub_domain_full_name** -which is assigned for you as a partner of Comm100 e.g. `https://loveapp.platform.comm100.com`.
       
       
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

### Step 4 - Start Nginx and test
Load the cmd to the Nginx root path, e.g. `F:\nginx-1.15`. Type the command as the follows:
1. Start Nginx   
   `F:\nginx-1.15.2>start nginx`
2. Reload Nginx after updating the configuration.    
   `F:\nginx-1.15.2>nginx -s reload`
3. Quit Nginx    
   `F:\nginx-1.15.2>nginx -s quit`

After starting Nginx successfully, Type the custom domain in the browser, e.g. `https://loveapp.agx.com`. If everything is ok, the browser will lead you to the login page as follows:
`https://loveapp.agx.com/adminManage/login.aspx`.Then the custom of the partner can use the product and the service.

### Apache as a reverse proxy server
  Apache is one of the most popular open source web server. If you use the Apache as your web server or you want to use it, you can do as follows to set the Apache as your reverse proxy server.
  - apply an custom domain
  - install apache
  - configure apache
  - start apache and test

#### Step 1 - Apply a custom domain
  Firstly, you must apply a custom domain which points to the IP address of the reverse proxy and support SSL cert. Comm100 only allow request with `https`. Such as `https://loveapp.apache.com`. After that, you need download the SSL cert on the reverse proxy server for configuration.

#### Step 2 - Install Apache
  If you have used the Apache, please skip this step. 
  You can download the Apache from **[APACHE](http://httpd.apache.org/download.cgi)** according to the IT environment.
  Then install the Apache.

#### Step 3 - Configure Apache
  Get the sub-domain(which is assigned for you as a partner of Comm100, e.g. `loveapp.platform.comm100.com`) of product from Comm100.  
  
  Configuration Params:
  - **independent_domain** - Partner own custom domain, e.g. `loveapp.apache.com`.
  - **ssl_crt** -relative path of the SSL certificate of the custom domain ,e.g. `cert/loveapp.crt` means that the cert named `loveapp.crt` stores in the folder `conf\cert`.
  - **ssl_crt_key** - relative path of the SSL certificate key of the custom domain ,e.g. `cert/loveapp.key` means that the cert key named `loveapp.key` stores in the folder `conf\cert`.
  - **sub_domain** - which is assigned for you as a partner of Comm100, e.g. `loveapp.platform.comm100.com`.
  - **sub_domain_full_name** -which is assigned for you as a partner of Comm100 e.g. `https://loveapp.platform.comm100.com`.
   
       
##### update httpd.conf configuration file
Edit `/conf/httpd.conf` as follows(Use a real value to replace the {parm_name}):  
To comment out a line in httpd.conf place a # symbol at the beginning of the line.  
To uncomment a line in httpd.conf remove the # symbol at the beginning of the line.  

Comment out:  
`Listen 80`

Find the following lines and uncomment them. These lines are not contigious so will need to be found and uncommented one by one:  
\#LoadModule headers_module modules/mod_headers.so  
\#LoadModule lbmethod_byrequests_module modules/mod_lbmethod_byrequests.so  
\#LoadModule proxy_module modules/mod_proxy.so  
\#LoadModule proxy_http_module modules/mod_proxy_http.so  
\#LoadModule rewrite_module modules/mod_rewrite.so  
\#LoadModule slotmem_shm_module modules/mod_slotmem_shm.so  

Find:  
`ServerName localhost:80 `  
And change it to something appropriate e.g. replacing `{independent_domain}` with the real value of the custom domain:  
`ServerName {independent_domain}:443`

Find section `IfModule ssl_module` and update, make sure that the configuration file named `httpd-ssl.conf` exists in the folder `conf/extra/`:  
```javascript
<IfModule ssl_module>
   Include conf/extra/httpd-ssl.conf
   SSLRandomSeed startup builtin
   SSLRandomSeed connect builtin
</IfModule>
```


##### update httpd-ssl.conf configuration file
Edit `/conf/extra/httpd-ssl.conf` as follows(Use a real value to replace the {parm_name}): 

Find section `VirtualHost` and update, insert into the file if the section is not exist:  
```javascript
NameVirtualHost *:443
<VirtualHost *:443>

DocumentRoot "${SRVROOT}/htdocs"
ServerName {sub_domain}
ServerAlias {sub_domain}

SSLEngine on
SSLProxyEngine on
ProxyRequests off
<Proxy *>
  Order deny,allow
  Allow from {sub_domain}
</Proxy>

RewriteEngine on
ProxyPass / {sub_domain_full_name}/
 ProxyPassReverse / {sub_domain_full_name}/
 AddOutputFilterByType SUBSTITUTE text/html
 Substitute  "s|https://{independent_domain}/|{sub_domain_full_name}/|i"

SSLCipherSuite ALL:!ADH:!EXPORT56:RC4+RSA:+HIGH:+MEDIUM:+LOW:+SSLv2:+EXP:+eNULL


SSLCertificateFile "${SRVROOT}/{ssl_crt}"
SSLCertificateKeyFile "${SRVROOT}/{ssl_crt_key}"


<FilesMatch "\.(cgi|shtml|phtml|php|aspx)$">
    SSLOptions +StdEnvVars
</FilesMatch>

<Directory />
    Options FollowSymLinks
    AllowOverride none
    Require all granted
    Allow from all
</Directory>

<Directory "${SRVROOT}/cgi-bin">
    SSLOptions +StdEnvVars
</Directory>
BrowserMatch ".*MSIE.*" \
         nokeepalive ssl-unclean-shutdown \
         downgrade-1.0 force-response-1.0

CustomLog "${SRVROOT}/logs/ssl_request.log" \
          "%t %h %{SSL_PROTOCOL}x %{SSL_CIPHER}x \"%r\" %b"

</VirtualHost>     
```

### Step 4 - Start Apache and test
Enter the `bin` folder in Apache root path, e.g. `G:\Apache24\bin`. :
1. Start ApacheMonitor   
   `G:\Apache24\bin>apachemonitor`
2. Open the Apache monitor window, you'll find some menu to operate the Apache. These buttons correspond to the operation of the Apache server. 

After starting Apache successfully, Type the custom domain in the browser, e.g. `https://loveapp.apache.com`. If everything is ok, the browser will lead you to the login page as follows:
`https://loveapp.apache.com/adminManage/login.aspx`.Then the custom of the partner can use the product and the service.  

### IIS as a web server
The next part will show you how to use the Application Request Routing (ARR) and URL Rewrite features of Internet Information Services (IIS) to implement a forward proxy server.

To set up a forward proxy server using ARR, you must have the following:
- IIS 7.0 or above on Windows 2008 (any SKU) or newer with Tracing role service installed for IIS.
- Microsoft Application Request Routing Version 3 and dependent modules
- Minimum of one worker server with working sites and applications.

#### Step 1 - Install ARR
If Application Request Routing Version 3 has not been installed, it is available for download [here](https://www.microsoft.com/en-us/download/details.aspx?id=39715). The download site displayed by this link includes installation instructions.

#### Step 2 - Install URL Rewrite
Install the URL Rewrite module for IIS through the Server Manager. For more information, see [Installing IIS 8.5 on Windows Server 2012 R2](https://docs.microsoft.com/en-us/iis/install/installing-iis-85/installing-iis-85-on-windows-server-2012-r2).

#### Step 3 - Configure ARR as a Forward Proxy
To enable ARR as a proxy, and to create a URL Rewrite rule to enable ARR as a forward proxy, proceed as follows:
1. Open Internet Information Services (IIS) Manager.
2. In the Connections pane, select the **server**.
3. In the server pane, double-click **Application Request Routing Cache**.
![IIS](https://docs.microsoft.com/en-us/iis/extensions/configuring-application-request-routing-arr/creating-a-forward-proxy-using-application-request-routing/_static/image3.jpg)

4. In the **Actions** pane, click **Server Proxy Settings**.
![iis](https://docs.microsoft.com/en-us/iis/extensions/configuring-application-request-routing-arr/creating-a-forward-proxy-using-application-request-routing/_static/image4.jpg)

5. On the **Application Request Routing** page, select **Enable proxy**.
![iis](https://docs.microsoft.com/en-us/iis/extensions/configuring-application-request-routing-arr/creating-a-forward-proxy-using-application-request-routing/_static/image5.jpg)

6. In the **Actions** pane, click **Apply**. This enables ARR as a proxy at the server level.
![iis](https://docs.microsoft.com/en-us/iis/extensions/configuring-application-request-routing-arr/creating-a-forward-proxy-using-application-request-routing/_static/image6.jpg)

#### Step 4 - Add a Proxy Site  
1. Right-click on the **Sites** node in the **Connections** pane and select **Add Website**.
2. Config the website and click **OK** to save settings.
   - Physical path - Could be an empty directory.
   - Host name - Partner own custom domain, e.g. www.proxyserver.com.
   - Binding type - https   
   ![](https://raw.githubusercontent.com/hypnus1983/LivechatAPI/master/add%20website.png)
3. Explodes the **Sites** node in the **Connections** pane, and click the proxy site.
4. In the server pane, double-click **Compression**.
5. In the **Compression page**, unselect **Enable dynamic content compression**.In the Actions pane, click Apply. This disenables dynamic content compression at the site level.


#### Step 5 - Config URL Rewrite Rules
1. Click the proxy site in **Sites** node in the **Connections** pane. In the **Actions** pane, click **Explore** to open the website's directory.
2. Open the **web.config** by notepad.
3. Edit the file as follows the example. Make sure to replace ***www.proxyserver.com*** to the partner own custom domain, and replace **app.platform.comm100.com** to the Comm100's partner sub-domain. Save the web.config file at last.

``` xml
<?xml version="1.0" encoding="UTF-8"?>
<configuration>
    <system.webServer>
        <rewrite>
            <rules>
                <rule name="test">
                    <match url="^(.*)" />
                    <conditions>
                        <add input="{HTTP_HOST}" pattern="^www.proxyserver.com$" />
                    </conditions>
                    <action type="Rewrite" url="https://app.platform.comm100.com/{R:1}" />

                </rule>
            </rules>
            <outboundRules>
                <rule name="rewrite tags" preCondition="IsHTML">
                    <match filterByTags="A, Form, Img, Link" pattern="(http|https)://app.platform.comm100.com/(.+)" />
                    <conditions>
                    </conditions>
                    <action type="Rewrite" value="{R:1}://www.proxyserver.com/{R:2}" />
                </rule>
                <rule name="rewrite window.location" preCondition="IsHTML">
                    <match filterByTags="None" pattern="window[.]location([.]href){0,1}[ ]*=[ ]*(&amp;#39;|')(http|https)://app.platform.comm100.com/(.+?)(&amp;#39;|')" />
                    <action type="Rewrite" value="window.location{R:1}={R:2}{R:3}://www.proxyserver.com/{R:4}{R:5}" />
                </rule>
                <rule name="rewrite window.open" preCondition="IsHTML">
                    <match filterByTags="None" pattern="window.open[(]&quot;(https|http)://app.platform.comm100.com/(.+?)&quot;" />
                    <action type="Rewrite" value="window.open(&quot;{R:1}://www.proxyserver.com/{R:2}&quot;" />
                </rule>
                <preConditions>
                    <preCondition name="IsHTML">
                        <add input="{RESPONSE_CONTENT_TYPE}" pattern="^text/html" />
                    </preCondition>
                </preConditions>
            </outboundRules>
        </rewrite>
        <urlCompression doDynamicCompression="false" />
    </system.webServer>
</configuration>
```


#### Step 6 - Test
1. Click the proxy site in **Sites** node in the **Connections** pane. In the **Actions** pane, click **Restart** to restart the website.
2. Type the partner own custom domain in the browser, e.g. https://www.proxyserver.com. If everything is ok, the browser will lead you to the login page as follows: https://www.proxyserver.com/adminManage/login.aspx. Then the custom of the partner can use the product and the service.