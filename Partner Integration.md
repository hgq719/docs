# General
1. [业务目标](#business-goals)
2. [角色定义](#role-definition)
3. [业务场景](business-scenario)
3. [需求分析](#requirement-analysis)
4. [设计与实现](#design-implementation)

## Business Goals
1. 企业客户成为Comm100的代理商，通过简单的配置，将Comm100产品直接销售给他的客户。
2. 企业客户利用Comm100的开放性，将Comm100的产品集中到自己的产品中，丰富自己的功能，加强自己产品的黏性。
3. Comm100借助合作伙伴的产品、销售等能力，与合作伙伴进行联合销售，实现双赢。

## Role Definition
 - Comm100 
 - Partner -合作伙伴
   + 代理商 -作为Comm100的代理商，销售Comm100的产品的企业
   + 集成商 -需要将Comm100产品集成到自己产品中的企业
 - 客户 -合作伙伴的客户，每个客户有自己的站点
 - Agent -客服，隶属于合作伙伴的客户

## Business Scenario
1. Partner自定义一套Comm100的产品，直接将这个自定义产品卖给他的客户，供其使用。  
2. Partner将Comm100产品的功能集成到自己的系统中，提供给他的客户使用。

## Requirement Analysis
1. Partner注册   
  企业可以通过Comm100提供的入口注册成为一个Partner，注册的过程中需要提供企业的名字、联系人及其电话号码、邮箱及其他一些必要信息，注册提交后由Comm100进行审核，审核通过以后Comm100会给企业生成一个Parter账号，该账号可以登录Partner应用系统。Comm100对于Partner的审核过程，包括资质审核、与Partner沟通使用说明、合作方式等。

2. Partner管理系统     
  该系统用于Comm100管理自己的Partner，查看Partner的相关报表及账单信息等。

3. Partner应用系统  
  Partner应用系统为Partner用于管理客户及相关配置的应用系统，Partner应用系统中，Partner应该可以使用下面的功能：  
  - 登录 -Partner可以登录Partner应用系统，     
  - 维护基本信息 -Partner可以维护自己的基本信息，包括联系人、电话号码、邮箱等。
  - 定制Branding/Logo -Partner可以定义自己的Branding/Logo，让客户看到的产品直观上是属于Partner的系统
  - 定制Theme -Partner可以根据自己的需求定义一套自己的前端样式
  - 开户 -Partner可以通过Comm100提供的界面或Api来给自己的客户开户
  - 客户管理 -Partner可以管理自己开户的客户，如关闭或激活某个客户的站点  

4. 功能集成    
  - Partner没有自己的产品，通过代理Comm100的产品及Branding/Logo的配置，将系统出售给他的客户使用，对客户的身份认证也完全采用Comm100的账号系统进行认证。客户可使用Comm100产品提供的所有权限内的功能。
  - Partner需要将Comm100的功能集成到自己的系统中，可以采取Api或界面集成。如果是界面集成的情况，Partner可以自主的选择界面的Header、Footer和菜单的可见性。客户可使用Partner集成到自己系统中的功能。
    + 界面集成  
      * 用户可以直接使用链接或者iframe引用Live Chat后台管理界面
      * 用户可以在引入界面时去掉头， 脚，菜单
      * 用户可以使用自己的账号系统来通过认证
    + API集成   
      * 用户可以通过API管理站点的Agent信息, 权限
      * 用户可以通过API管理Campaign, Canned Message等配置信息
      * 用户可以通过API获取Report数据, 集成在统一的Report模块
      * 用户可以通过API控制Agent的状态, 操作Chat

5. 配置
  为了让Partner的客户能够方便的使用系统，Partner需要进行以下的配置，这些配置也需要在Partner应用系统中添加入口：   
  - SSO -Partner可以配置相应的SSO，使用自己的账号系统对客户的Agent进行身份认证。Agent无需输入单独的凭证就可以访问Comm100。
  - OAuth客户端 -Partner需要调用RestfulApi来访问用户数据时则必须申请OAuth客户端。
  - IP白名单 -使用Comm100的Partner API的IP白名单 

6. 部署
   Comm100可以根据Partner的需求来选择系统的部署方案：  
   + Partner公共平台 -Partner平台使用二级域名来区分不同的Partner ，如`cisco.comm100.com`、`avaya.comm100.com`。
   + 单独部署 -Partner使用自己的独立域名，如`chat.cisco.com`。
   Desktop/Mobile版本的系统需要由Comm100进行独立编译以后，交由Partner给客户使用。一般来说这种版本的系统需要一定的周期才能完成，特别是iOS版本需要Apple公司的审核通过后才能进行发布。

7. 收费
  Partner及其客户的收费目前可考虑两种方案：  
  1. Partner客户的账单统一由Comm100并收取费用，Comm100再根据Partner的情况进行相应的分成。
  2. Partner直接在Comm100的Partner账号系统中充钱，充多少用多少。

## Design & Implementation
  - Partner账号系统
    + [Partner Object](#partner-object)
    + [Partner Configuration](#partner-configuration)
    + [Partner API](#partner-api)
  - Agent Login Integration
    + Comm100账号系统 -Partner直接使用Comm100的账号系统对Agent身份进行认证
    + [Agent SSO Login & Logout](#agent-sso-login-logout)
  - [Integration Ways](#integration-ways)

### Partner Object
  Comm100中的Partner对象包括下面的属性：  
  + 基本信息
    - `id` - Partner的唯一Id
    - `name` - Partner的名字
    - `contactName` - Partner的联系人名字
    - `contactEmail` - Partner的联系人邮箱
    - `phone` - Partner的电话号码
    - `isActive` - 该Partner是否处于激活状态
  + 样式控制
    - `theme` - 该partner使用的主题名字, 包含对应的资源和样式, 如果需要Comm100会为Partner创建对应的主题, 由Comm100维护, Partner不能修改
  + Partner API的Credentials
    - `apiKey` - Partner调用Api时使用的apiKey换取access_token来访问Partner API，Comm100自动生成 
    - `ipRestrictions` - 允许调用Comm100的Partner API的IP
  + Partner Site的Agent的验证方式配置
    - [SSO Settings](#sso-settings) -SSO配置
  + OAuth客户端配置
    - `client_id` -Partner调用Api请求客户的数据时使用的`client_id`换取access_token，Comm100自动生成
    - `client_secret`-Partner调用Api请求客户的数据时使用的`client_secret`换取access_token，Comm100自动生成

#### SSO Settings
- SAML
    + `cert` -SAML Certificate
    + `endpoint` 
      * `loginUrl`   
        SAML方式配置的登录页面，如：`https://partnerCompany.com/saml/sso`
      * `logoutUrl`   
        SAML方式配置的登出页面，如：`https://partnerCompany.com/logout`   
  - JWT
    + `endpoint`
      * `loginUrl`   
        JWT方式配置的登录页面，如：`https://partnerCompany.com/login`
      * `logoutUrl`   
        JWT方式配置的登录页面，如：`https://partnerCompany.com/logout`
    + `other instructions`
      * `alg` Comm100只支持HS256的加密算法
      * `signature` jwt的签名密钥使用上面的`apiKey`
  - `primarySSO` -主SSO，在SAML和JWT同时配置的情况下，Comm100可根据这个主SSO来选择重定向的登录页面
### Partner Configuration
  - 基本信息配置   
  Comm100提供相应的界面给Partner来维护自己的基本信息,包括`name`、`contactName`、`contactEmail`、`phone`
  - API访问权限配置  
  Comm100提供相应的界面给Partner配置需要访问Partner API的IP地址，`api_key`由Comm100自动生成
  - OAuth客户端申请    
  Comm100提供界面给Partner进行OAuth客户端申请，申请完成后自动生成`client_id`和`client_secret`
  - Branding/Logo配置、样式  
  Comm100提供界面给Partner来维护自己的Branding/Logo。前后端完全分离之前，样式由Comm100根据对方的需求来定义；前后端完全分离之后，由Comm100提供界面接口给Partner自己来配置。

#### Partner Table
t_Partner：Partner基础表，记录Partner基本信息  

| field | Description
| --- | ---
| `id` | the primary key of the partner.
| `name` | the name of the partner
| `contactName` | the name of the partner's contact
| `contactEmail` | the email of the partner's contact
| `phone` | the phone of the partner
| `isActive` | whether the partner is active or not, defaults to `true`
| `apiKey` | the key by which you can exchange the access_token when calling partner api
| `ipRestrictions` | the ip white list for calling partner api
| `client_id` | the id which you can exchange the access_token when requesting customer's data
| `client_secret` | the secret which you can exchange the access_token when requesting customer's data

   t_Partner_Config：Partner配置表，记录Partner的配置信息

| field | Description
| --- | ---
| `id` | the primary key of the partner config.
| `partnerId` | the primary key of the partner.
| `branding` | the branding text of partner
| `logo` | the url of partner's logo

  t_Partner_SSO：Partner SSO配置表，记录Partner的SSO配置信息
   
| field | Description
| --- | ---
| `id` | the primary key of the sso settings.
| `partnerId` | the primary key of the partner.
| `ssoType` | the type of sso which partner settings,including `SAML` and `JWT`
| `isPrimarySSO` | whether current SSO is primary way  or not, defaults to `false`
| `loginUrl` | the url of login
| `logoutUrl` | the url of logout

  t_Partner_Theme：Partner主题配置表，记录Partner的主题配置信息
   
| field | Description
| --- | ---
| `id` | the primary key of the css settings.
| `partnerId` | the primary key of the partner.
| `cssKey` | the primary key word of css, ie. `backgroundColor`
| `cssValue` | the value correspond to the primary key word of css,ie. `#1C86EE`

### Partner API
   Partner通过下面的Api给他的客户开户，创建[Site](#site-object)，维护自己客户的对应站点。Partner API不支持跨域请求， 即在跨域的情况下只允许后台调用，浏览器中不能调用。
   
   开发者需要通过下面的API来向Comm100请求访问API的token，Comm100再结合Partner配置的`ipRestrictions`中的IP来授权Partner API的访问。

  `GET https://hosted.comm100.com/partner/oauth/token`

  Request Parameters:
  - `grant_type` - `password`, 指定获取token的方式为password
  - `client_id` - partner id
  - `client_secret` - 访问Api时使用的key，Agent只能访问自己所属站点的数据

  Response示例：
  ```json
    Status: 200 OK

    {
      "access_token":"98asjdfka172dsfsd9s2342sdfs",
      "expires_in": "3600"
    }
  ```
  开发者可以通过上面获取的`access_token`来进行API调用，格式如下：

  `Authorization": "bearer {access_token}"`
     
  开户中，Partner可用的API如下：
  - `GET /api/v1/livechat/partner/sites` -获取当前Partner的所有客户的站点信息   
  - `GET /api/v1/livechat/partner/sites/{site_id}` -获取当前Partner的某一个站点的信息   
  - `POST /api/v1/livechat/partner/sites` -给自己的客户开户，新建一个[Site对象](site-object)，同时为这个Site对象生成一个管理员   
  - `PUT /api/v1/livechat/partner/sites/{site_info}` -更新Partner的某一个客户的站点信息
  - `PUT /api/v1/livechat/partner/sites/{site_id}/disable` -关闭Partner的某个客户的站点
  - `DELETE /api/v1/livechat/partner/sites/{site_id}` -给自己的客户销户，删除这个客户的站点信息

#### Site Object
  Comm100中Site对象包含下面的属性：
  - `id` -主键id
  - `company` -站点所属的公司name
  - `companySize` -公司规模
  - `website` -站点的网站地址
  - `phoneNumber` -电话号码
  - `mobilePhone` -手机号码
  - `country` -国家
  - `city` -城市
  - `ifClose` -是否关闭
  - `ifActive` -是否处于激活状态  
  还有一些其他属性待后续添加进来。  

### Agent SSO Login & Logout
  Partner所配置的站点下面的Agent采用SSO的方式进行身份校验，Agent可以在登录Partner的Site以后直接使用嵌入在partner系统中的Comm100的页面、组件或Api。Comm100提供了两种SSO登录验证集成的方式, 一种为基于[SAML2.0](https://en.wikipedia.org/wiki/SAML_2.0), 另一种为[JWT](http://self-issued.info/docs/draft-ietf-oauth-json-web-token.html)。

1. SAML 

  Comm100 Assertion Consumer Service Url：  
  - `https://partnerSecondDomain.comm100.com/sso/saml/acs`
  
  Comm100 Logout Url：
  - `https://partnerSecondDomain.comm100.com/sso/saml/logout`
     
  Login流程
  - 未认证的用户在请求Comm100的资源时，被重定向到Partner配置SAML SSO的Login URL,如：`https://partnerCompany.com/saml/sso？SAMLRequest=*****`，其中SAMLRequest为SAML的认证请求消息，由于认证请求通常为比较长的XML格式，需要压缩、编码后传输。

  ```xml
  <AuthnRequest  ID="sujg....sdflt" 
    Version="2.0" 
    IssueInstant="2018-03-22T09:28:50Z" 
    ProtocolBinding="urn:oasis:names:tc:SAML: 2.0:bindings:HTTP-POST" 
    ProviderName="comm100.com" 
    AssertionConsumerServiceURL="https://partnerSecondDomain.comm100.com/sso/saml/acs">
    <Issuer>comm100.com</Issuer>
    <NameIDPolicy  AllowCreate="true"
      Format="urn:oasis:names:tc:SAML:1.1:nameid-format:unspecified"/>;
  </AuthnRequest>
  ```
  - Partner对用户身份进行认证，认证完成向Comm100返回SAML身份认证Response并重定向到Comm100的SAML的endpoint：`https://partnerSecondDomain.comm100.com/sso/saml/acs`.

  ```xml
  <Response Version="2.0" 
    IssueInstant="2018-03-22T09:29:00Z" 
    Destination="https://partnerSecondDomain.comm100.com/sso/saml/acs" InResponseTo="sujg....sdflt">   
    <Issuer>https://partnerCompany.com/</Issuer>   
    <Status>
      <StatusCode   
        Value="urn:oasis:names:tc:SAML:2.0:status:Success"/> 
    </Status> 
    <Assertion Version="2.0" 
      IssueInstant="2018-03-22T09:29:00Z">     
      <Issuer>https://partnerCompany.com/</Issuer>   
      <Subject> 
        <NameID>kim</NameID>   
        <SubjectConfirmation ...> 
          <SubjectConfirmationData 
            NotOnOrAfter="2013-02-05T09:34:00Z"   
            Recipient="https://partnerSecondDomain.comm100.com/sso/saml/acs" InResponseTo="sujg....sdflt"/>  
          </SubjectConfirmation> 
      </Subject> 
      <Conditions NotBefore="2018-03-22T09:28:30Z" NotOnOrAfter="2018-03-22T09:34:00Z"> 
      </Conditions> 
      <AuthnStatement 
        AuthnInstant="2018-03-22T09:29:00Z" 
        SessionNotOnOrAfter="2018-03-22T17:29:00Z"> 
      </AuthnStatement> 
    </Assertion>
  </Response>
  ```
  - Comm100对SAML Response进行验证，验证成功完成Agent的认证，并重定向到Agent请求的资源。如：通过对上面的response进行验证，提取出Comm100能够识别的用户身份(NameID，即kim)，验证完成，kim将成功登陆Comm100，生成相应会话。
    
 Logout 
  - 已经认证的用户在Partner的账号系统中Logout的同时，需要将此用户的身份认证Response传给Logout Url，调用成功后Comm100注销当前用户的会话，用户在Comm100完成Logout。
  - 已经认证的用户在Comm100这边Logout的同时，Comm100会调用Partner在SSO中配置的Logout Url，调用成功后在Comm100注销当前用户会话的同时在Partner的系统中完成Logout。

2. JWT

 State - support cookie

  Comm100身份认证endpoint:
   - `https://hosted.comm100.com/sso/jwt?jwt=xxx.xxx.xx&return_to=https://hosted.comm100.com/livechatdashboard/dashboard.aspx?siteId=111111`

  Comm100 Logout Url：
   - `https://partnerSecondDomain.comm100.com/sso/jwt/logout?jwt=xxx.xxx.xx`

  参数说明
  - `jwt`
      jwt中包含三部分内容：Header头部、[Payload负载](#jwt-payload)和Signature。将header和payload使用Base64编码，Signature根据编码后的header、payload和特定的密钥(Comm100为每个Partner生成的特定密钥)，使用header中指定的签名算法(HS256)进行签名。
  - `return_to` -身份验证通过后浏览器重定向的页面
  
  Login流程
  - 未认证的用户在请求Comm100的资源时，被重定向到Partner配置的JWT SSO的Login Url地址，如：
     `https://partnerCompany.com/login?return_to=https://hosted.comm100.com/livechatdashboard/dashboard.aspx?siteId=111111`。
  - 由Partner对Agent进行身份认证，构建一个包含身份信息的JWT，并重定向到Comm100的Endpoint：`https://hosted.comm100.com/sso/jwt`   

  ```json
    head:
    {
      "typ":"JWT",
      "alg":"HS256"
    }

    payload:
    {
      "iss":"joe",
      "exp":1300819380,
      "sub":"comm100",
      "iat":1300809380
    }
  ```
  - Comm100解析JWT完成Agent的认证，生成相应会话   
  - 写cookie, 用来维护状态   

  移动App增加直接接收JWT登录认证的接口：  

   `Comm100://login?jwt=xx.xxx.xx`

  这个接口允许用户在打开上面的login接口的时候跳转到自己的APP中, 实现从自己的APP验证的业务, 用户验证完以后通过上面地址跳转回Comm100 APP
    
 iOS  
    
  ```objective-c
     NSURL* url = [NSURL URLWithString: @"Comm100://login?jwt=xxx.xxx.xx"];  
     [[UIApplication sharedApplication] openURL: url];  
  ```

  Android 
    
  ```java
    Intent intent = new Intent(Intent.ACTION_VIEW,Uri.parse("Comm100://login?jwt=xxx.xxx.xx"));
    startActivity(intent); 
  ```

 Logout 
  - 已经认证的用户在Partner的账号系统中Logout的同时，需要将此用户的身份认证Token传给Logout Url，调用成功后Comm100注销当前用户的会话，用户在Comm100完成Logout。
  `https://partnerSecondDomain.comm100.com/sso/jwt/logout?jwt=xxx.xxx.xx`   
  - 已经认证的用户在Comm100这边Logout的同时，Comm100会调用Partner在SSO中配置的Logout Url，调用成功后在Comm100注销当前用户会话的同时在Partner的系统中完成Logout。

### Integration Ways
  - [界面集成](#ui-integration)     
     通过直接指定Comm100的页面地址将Comm100的功能引入到Partner的界面中。主要是后台配置界面和Agent Console中的部分界面, 用户可以通过指定的url参数来控制页面中的部分内容，如头部，菜单等可以隐藏。Comm100将自己产品中的CSS抽象出来，Partner可以根据自己的需求，配置一套符合自己公司样式的产品给自己的客户使用，只是这部分样式的配置目前由Comm100进行配置。  
     以下以Campaign List为例：   
         
     `https://hosted.comm100.com/livechat/campaigns.aspx?siteId=10000118&onlyDisplayBody=true`   

     参数说明：     
      `onlyDisplayBody`: 是否只显示主体内容，true：只显示主体内容，菜单、header和footer隐藏；false：显示所有内容，即菜单、header、主体内容和footer。   
      `siteId`: Site主键，可关联到Partner，获取Partner配置的样式。   
    
      样式控制： 根据站点信息获取到partner的信息，加载partner中配置的样式文件   

  - [组件集成](#component-integration)        
     通过引入Comm100的组件代码将Comm100的功能集成Partner的页面中，这种方式需要Partner的终端支持Comm100的组件。目前只会考虑JS的组件, 用户可以通过这些组件重新编译生成自己的客户端。
  - [接口集成](#api-integration)       
    Partner通过调用Comm100的RESTful API，自己构建界面或后台来完成特定功能和逻辑。API的调用采取[OAuth](https://github.com/hgq719/docs/blob/master/IntegrationRestfulAPI.md#authentication)的方式进行身份验证。
  - App集成   
    目前Comm100对于移动端App的集成采用的是单独App方式，需要为每个Partner单独编译，iOS和Android需要手动发布到App Store和Google Play，可通过WebView或者原生App直接打开。不同Partner的客户端不能登录到其他Partner下面的站点。暂时不考虑深度集成。 

#### UI Integration
  Partner可采用以下的方式将Comm100的页面集成到自己的系统中：
  - iframe嵌入页面
     通过iframe的src设置Comm100的页面。该方式可以让Partner将Comm100的菜单、header、footer隐藏起来，使用Partner自己的相关部分。但是这种方式交互的内容只影响到该iframe，如弹出框。
  - 直接指定页面地址
     通过直接指定页面地址嵌入整个Comm100的页面。
  Comm100提供的可供Partner集成的界面如下：  
  - [Control Panel UI](#control-panel-ui)
  - [Agent Console UI](#agent-console-ui)

##### Control Panel UI
  Control Panel中Partner可用于集成的界面如下：     
   - Site管理
     + Site Profile -具有修改站点信息权限的人可以通过该页面修改站点的基本信息   
         `https://hosted.comm100.com/adminManage/adminPanel/siteProfile.html?siteId=000000`  
   - Agent管理
     + Agents
       * Agent Profile -具有Agent和Group管理权限的人可以通过该界面修改Agent的基本信息
          `https://hosted.comm100.com/adminManage/adminPanel/agentProfile.html?siteId=000000`  
     + Groups -具有Agent和Group管理权限的人可以通过该界面来维护Group
        `https://hosted.comm100.com/adminManage/adminPanel/agentGroup.html?siteId=000000`  
   - 权限配置
     + Permissions -站点管理员可以通过该界面配置Agent或者Group对应的权限
        `https://hosted.comm100.com/adminManage/adminPanel/permission.html?siteId=000000`  
     + IP Restrictions -站点管理员可以通过该界面配置需要限制访问的ip地址
        `https://hosted.comm100.com/adminManage/adminPanel/ipRestrictions.html?siteId=000000`  
   - Campaign配置 -具有Campaign管理权限的人可以通过下面的界面来对Campaign进行配置  
   - Settings配置 -具有Settings管理权限的人可以通过下面的界面进行相应的配置  

#### Agent Console UI
  Agent Console中Partner可用于集成的界面如下：     
  - Agent Console -整个Agent Console页面，包含Agent Console的所有功能（Settings、状态切换、Visitors等）   
    `https://hosted.comm100.com/LiveChat/AgentConsole.html?siteId=000000`  
  - Settings -Agent Console的Preference Settings页面  
    `https://hosted.comm100.com/LiveChat/AgentConsole/Settings.html?siteId=000000`  
  - Visitor -当前可用的访客列表   
    `https://hosted.comm100.com/LiveChat/AgentConsole/Visitors.html?siteId=000000`  
  - MyChats -当前agent正在进行的聊天列表，可以考虑包含右侧的Tab区域      
    `https://hosted.comm100.com/LiveChat/AgentConsole/MyChats.html?siteId=000000`  


### Agent Console Component Integration

  引用Comm100 Agent Console的JS SDK可以在自己的页面中轻松构建Agent Console, 可供用户集成的模块为visitors和chats, 

  ```javascript
    const container = document.getElement('container');
    const config = {
      server: 'https://partner.comm100.com',
      modules: ['visitors', 'chats'],
      visitors: {
        enterSite: enterSiteHandler,
        //...
      },
      chats: {
        startChat: startChatHandler,
        //...
      },
      display: 'visitors',  // default
    }
    const app = Comm100AgentConsole.init(container, config);    // 初始化app
    app.do('agentConsole.login',{
        type: 'jwt',
        data: 'xxx.xxx.xx',
        // type: 'password',
        // data: {
        //   email: 'allon@comm100.com',
        //   password: 'Aa000000',
        // },
      }
    );
    app.do('agentConsole.modules.display', 'chats'); // show chats module

    const visitors = app.get('agentConsole.visitors'); // get current visitor list

    app.do('agentConsole.chat.acceptChat', visitorId); // accept chat
  ```
  
  Comm100将系统中的部分功能编译成了组件，Partner可以通过引入这些组件，将功能集成到自己的系统中供客户使用，目前Comm100提供下面的js组件：  
  - [visitors](#visitors-module) - 访客列表, 只有modules中包含了该模块才会显示
  - [chats](#chats-module) - 聊天列表以及聊天窗口

#### Visitors Module
  在visitors模块中，Partner可用的对象、属性、时间及操作为：
  - Objects
    + `agentconsole.visitor`
  - Properties
    + `visitors` -访客模块中的在线访客列表
    ```javascript
      const visitors = app.get('agentConsole.visitors');
    ```
  - Events -在模块的配置中，Partner可以在visitor的这些事件中添加自己的操作
    + `agentconsole.visitor.enterSite` -访客进入站点
    + `agentconsole.visitor.leaveSite` -访客离开站点
  - [Actions](#visitors-actions)

##### Visitors Actions
  在visitors模块中，Partner可用的操作如下：
  - refuse -拒绝当前访客的聊天  
  ```javascript
    app.do('agentConsole.chat.refuse', visitorId); // refuse chat
  ```
  - invite -邀请当前访客进行聊天
  ```javascript
    app.do('agentConsole.chat.invite', visitorId); // invite chat
  ```
  - capture -将当前访客固定在访客列表中，不管访客是否退出站点都显示在列表中
  ```javascript
    app.do('agentConsole.chat.capture', visitorId); // capture chat
  ```
  - release -将当前访客从capture状态释放，访客退出站点后将从访客列表中消失
  ```javascript
    app.do('agentConsole.chat.release', visitorId); // release chat
  ```
  - ban -禁止当前访客聊天，且让访客不显示在列表中
  ```javascript
    app.do('agentConsole.chat.ban', visitorId); // ban chat
  ```
  - join -加入当前访客正在进行的聊天
  ```javascript
    app.do('agentConsole.chat.join', visitorId); // join chat
  ```
  - monitor -监视当前访客正在进行的聊天
  ```javascript
    app.do('agentConsole.chat.monitor', visitorId); // monitor chat
  ```

#### Chats Module
在chats模块中，Partner可用的对象、属性及操作为：
  - Objects
    + Chat
      * `agentConsole.chat.chatId` -聊天主键id
      * `agentConsole.chat.messages` -聊天信息
      * `agentConsole.chat.visitor` -聊天访客
  - Properties
    + `agentConsole.chats` -当前Agent正在进行的聊天列表
    ```javascript
      const chats = app.get('agentConsole.chats');
    ```
  - Events -在模块的配置中，Partner可以在聊天的这些事件中添加自己的操作
    + `startChat` -开始聊天的时候
    + `endChat` -结束聊天的时候
    + `receivedMessage` -agent接收到一条消息的时候
    + `sentMessage` -agent发送一条信息的以后
  - [Actions](#chats-actions)

##### Chats Actions
  在chats模块中，Partner可用的操作如下：
  - leave -离开当前聊天  
  ```javascript
    app.do('agentConsole.chat.leave', chatId); // leave chat
  ```
  - ban -禁止当前访客聊天，且让访客不显示在列表中
  ```javascript
    app.do('agentConsole.chat.ban', visitorId); // ban chat
  ```
  - sendMessage -在当前聊天中发送一条信息
  ```javascript
    app.do('agentConsole.chat.sendMessage', chatId, message); // send a message
  ```


### API Integration
  - Partner API
    + [Site Managment](#site-managment)
  - [Acount API](https://github.com/hgq719/docs/blob/master/IntegrationRestfulAPI.md#account-api)  
  - [LiveChat API](https://github.com/hgq719/docs/blob/master/IntegrationRestfulAPI.md#livechat-api)  
  - [Report API](#report)
  - [ChatServer API](#chatserver-api)

#### Report
  用户可以通过ReportApi获取到报表数据，集成到自己的报表系统中，ReportApi的详情可参考[Report API](https://gist.github.com/chendesheng/50e9b63573f09a1c1a76c1f4ec074ac9)。部分报表如果不考虑深度集成，也可采用界面集成的方式直接将该报表的UI集成到Partner的界面中。