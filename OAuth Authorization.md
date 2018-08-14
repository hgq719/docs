# OAuth Authentication
  You can use OAuth2 to authenticate all your API requests to Comm100. OAuth provides a secure way for your application to access your account data without requiring that sensitive information like email and password be sent with the requests. There are different OAuth flows according to different type of API.

1. [Partner API OAuth Authentication](#partner-api-oauth-authentication)
2. [Account & Livechat API OAuth Authentication](#account-and-livechat-api-oauth-authentication)

## Partner API OAuth Authentication
  You can only use password grant type to exchange a partner's email and password for an access token directly while calling the Partner API.This grant type is supported for the partner which is highly secured by Comm100,  and it can operate the data which belongs to the partner. 

### Using cURL
  Params:
  - email - the email of the partner account.
  - password - the password of the partner account.
  - grant_type - specify `password` as the value.

  ```javascript
    curl https://app.platform.comm100.com/oauthServerForPartner/oauth/token \
      -H "Content-Type:application/x-www0form-urlencoded" \
      -d 'grant_type=password&email={comm100_parnter_email}&password={comm100_partner_password}'
      -X POST
  ```

### Example Response
  ```javascript    
  HTTP/1.1 200 OK
  Content-Type: application/json
  {
    "access_token":"vQAQmLX8jvtsG71ItN2QAisqI_F7cDIE0yaX0FfS3RX6g-HR4gfHSVMaOukomYJiJX0Q"
    ,"token_type":"bearer"
    ,"expires_in":43199
    ,"refresh_token":"91a728cdd4c64fb7b128f74f4855c3daee44167ef60542a2b45c21e16373ed02"
  }
  ```

## Account And Livechat API OAuth Authentication
  Comm100 supports several OAuth flows.The first flow, the authorization code grant flow, uses an authorization code after getting user confirmation to exchange for an access token that acts on behalf of that user. The other two options are server-side grant types that don't require interacting with end users.
  - [Authorization code grant flow](#authorization-code-grant-flow)
  - [Implicit grant flow](#implicit-grant-flow)
  - [Password grant type](#password-grant-type)
  - [Client credentials type](#client-credentials-type)

### Authorization Code Grant Flow
  To implement the authorization code grant flow, you should get an authorization code firstly. Then you can use it to exchange an access token and use the access token to call api.   

#### Get an authorization code
  Params:
  - client_id - the id of oauth client.
  - siteId - the id of rueqest site.
  - redirect_uri - the redirect uri of oauth client.
  - response_type - specify `code` as the value.

  ```javascript
    curl "https://app.platform.comm100.com/oauthServer/oauth/authorize?client_id={oauth_client_id}&siteId={request_siteId}&redirect_uri={oauth_client_redirectUri}&response_type=code"
  ```

#### Example Response
  ```javascript    
  {oauth_client_redirectUri}?code=591c35a40c8145e0b08dfa2b6e3294f17afc56729eb943eeac290c70+ef49b6e
  ```

#### Exchange an access token
  Params:
  - grant_type - specify `authorization_code` as the value.
  - code - the authorization code.
  - redirect_uri - the redirect uri of oauth client.
  - client_id - the id of oauth client.
  - client_secret - the secret of oauth client.

  ```javascript
    curl https://app.platform.comm100.com/oauthServerForPartner/oauth/token \
      -H "Content-Type:application/x-www0form-urlencoded" \
      -d 'grant_type=authorization_code&code={authorization_code}&redirect_uri={oauth_client_redirectUri}&client_id={oauth_client_id}&client_secret={oauth_client_secret}'
      -X POST
  ```

#### Example Response
  ```javascript    
  HTTP/1.1 200 OK
  Content-Type: application/json
  {
    "access_token":"vQAQmLX8jvtsG71ItN2QAisqI_F7cDIE0yaX0FfS3RX6g-HR4gfHSVMaOukomYJiJX0Q"
    ,"token_type":"bearer"
    ,"expires_in":43199
    ,"refresh_token":"91a728cdd4c64fb7b128f74f4855c3daee44167ef60542a2b45c21e16373ed02"
  }
  ```

### Implicit Grant Flow
  The implicit grant flow is similar to the authorization code grant flow except there's no need to apply the authorization code. You can request an access token directly while you set the value of the `response_type` parameter to `token` instead of `code`.

#### Get an access token
  Params:
  - client_id - the id of oauth client.
  - siteId - the id of rueqest site.
  - redirect_uri - the redirect uri of oauth client.
  - response_type - specify `token` as the value.

  ```javascript
    curl "https://app.platform.comm100.com/oauthServer/oauth/authorize?client_id={oauth_client_id}&siteId={request_siteId}&redirect_uri={oauth_client_redirectUri}&response_type=token"
  ```

#### Example Response
  ```javascript    
  HTTP/1.1 200 OK
  Content-Type: application/json
  {
    "access_token":"vQAQmLX8jvtsG71ItN2QAisqI_F7cDIE0yaX0FfS3RX6g-HR4gfHSVMaOukomYJiJX0Q"
    ,"token_type":"bearer"
    ,"expires_in":43199
    ,"refresh_token":"91a728cdd4c64fb7b128f74f4855c3daee44167ef60542a2b45c21e16373ed02"
  }
  ```

### Password Grant Type
  You can only use password grant type to exchange a agent's email and password for an access token directly while calling the account or livechat API.This grant type is supported for the partner which is highly secured by Comm100. 

#### Using cURL
  Params:
  - email - the email of the agent account.
  - password - the password of the agent account.
  - grant_type - specify `password` as the value.

  ```javascript
    curl https://app.platform.comm100.com/oauthServerForPartner/oauth/token \
      -H "Content-Type:application/x-www0form-urlencoded" \
      -d 'grant_type=password&email={comm100_agent_email}&password={comm100_agent_password}'
      -X POST
  ```

#### Example Response
  ```javascript    
  HTTP/1.1 200 OK
  Content-Type: application/json
  {
    "access_token":"vQAQmLX8jvtsG71ItN2QAisqI_F7cDIE0yaX0FfS3RX6g-HR4gfHSVMaOukomYJiJX0Q"
    ,"token_type":"bearer"
    ,"expires_in":43199
    ,"refresh_token":"91a728cdd4c64fb7b128f74f4855c3daee44167ef60542a2b45c21e16373ed02"
  }
  ```

### Client Credentials Type
  The client credentials grant flow is used to access API endpoints designed specifically for the third applications rather than for users. 

#### Using cURL
  Params:
  - grant_type - specify `client_credentials` as the value.
  - redirect_uri - the redirect uri of oauth client.
  - client_id - the id of oauth client.
  - client_secret - the secret of oauth client.
  - siteId - the id of request site.

  ```javascript
    curl https://app.platform.comm100.com/oauthServerForPartner/oauth/token \
      -H "Content-Type:application/x-www0form-urlencoded" \
      -d 'grant_type=client_credentials&code={authorization_code}&redirect_uri={oauth_client_redirectUri}&client_id={oauth_client_id}&client_secret={oauth_client_secret}&siteId={request_siteId}'
      -X POST
  ```

#### Example Response
  ```javascript    
  HTTP/1.1 200 OK
  Content-Type: application/json
  {
    "access_token":"vQAQmLX8jvtsG71ItN2QAisqI_F7cDIE0yaX0FfS3RX6g-HR4gfHSVMaOukomYJiJX0Q"
    ,"token_type":"bearer"
    ,"expires_in":43199
    ,"refresh_token":"91a728cdd4c64fb7b128f74f4855c3daee44167ef60542a2b45c21e16373ed02"
  }
  ```