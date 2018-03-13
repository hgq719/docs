# General

1. [Role](#role)
2. [Deployment](#deployment)
3. [Partner Object](#partner-object)
4. [Open Account](#partner-open-account)
5. [Integration Ways](#integration-ways)

## Role
  - Comm100 
  - Partner -合作伙伴，需要集成Comm100产品的客户，如某个PhoneCall公司。Comm100的代理商
  - 客户 - 合作伙伴的客户

## Deployment

合作伙伴可以选择直接使用Comm100的Partner平台，或者选择单独部署一个平台。Partner平台使用二级域名来区分不同的Partner (如：cisco.comm100.com, avaya.comm100.com)，而单独部署平台则可以使用用户自己的域名(如：chat.cisco.com)。

每一个Partner在部署时需要确定几个内容
1. 样式，每一个Partner可以定义一套自己的前端样式，由Comm100根据对方的需求来定义， Partner客户打开Live Chat产品会显示Partner定义的样式
  - 样式通过静态资源的UrlRewrite来完成，不同二级域名下的静态资源重写到指定的目录下面
2. Branding/Logo，Partner可以定义自己的Branding以及Logo，这些会显示在界面中
3. Agent Console Desktop/iOS/Android客户端需要为每个客户单独编译，iOS和Android需要手动发布到App Store和Google Play。不同Partner的客户端不能登录到其他Partner下面站点

## Partner Configuration
  Parter在使用Comm100的产品之前，必须要进行相应的配置。如下所示：
  1. 基本信息 -包括名字、邮箱、电话号码等  
  2. IP白名单 -配置使用Comm100的Partner API的IP白名单  
  3. SSO配置 -Partner根据自己的需求，进行相应的SSO配置  
  4. Branding/Logo -配置Partner的品牌信息以显示在相应的界面中  

## Partner Object
  Comm100中的Partner对象包括下面的属性：  
  + 基本信息
    - `id` -主键id
    - `name` -Partner的name
    - `email` -Partner的email地址
    - `phone` -Partner的电话号码
    - `ifActive` -该Partner是否处于激活状态
    - `siteList` -该Partner对应的所有站点的列表
      * `siteObject` -Site对象
  + 样式控制
    - `css` -使用哪套样式
  + Partner API的验证信息, Partner用以下内容来调用Partner API
    - `apiKey` -Partner调用Api时使用的apiKey，使用basic partner_id:api_key来访问API 
    - `ipWhiteList` -允许Partner使用Comm100的Partner API的IP白名单
  + Partner Site的Agent的验证方式配置
    - [SSO Settings](#sso-settings) -SSO配置  
    - No SSO  
       Partner的Site不使用SSO的情况，Agent默认采用Comm100的标准身份认证方式进行验证，在未认证的情况下，重定向到Comm100的登录页面进行登录，如`https://www.comm100.com/secure/login.aspx`。

#### SSO Settings
  - SAML
    + `cert` -SAML Certificate
    + `endpoint` 
      * `loginUrl`   
        SAML方式配置的登录页面，如：`https://partnerCompany.com/services/login.html`
      * `logoutUrl`   
        SAML方式配置的登出页面，如：`https://partnerCompany.com/services/comm100_logout.html`   
  - JWT
    + `secret` -Comm100与Partner之间用于jwt签发和验证的密钥,可使用api_key作为该密钥
    + `endpoint`
      * `loginUrl`   
        JWT方式配置的登录页面，如：`https://partnerCompany.com/services/login.html`
      * `logoutUrl`   
        JWT方式配置的登录页面，如：`https://partnerCompany.com/services/comm100_logout.html`

### Account Login Integration
  Partner可以使用两种方式进行登录验证的集成：NoSSO和SSO。使用NoSSO的方式集成，Agent在登录到Partner的Site以后还需要重新进入到Comm100的登录页面认证完成使用Comm100的功能；而使用SSO的方式，Partner的用户可以在登录自己的系统以后，直接使用嵌入在自己系统中的Comm100的页面、组件或Api，不需要再进行其他认证了。目前Comm100 提供两种SSO登录验证集成的方式, 一种为基于[SAML2.0](https://en.wikipedia.org/wiki/SAML_2.0), 另一种为[JWT](http://self-issued.info/docs/draft-ietf-oauth-json-web-token.html)。
1. SAML

  签名验证服务endpoint：  
     `https://partnerSecondDomain.comm100.com/sso/saml/acs`

  流程
  - 未认证的用户在请求Comm100的资源时，被重定向到Partner配置SAML SSO的Login URL地址  
  - Partner对用户身份进行认证，认证完成向Comm100返回SAML身份认证Response并重定向到Comm100的SAML的endpoint：`https://partnerSecondDomain.comm100.com/sso/saml/acs`  
  - Comm100对SAML Response进行验证，验证成功完成Agent的认证，并重定向到Agent请求的资源  

2. JWT

 State - support cookie

  身份认证endpoint:
   - `https://hosted.comm100.com/sso/jwt?jwt=xxx.xxx.xx&return_to=https://hosted.comm100.com/livechatdashboard/dashboard.aspx?siteId=111111`

  参数说明
  - `jwt`
      jwt中包含三部分内容：Header头部、[Payload负载](#jwt-payload)和Signature。将header和payload使用Base64编码，Signature根据编码后的header、payload和特定的密钥(Comm100为每个Partner生成的特定密钥)，使用header中指定的签名算法(HS256)进行签名。
  - `return_to` -身份验证通过后浏览器重定向的页面
  
  流程
  - 未认证的用户在请求Comm100的资源时，被重定向到Partner配置的JWT SSO的Login Url地址  
  - 由Partner对Agent进行身份认证，构建一个包含身份信息的JWT，并重定向到Comm100的Endpoint：`https://hosted.comm100.com/sso/jwt`   
  - Comm100解析JWT完成Agent的认证   
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

### JWT Payload
  JWT的Payload中包含以下参数：
  * `iat` - JWT的发行时间
  * `jti` - JWT的唯一ID
  * `email` - 登录用户的email地址
  * `name` - 登录用户的名称
  * `userId` - 用户系统中的唯一标识这个用户的id, 可以为email/phone, 也可以是自己的id, 只需要保证唯一
  * `phone` - 电话号码

## Partner API
   Partner通过下面的Api给他的客户开户，创建[Site Object](#site-object)，维护自己客户的对应站点，Partner API不支持跨域请求。
   
   开发者需要通过下面的API来向Comm100请求访问API的token。

  `GET https://hosted.comm100.com/auth/token`

  Request Parameters:
  - `client_id` -用户的唯一id，如agentId，必须指定。
  - `api_key` -访问Api时使用的key，Agent只能访问自己所属站点的数据

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

### Site Object
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

## Integration Ways
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
    Partner通过调用Comm100的RESTful API，自己构建界面或后台来完成特定功能和逻辑。API的调用采取[OAuth](https://github.com/hgq719/docs/blob/master/IntegrationRestfulAPI.md#authentication)的方式进行身份验证.
  - App集成    
    目前Comm100对于移动端App的集成采用的是单独App方式，可通过WebView或者原生App直接打开，暂时不考虑深度集成。  

### UI Integration
  Partner可采用以下的方式将Comm100的页面集成到自己的系统中：
  - iframe嵌入页面
     通过iframe的src设置Comm100的页面。该方式可以让Partner将Comm100的菜单、header、footer隐藏起来，使用Partner自己的相关部分。但是这种方式交互的内容只影响到该iframe，如弹出框。
  - 直接指定页面地址
     通过直接指定页面地址嵌入整个Comm100的页面。
  Comm100提供的可供Partner集成的界面如下：  
  - [Control Panel UI](#control-panel-ui)
  - [Agent Console UI](#agent-console-ui)

#### Control Panel UI
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
     + Chat Button   
        `https://hosted.comm100.com/LiveChatFunc/CodePlan/ChatButton.html?siteId=000000&codePlanId=1234`   
     + Chat Window   
        `https://hosted.comm100.com/LiveChatFunc/CodePlan/ChatWindow.html?siteId=000000&codePlanId=1234`   
     + Pre-Chat   
        `https://hosted.comm100.com/LiveChatFunc/CodePlan/PreChat.html?siteId=000000&codePlanId=1234`   
     + Post-Chat   
        `https://hosted.comm100.com/LiveChatFunc/CodePlan/PostChat.html?siteId=000000&codePlanId=1234`   
     + Offline Message   
        `https://hosted.comm100.com/LiveChatFunc/CodePlan/OfflineMessage.html?siteId=000000&codePlanId=1234`   
     + Invitation   
        `https://hosted.comm100.com/LiveChatFunc/CodePlan/Invitation.html?siteId=000000&codePlanId=1234`   
     + Agent Wrap-up   
        `https://hosted.comm100.com/LiveChatFunc/CodePlan/OperatorWrapup.html?siteId=000000&codePlanId=1234`   
     + Language   
        `https://hosted.comm100.com/LiveChatFunc/CodePlan/Language.html?siteId=000000&codePlanId=1234`   
     + Routing Rules   
        `https://hosted.comm100.com/LiveChatFunc/CodePlan/RoutingRules.html?siteId=000000&codePlanId=1234`   
     + ChatBot   
        `https://hosted.comm100.com/LiveChatFunc/CodePlan/ChatBot.html?siteId=000000&codePlanId=1234`   
     + Multiple Campaigns   
        `https://hosted.comm100.com/LiveChatFunc/PlanList.html?siteId=000000&codePlanId=1234`   
   - Settings配置 -具有Settings管理权限的人可以通过下面的界面进行相应的配置
     + Canned Messages   
        `https://hosted.comm100.com/LiveChat/CannedMessageList.html?siteId=000000`   
     + Departments   
        `https://hosted.comm100.com/LiveChat/Departments.html?siteId=000000`   
     + Auto Allocation   
        `https://hosted.comm100.com/LiveChat/ChatsAutoAllocation.html?siteId=000000`   
     + Custom Away Status   
        `https://hosted.comm100.com/LiveChat/CustomAwayStatus.html?siteId=000000`   
     + Auto Translation   
        `https://hosted.comm100.com/LiveChat/AutoTranslation.html?siteId=000000`   
     + Ban List   
        `https://hosted.comm100.com/LiveChat/BanList.html?siteId=000000`   
     + Visitor Sementation   
        `https://hosted.comm100.com/LiveChat/CustomerSegmentationList.html?siteId=000000`   
     + Visitor Single Sign-On    
        `https://hosted.comm100.com/LiveChat/SingleSignOnSettings.html?siteId=000000`   

#### Agent Console UI Integration
  Agent Console中Partner可用于集成的界面如下：     
  - Agent Console -整个Agent Console页面，包含Agent Console的所有功能（Settings、状态切换、Visitors等）   
    `https://hosted.comm100.com/LiveChat/AgentConsole.html?siteId=000000`  
  - Settings -Agent Console的Preference Settings页面  
    `https://hosted.comm100.com/LiveChat/AgentConsole/Settings.html?siteId=000000`  
  - Visitor -当前可用的访客列表   
    `https://hosted.comm100.com/LiveChat/AgentConsole/Visitors.html?siteId=000000`  
  - MyChats -当前agent正在进行的聊天列表   
    `https://hosted.comm100.com/LiveChat/AgentConsole/MyChats.html?siteId=000000`  
  - CurrentChat -当前agent当前正在进行的聊天窗口，可以考虑包含右侧的Tab区域   
    `https://hosted.comm100.com/LiveChat/AgentConsole/CurrentChat.html?siteId=000000`  
  - Agents -当前在线的agent列表   
    `https://hosted.comm100.com/LiveChat/AgentConsole/Agents.html?siteId=000000`  

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
    app.do('login',{
        type: 'jwt',
        data: 'xxx.xxx.xx',
        // type: 'password',
        // data: {
        //   email: 'allon@comm100.com',
        //   password: 'Aa000000',
        // },
      }
    );
    app.do('display', 'chats'); // show chats module

    const visitors = app.get('visitors');

    app.do('acceptChat', visitorId); // accept chat
  ```
  
  Comm100将系统中的部分功能编译成了组件，Partner可以通过引入这些组件，将功能集成到自己的系统中供客户使用，目前Comm100提供下面的js组件：  
  - [visitors](#visitors-module) - 访客列表, 只有modules中包含了该模块才会显示
  - [chats](#chats-module) - 聊天列表以及聊天窗口

#### Visitors Module
  在visitors模块中，Partner可用的对象、属性、时间及操作为：
  - Objects
    + Visitor
  - Properties
    + `visitors` -访客模块中的在线访客列表
    ```javascript
      const visitors = app.get('visitors');
    ```
  - Events -在模块的配置中，Partner可以在visitor的这些事件中添加自己的操作
    + `enterSite` -访客进入站点
    + `leaveSite` -访客离开站点
  - [Actions](#visitors-actions)

##### Visitors Actions
  在visitors模块中，Partner可用的操作如下：
  - refuse -拒绝当前访客的聊天  
  ```javascript
    app.do('refuse', visitorId); // refuse chat
  ```
  - invite -邀请当前访客进行聊天
  ```javascript
    app.do('invite', visitorId); // invite chat
  ```
  - capture -将当前访客固定在访客列表中，不管访客是否退出站点都显示在列表中
  ```javascript
    app.do('capture', visitorId); // capture chat
  ```
  - release -将当前访客从capture状态释放，访客退出站点后将从访客列表中消失
  ```javascript
    app.do('release', visitorId); // release chat
  ```
  - ban -禁止当前访客聊天，且让访客不显示在列表中
  ```javascript
    app.do('ban', visitorId); // ban chat
  ```
  - join -加入当前访客正在进行的聊天
  ```javascript
    app.do('join', visitorId); // join chat
  ```
  - monitor -监视当前访客正在进行的聊天
  ```javascript
    app.do('monitor', visitorId); // monitor chat
  ```

#### Chats Module
在chats模块中，Partner可用的对象、属性及操作为：
  - Objects
    + Chat
      * `chatId` -聊天主键id
      * `messages` -聊天信息
      * `visitor` -聊天访客
  - Properties
    + `chats` -当前Agent正在进行的聊天列表
    ```javascript
      const chats = app.get('chats');
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
    app.do('leave', chatId); // leave chat
  ```
  - ban -禁止当前访客聊天，且让访客不显示在列表中
  ```javascript
    app.do('ban', visitorId); // ban chat
  ```
  - promote -将当前visitor变成user或者是contact
  ```javascript
    app.do('promote', visitorId，'user'); // promote to a user
    app.do('promote', visitorId，'contact'); //promote to a contact
  ```
  - sendMessage -在当前聊天中发送一条信息
  ```javascript
    app.do('sendMessage', chatId, message); // send a message
  ```

### API Integration
  - Partner API
    + [Site Managment](#site-managment)
  - Account Managment API
    + [Agent Managment](https://www.comm100.com/doc/api/operators.htm)
    + [Department Managment](https://www.comm100.com/doc/api/departments.htm)
  - [Authority Manage API](https://github.com/hgq719/docs/blob/master/IntegrationRestfulAPI.md#authority-managment-api)  
  - Control Panel
    + [Campaign API](https://github.com/hgq719/docs/blob/master/IntegrationRestfulAPI.md#campaign-api)
    + [Settings API](https://github.com/hgq719/docs/blob/master/IntegrationRestfulAPI.md#settings-api)
    + [Report API](#report)
  - [Agent Console API](#agent-console-api) 


### Report
  用户可以通过ReportApi获取到报表数据，集成到自己的报表系统中，ReportApi的详情可参考[Report API](https://gist.github.com/chendesheng/50e9b63573f09a1c1a76c1f4ec074ac9)。部分报表如果不考虑深度集成，也可采用界面集成的方式直接将该报表的UI集成到Partner的界面中。