# General
1. [Role](#role)
2. [Open Account](#open-account)
3. [Integration Ways](#integration-ways)
4. [Account Integration](#account-integration)
5. [Function Integration](#function-integration)

## Role
  - Comm100 
  - Partner -合作伙伴，需要集成Comm100产品的客户，如某个PhoneCall公司。Comm100的代理商
  - 客户 -合作伙伴的客户

## Open Account
   由Partner通过Api给他的客户开户，创建Site

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
    Partner通过调用Comm100的RESTful API，自己构建界面或后台来完成特定功能和逻辑。API的调用采取OAuth的方式进行身份验证： 
    + [发送Comm100授权页面给用户](#send-authorization-page)
    + [处理用户授权](#handle-authorization-decision)
    + [使用access_token调用API](#call-api) 

### Send Authorization Page
  开发者需要通过下面的API来向Comm100发起一个授权请求。

  `GET https://hosted.comm100.com/oauth/authorizations`

  Request Parameters:
  - `response_type` -授权类型，默认值`token`，必须指定。
  - `redirect_url` -指定用户授权以后的重定向页面，该url必须是一个绝对地址。必须指定。
  - `client_id` -App申请时给定的唯一id，必须指定。
  - `scope` -指定Comm100资源的访问权限列表，包括`read`、`write`，还可以指定访问特定的资源或所有资源，具体参考[Request Scope Setting](#request-scope-setting)，必须指定。
  - `state` -客户端的当前状态，任意值，认证服务器会原封不动的返回。

#### Request Scope Setting
  开发者可以指定`Scope`来控制App对Comm100资源的访问。`read`指定App有权限使用`GET`方式请求终端接口，`write`指定App有权限使用`POST`、`PUT`和`DELETE`方式请求终端接口来创建、更新和删除资源。可以同时给予两种`scope`设置，如：
  `scope=read write`

  另外，开发者还可以对特定的资源进行授权范围的设置，资源如下：
  - visitor
  - operater
  - chat
  - offlineMessage
  - department


  设置语法如下：`scope=resource:scope`,不指定资源则标识针对所有资源有效。
  单个资源请求设置如下： 


  `scope=offlineMessage:read`


  多个资源的请求设置如下：


  `scope=visitor:read visitor:write offlineMessage:read`

### Handle Authorization Decision
  当用户做出授权决策以后，开发者必须处理这个响应。如果用户决定授权给应用来访问自己在Comm100的资源，Comm100将在重定向页面地址的hash部分包含一个访问令牌，如：
  
  `{redirect_url}#access_token=98asjdfka1729&state=aaa&token_type=example&expires_in=3600`
     
### Call API
  开发者可以通过上面获取的`access_token`来进行API调用，格式如下：  

  `Authorization": "bearer {access_token}"`

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

#### Agent Console UI
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

### Component Integration
  Comm100将系统中的部分功能编译成了组件，Partner可以通过引入这些组件，将功能集成到自己的系统中供客户使用，目前Comm100提供下面的js组件：  
  - settings -当前agent的agent console配置
  - visitors -当前的访客列表
  - currentChat -当前正在进行的聊天
  - agents -当前在线的agent列表

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
    + [Report API](#report-managment)
  - [Agent Console API](#agent-console-api) 

#### Site Managment
  Partner可以通过下面的Api来完成开户，维护自己客户的对应站点。在Partner的账户系统中，每个[Partner对象](#partner-object)在生成的时候就对应生成了一个`api_key`，Partner可以通过这个`api_key`来进行下列这些API的访问。    
  - `GET /api/v1/livechat/partner/sites` -获取当前Partner的所有客户的站点信息   
  - `GET /api/v1/livechat/partner/sites/{site_id}` -获取当前Partner的某一个站点的信息   
  - `POST /api/v1/livechat/partner/sites` -给自己的客户开户，新建一个[Site对象](site-object)，同时为这个Site对象生成一个管理员   
  - `PUT /api/v1/livechat/partner/sites/{site_info}` -更新Partner的某一个客户的站点信息
  - `PUT /api/v1/livechat/partner/sites/{site_id}/disable` -关闭Partner的某个客户的站点
  - `DELETE /api/v1/livechat/partner/sites/{site_id}` -给自己的客户销户，删除这个客户的站点信息

##### Partner Object
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
    - [SSO Settings](#sso-settings)   
       SSO配置
    - No SSO  
       Partner的Site不使用SSO的情况，Agent默认采用Comm100的标准身份认证方式进行验证，在未认证的情况下，重定向到Comm100的登录页面进行登录，如`https://www.comm100.com/secure/Login.aspx`。

##### SSO Settings
  - SAML
    + `cert` -SAML Certificate
    + `endpoint` 
      * `loginUrl`   
        SAML方式配置的登录页面，如：`https://partnerCompany.com/services/login.html`
      * `logoutUrl`   
        SAML方式配置的登出页面，如：`https://partnerCompany.com/services/comm100_logout.html`   
  - JWT
    + `secret` -Comm100与Partner之间用于jwt签发和验证的密钥
    + `endpoint`
      * `loginUrl`   
        JWT方式配置的SSO登录页面，如：`https://partnerCompany.com/services/login.html`
      * `logoutUrl`   
        JWT方式配置的登录页面，如：`https://partnerCompany.com/services/comm100_logout.html`

##### Site Object
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

## Account Login Integration
  Partner可以使用两种方式进行登录验证的集成：NoSSO和SSO。使用NoSSO的方式集成，Agent在登录到Partner的Site以后还需要重新进入到Comm100的登录页面认证完成使用Comm100的功能；而使用SSO的方式，Partner的用户可以在登录自己的系统以后，直接使用嵌入在自己系统中的Comm100的页面、组件或Api，不需要再进行其他认证了。目前Comm100 提供两种SSO登录验证集成的方式, 一种为基于SAML2.0, 另一种为JWT。
1. SAML

  endpoint：  
     `https://partnerSecondDomain.comm100.com/sso/saml/acs`

  流程
  - 未认证的用户在请求Comm100的资源时，被重定向到Partner配置SAML SSO的Login URL地址  
  - Partner对用户身份进行认证，认证完成向Comm100返回SAML身份认证Response并重定向到Comm100的SAML的endpoint：`https://partnerSecondDomain.comm100.com/sso/saml/acs`  
  - Comm100对SAML Response进行验证，验证成功完成Agent的认证，并重定向到Agent请求的资源  

2. JWT

 State - support cookie

  endpoint:
   - `https://hosted.comm100.com/access/jwt?jwt=xxx.xxx.xx&return_to=https://hosted.comm100.com/livechatdashboard/dashboard.aspx?siteId=111111`

  参数说明
  - `jwt`
      jwt中包含三部分内容：Header头部、[Payload负载](#jwt-payload)和Signature。将header和payload使用Base64编码，Signature根据编码后的header、payload和特定的密钥(Comm100为每个Partner生成的特定密钥)，使用header中指定的签名算法(HS256)进行签名。
  - `return_to` -身份验证通过后用户将看到的页面
  
  流程
  - 未认证的用户在请求Comm100的资源时，被重定向到Partner配置的JWT SSO的Login Url地址  
  - 由Partner对Agent进行身份认证，构建一个包含身份信息的JWT，并重定向到Comm100的Endpoint：`https://hosted.comm100.com/access/jwt`   
  - Comm100解析JWT完成Agent的认证   
  - 写cookie, 用来维护状态   
  
### JWT Payload
  JWT的Payload中包含以下参数：
  * `iat` -JWT的发行时间
  * `jti` -JWT的唯一ID
  * `email` -登录用户的email地址
  * `name` -登录用户的名称
  * `externalId` -如果系统中不是通过email来唯一标识一个用户，则可用系统中的唯一id来标识这个用户
  * `phone` -电话号码
  * `user_fields` -json格式的其他自定义用户字段


### Report
  用户可以通过ReportApi获取到报表数据，集成到自己的报表系统中，ReportApi的详情可参考[Report API](https://gist.github.com/chendesheng/50e9b63573f09a1c1a76c1f4ec074ac9)。部分报表如果不考虑深度集成，也可采用界面集成的方式直接将该报表的UI集成到Partner的界面中。

### Agent Console API


## Account Integration
  + Account Manage -Partner可以直接通过接口创建、删除或修改Comm100的Agent或Department
     - New Agent -Partner可以在界面中选择自己系统中的某个/某些账户直接生成对应的Comm100 Agent
     - Delete Agent -Partner在删除自己的账户的同时删除相应的Comm100 Agent；或者只删除Comm100 Agent
     - New Department -Partner可以选择自己的系统中对应的Department生成对应的Comm100 Department,生成的同时可以选择性将该部门下面的人员自动生成Comm100 Agent并加入到当前部门中
     - Delete Department -Partner可以在删除自己的部门的同时删除相应的Comm100 Department；或者只删除Comm100 Department    
  + Authority Manage  
     - Partner可以在自己的用户管理界面中通过调用Comm100 RESTful API来配置自己系统中的账户在Comm100中权限。
  + Account Login    
     Comm100可以提供SSO和AD的身份认证方式，让Partner的用户可以在登录自己的系统以后   
     - 直接使用嵌入在自己系统中的Comm100的页面、组件或Api，不需要再进行登录, Comm100需要提供登录的方式和接口
     - 完全通过链接嵌入Agent Console，直接点击链接进入Agent Console

## Function Integration
  - [Agent Console](#agent-console)
  - [Control Panel Settings](#control-panel-settings)
  - [Report](#report)

### Agent Console
  将聊天功能集成到Partner的界面中，或者直接使用Comm100的Agent Console与访客进行聊天，查看访客列表等。

  UI & 功能
  + Visitors
      * visitors   
          Partner的Agent可以查看访客列表，并对访客列表进行相应操作
      * mychats    
          Partner的Agent可以与访客进行聊天
  + Settings： Partner可以在界面中使用Comm100 Agent Console中的Settings页面

Api      
+ 状态切换  
   Partner可以在界面中切换Comm100 Agent的状态或者切换自己系统中的状态的同时通过接口来改变Comm100 Agent的状态
+ 聊天的部分操作
  - ListVisitor -聊天访客列表
  - Accept -接受聊天
  - Refuse -拒绝聊天
  - Ban -Ban当前Visitor的Id或Ip
  - Invite -邀请访客进行聊天
+ ChatServer提供Api能够让Partner自己来构建自己的访客与客服的聊天  
  - Send -发送消息
  - Heartbeat -心跳包
  - GetMessage -获取聊天信息
  - Transfer -将当前聊天转交给其他Agent或ChatBot

 

