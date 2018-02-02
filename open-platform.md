# General

1. [App Developer Account](#app-developer-account)
2. [App Apply](#app-apply)
3. [App File Requirements](#app-file-requirements)
4. [Setting The Location](#app-the-location)
5. [API](#api)
6. [Security and Authentication](#security-and-authentication)
7. [Rate Limits](#rate-limits)
8. [Error Manage](#error-manage)
9. [Response Format](#response-format)

## App Developer Account
  Comm100专门为App开发者新增一套Developer账号系统，该系统基于现有系统进行身份验证，可以直接将Comm100的现有账号升级为Developer账号。通过Developer可以：
  - 开发私有App来丰富自己的Comm100产品功能
  - 开发共有App并注册到Comm100的Marketplace供其他的客户安装及使用
  - 在Marketplace中维护自己开发的App的基本信息
  - 查看App的安装、使用报表

## App Apply
  Developer在开发App之前必须先通过Comm100提供的页面申请App的访问权限，才能进行Api调用。通过提供`AppName`、`CompanyName`、`AppIdentity`等信息获取到下面的信息
  - `client_id` - App唯一标识，用于Developer、使用App的SiteManager、Agent获取App元数据
  - `client_secret` - App身份密钥，用于换取`Access_token`来访问Comm100的Api

## App File Requirements
  App需要在Comm100的产品中安装和使用必须包含下面的文件及结构，可根据需求添加其他文件。

  ```javascript
  assets/
    logo.png
    logo-small.png
  manifest.json
  ```

  - manifest.json - App的描述和配置文件，具体属性配置可查看[Manifest Reference](https://github.com/hgq719/docs/blob/master/ManifestReference.md)。
  - assets - 用来存放当前App需要使用的其他相关文件的文件夹
  - assets/logo.png - Comm100应用管理中的App图标
  - assets/logo-small.png - Comm100产品安装App的位置的icon图标,包括Agent Console的topBar、navigationBar、sideBar中的图标

## Setting The Location
  开发者可以通过`manifest.json`文件中的`location`属性来配置App安装后出现在Comm100产品界面的位置。这个配置的路径地址可以是相对路径(指向`assets`文件夹下的一个html文件)，也可以是绝对路径(指向一个外部页面)。  
  例如，开发者可以在Control Panel的头部添加一个产品级菜单。

  ```json
  "location": {
    "agentConsole_topBar": "/assets/index.html"
  }
  ```
  所有可用位置可以查看[location](https://github.com/hgq719/docs/blob/master/ManifestReference.md#location)。  
  注：如果使用绝对路径，建议使用`https`页面。

## Instance
  标识App的运行实例，每一个iframe都是一个实例。同一个App在Manifest中定义了多个位置，则这个App就存在多个App Instance。可以通过API来获取当前App的实例信息。

  - Control Panel API
  ```javascript
    Comm100API.get('app.instance')
  ```

  - Agent Console API
  ```javascript
    Comm100AgentConsoleAPI.get('app.instance')
  ```

## API
  Developer可以在不同的场景通过调用不同类型的API来开发第三方应用集成。
  - [Restful API](https://www.comm100.com/doc/api/introduction.htm)
  - Javascript API
    + [Agent Console API](https://github.com/Comm100/agent-console-extension-sample/blob/master/doc/agent-console-api.md)
    + [Control Panel API](#control-panel-api)
    + [Visitor Side API](https://ent.comm100.com/LiveChatFunc/doc/CustomJS/index.html#/)
  - [Webhook](https://www.comm100.com/livechat/knowledgebase/category/live-chat-api-good-practices/)

## Security and Authentication
  1.Comm100的身份认证  
  - Restful API 

    Comm100对于Restful的Api采取标准的[OAuth2.0](#oauth2.0)的方式对调用者进行身份验证。Developer可以通过[App Apply](#app-apply)中获取的`client_secret`来换取`Access_token`进行Api的调用。  

  - Agent Console和Control Panel API  

    这两端的JS开放的Api只能在Agent登录的情况下才能进行调用，而Developer开发的嵌入在Comm100的iframe中的页面就只能让用户在当前用户和当前App的身份下进行Api的调用，不做额外的身份验证。  
  - Visitor Side Javascript  

    该端开放的Api只能让用户操作访客端前端的一些UI或者event交互，涉及的数据都是当前访客的数据，不涉及到受限的资源，不做身份验证。  
    
  - 后台权限配置   
  
    通过该配置，Site Manager能对一些特定的功能进行相应的权限配置，如配置App的配置界面只有Site Manager才有权限访问。


  2.Developer对Comm100的身份认证  
  - User Meta  
    Agent Console和Control Panel只有在用户登录的情况下才能进行操作，Developer可通过Comm100提供的Api来获取User Meta(当前登录用户的元数据信息)，从元数据中获取当前用户的身份信息来进行身份验证。
  - [JSON Web Token](#json-web-token)  
    安装在Comm100产品中的App能包含一个由开发者远程托管的的页面，该页面会加载在Comm100的某一个特定的iframe中。当打开Comm100产品中的app的时候，Comm100必须去请求这个远程托管的原始页面，为了帮助开发者对这个请求进行验证，Comm100可以在这个请求中加入JSON Web Token，开发者的远程托管页面可以通过这个JWT来验证当前请求是否是来自于一个Comm100的合法请求。


  3.用户系统对访客的身份认证  
  - Visitor Property  
    Comm100的访客对象中包含SSO标志和Custom Variable，可以通过这些属性来判断当前访客的登录状态或信息。

### JSON Web Token
  JSON Web Token简称[JWT](http://self-issued.info/docs/draft-ietf-oauth-json-web-token.html)，是一种紧凑的URL安全方法，用于在网络通讯的双方之间传递。Comm100的JWT Token包含下面主要属性，用户可以通过这些属性来对这个请求进行验证。
  - `iss` -JWT的签发者
  - `sub` -JWT所面向的用户
  - `aud` -JWT的接收方
  - `exp` -时间戳，JWT的过期时间
  - `iat` -时间戳，JWT的签发时间
  - `nbf` -时间戳，JWT的生效开始时间，在此之前JWT无效

### 处理JWT Token
  - 一旦[启用JWT Token]()，Comm100会做如下的事情：
      + 将请求类型由GET变为POST
      + 在POST请求中包含一个`token`字段，这个`token`包含JWT Token的信息  

  - 为了完成验证，开发者需要完成以下的事情：
      + 处理当前的POST请求
      + 从请求的数据中获取Token信息
      + 校验JWT Token  


  Comm100使用RSA来签名这个JWT token，需要校验它，则需要[获取app的公钥](#get-app-public-key)来解密这个token。如

  ```javascript
    public_key = getPublicKey();
    decoded_token = JWT.decode(data["token"],public_key,"RS256");
    jwt_claims = decoded_token.claims;
    user_info = jwt_claims.userInfo
    user_name = user_info["user"]["name"];
    iss = jwt_claims.iss;    //如：comm100.com
    aud = jwt_claims.aud;    //如：myApp.com
  ```  


### Get app public key
  可以通过`client_secret`，访问下面的API来获取App的公钥。开发者可以使用这个公钥来识别某个特定的请求是否是来自Comm100的合法请求。

  ```javascript
    Get /api/v1/apps/public_key
  ```

### OAuth2.0
  OAuth2.0采用了OAuth2.0标准协议来进行用户身份验证和获取用户授权，其认证流程简单、安全。开发者需要在自己的请求头中指定`access_token`，格式如下：
  ```json
    "Authorization": "bearer {access_token}"
  ```

## Rate Limits
  - API允许同一时刻的并发数量限制。
  - Api限制同一用户或ip在每段时间只能请求一定的次数。限制的单位时间为每天（每小时）；限制的维度为授权用户或ip。
  - 部分特殊接口有单独的api请求次数限制
  - 不同级别的账号对api访问次数的限制也有不同的设置。

## Error Manage
  - [Restful API Error](#restful-api-error)
  - [Javascript API Error](#javascript-api-error)
  - [Webhook API Error](#webhook-api-error)

### Restful API Error
  1.在请求未正常执行时，Server会根据真实情况返回对应的http status code，在此基础上会从http response中返回Comm100定义的的`error code`和`error message`  

  2.错误规范  


| Http Status Code               | 返回结果                                                                                                                    |
| ------------------------------ |--------------------------------------------------------------------------------------------------------------------------- |
| 200 - OK                       | 一切正常，且Response里面返回正确的结果                                                                                        |
| 400 - Bad Request              | 参数传入不正确或者不合法。Response里面包含Comm100的`error code`和`error string`                                                |
| 401 - Unauthorized             | 无授权，用户验证不通过                                                                                                        |
| 403 - Forbidden                | 调用超出限制, Agent本身没有权限。Response里面包含Comm100的`error code`和`error string`                                         |
| 404 - Not Found                | 请求资源不存在。Response里面包含Comm100的`error code`和`error string`                                                         |
| 500 - Internal Error           | 服务器内部错误。Response里面包含Comm100的`error code`和`error string`。这个错误包含比较广泛，上述错误外，其他的错误都会在500中返回 |  


  3.Error Response，以json格式返回具体的错误信息
  ```json
  {
    "code": 403003,
    "message": "You have no permission to perform this operation."
  }
  ```  

  4.错误编码规范  
  - 错误编码采用Comm100 Framework中对各个产品能够使用的错误码范围中使用，保留400000 – 600000为api中特定使用的错误编码

|Error Code     | Http Status Code               | Message                                                                                                   
| ------------- |------------------------------- | -------------------------------------- 
| 400000        |400                    | Parameter '{param}' is required.       
| 400001        |400                    | Parameter '{param}' should be in time format of 'YYYY-MM-DDThh:mm:ssZ'.       
| 400002        |400                    | Parameter '{param}' should be in timezone format of '+-hh:mm'.       
| 400003        |400                    | Parameter '{param}' should be a number.
| 400004        |400                    | Parameter '{param}' should be 'true' or 'false'.
| 400005        |400                    | Parameter '{param}' should be an email.
| 400006        |400                    | Unsupported '{param}' type.
| 400008        |400                    | The time period should be within {duration} months.
| 400009        |400                    | Parameter '{param}' is outside the number range, between {from} and {to}.
| 400010        |400                    | Parameter '{param}' length exceeded the limit of {length}.
| 400011        |400                    | You can only search for the records of the last {duration} months.
| 403000        |403                    | Access denied.
| 403001        |403                    | Your accout has been closed.
| 403002        |403                    | Your accout is not available.
| 403003        |403                    | You do not have '{permission}' permission.
| 403004        |403                    | You have license(s) expired, or your current agent count has exceeded the total valid licenses. Please add new licenses to avoid any service interruption.
| 403005        |403                    | There are no licenses in your account. Please contact your account manager to purchase new licenses.
| 404000        |404                    | {url} not found.
| 404001        |404                    | {object} with ID {id} does not exists.
| 409000        |409                    | {object} with name {name} already exists.
| 500010        |500                    | You have reached the daily API calling limit: {times}. If you want to increase your API calling times, please contact us at: {email}.

  - error code范围  

|model          | error Code                                                                                                                 
| ------------- |------------------------------- 
| Common        |400000 – 600000 (不包括600000，下同)
| Livechat      |1000000-1100000
| KB            |1100000-1200000
| Social        |1200000-1300000
| Ticket        |1300000-1400000  
| Bot           |1500000-1600000  

### Javascript API Error
  1. 异步的调用，通过Promise返回，如果是错误的情况就从reject返回，参数为Error错误对象，该对象为JS 内置的对象, 可以通过`new Error("Input is not a number")`来生成对象，拥有属性description.
  2. 同步的调用，直接抛出异常

### Webhook API  Error
  详情请参考[Webhook API](#webhook-api)。


## Response Format
  1. Restful API只提供json的返回格式，不支持xml和jsonp的返回格式
    - 返回类型，根据Method
      + GET, 一般为查询，返回具体的对象或对象列表
      + POST, 一般为新增，返回新增的对象
      + PUT, 一般为修改，返回修改以后的对象
      + DELETE，一般为删除，返回空，（如果成功的话就只有200状态码）
    - 如果GET的时候有分页，则要返回除结果之外的内容
      + 返回对象, 包含查询的结果以及所有的记录数，以tickets查询为例

  ```json
  {
    "tickets": [
      // ticket
      // ...
      ],
  "total": 188
  }

  ```
  2. JS API
    - Agent Console API
        + 异步调用，返回promise
    - Visitor Side API
        + 同步返回js对象
        + 异步调用，返回promise