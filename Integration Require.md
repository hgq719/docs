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
         
     `https://hosted.comm100.com/livechat/campaigns.aspx?siteId=10000118&header=false&footer=false&jwt=xxxxx.xxx.xxxx`   

     参数说明：   
      header: 表示页头是否需要, 传false时隐藏页头   
      footer: 表示页脚是否需要, 传false时隐藏页脚   
      token: 用于jwt验证的token   
    
      样式控制： 根据站点信息获取到partner的信息，加载partner中配置的样式文件   

  - [组件集成](#component-integration)        
     通过引入Comm100的组件代码将Comm100的功能集成Partner的页面中，这种方式需要Partner的终端支持Comm100的组件。目前只会考虑JS的组件, 用户可以通过这些组件重新编译生成自己的客户端。
  - [接口集成](#api-integration)       
    Partner通过调用Comm100的RESTful API，自己构建界面或后台来完成特定功能和逻辑。API的调用采取OAuth的方式进行身份验证： 
    + [发送Comm100授权页面给用户](#send-authorization-page)
    + [处理用户授权](#handle-authorization-decision)
    + [从Comm100获取access_token](#get-access-token)
    + [使用access_token调用API](#call-api) 

### Send Authorization Page
  开发者需要通过下面的API来向Comm100发起一个授权请求。

  `GET https://hosted.comm100.com/api/v1/livechat/oauth/authorizations`

  Request Parameters:
  - response_type -默认证`code`，Comm100会根据要求返回一个Authorization Code，必须指定。
  - redirect_url -指定用户授权以后的重定向页面，该url必须是一个绝对地址。必须指定。
  - client_id -App申请时给定的唯一id，必须指定。
  - scope -指定Comm100资源的访问权限列表，包括`read`、`write`，还可以指定访问特定的资源或所有资源，具体参考[Request Scope Setting](#request-scope-setting)，必须指定。

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
  当用户做出授权决策以后，开发者必须处理这个响应。如果用户决定授权给应用来访问自己在Comm100的资源，Comm100将在重定向页面地址后添加一个授权码，如：
  
  `{redirect_url}?code=98asjdfka1729`

  如果用户拒绝授权给应用，Comm100则会在后面加上错误信息，如:

  `{redirect_url}?error=access_denied&error_message=****`

### Get Access Token
  开发者在收到Comm100给的`authorization_code`以后，可以通过下面的API来交换`access_token`。

  `POST https://hosted.comm100.com/api/v1/livechat/oauth/token`

  Request Parameters:
  - grant_type -指定授权类型，默认值为`authorization_code`，必须指定。
  - code -指定上面得到的`authorization_code`的值，必须指定。
  - api_key -用户访问API的key，必须指定。
  - agent_id -agent的唯一标识，必须指定。
  - redirect_url -授权完成后重定向页面，该url必须是一个绝对地址。必须指定。
  - scope -指定访问权限，默认值为`read`

  Request示例：
  ```json
    {
      "grant_type": "authorization_code",
      "code": "{authorization_code}",
      "api_key": "{api_key}",
      "agent_id" : "{agent_id}",
      "redirect_url":"{redirect_url}",
      "scope": "read"
    }
  ```
  Response示例：
  ```json
    Status: 200 OK

    {
      "access_token":"yhoaHL698huysOhs6a8e9HhoKdL",
      "token_type": "bearer",
      "scope": "read"
    }
  ```

### Call API
  开发者可以通过上面获取的`access_token`来进行API调用，格式如下：  

  `Authorization": "bearer {access_token}"`

### UI Integration
  Comm100提供的可供Partner集成的界面如下：  
  - [Control Panel UI](#control-panel-ui)
  - [Agent Console UI](#agent-console-ui)

#### Control Panel UI
  Control Panel中Partner可用于集成的界面如下：     
   - Site管理
     + Site Profile -具有修改站点信息权限的人可以通过该页面修改站点的基本信息
   - Agent管理
     + Agents
       * Agent Profile -具有Agent和Group管理权限的人可以通过该界面修改Agent的基本信息
     + Groups -具有Agent和Group管理权限的人可以通过该界面来维护Group
   - 权限配置
     + Permissions -站点管理员可以通过该界面配置Agent或者Group对应的权限
     + IP Restrictions -站点管理员可以通过该界面配置需要限制访问的ip地址
   - Campaign配置 -具有Campaign管理权限的人可以通过下面的界面来对Campaign进行配置  
     + Chat Button 
     + Chat Window
     + Pre-Chat
     + Post-Chat
     + Offline Message
     + Invitation
     + Agent Wrap-up
     + Language
     + Routing Rules
     + ChatBot
     + Multiple Campaigns
   - Settings配置 -具有Settings管理权限的人可以通过下面的界面进行相应的配置
     + Canned Messages
     + Departments
     + Auto Allocation
     + Custom Away Status
     + Auto Translation
     + Ban List
     + Visitor Sementation
     + Visitor Single Sign-On 

#### Agent Console UI
  Agent Console中Partner可用于集成的界面如下：     
  - Agent Console -整个Agent Console页面，包含Agent Console的所有功能（Settings、状态切换、Visitors等）
  - Settings -Agent Console的Preference Settings页面
  - Visitor -当前可用的访客列表
  - MyChats -当前agent正在进行的聊天列表
  - CurrentChat -当前agent当前正在进行的聊天窗口，可以考虑包含右侧的Tab区域
  - Agents -当前在线的agent列表

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
  - [Authority Manage API](#authority-managment-api)  
  - [Account Login](#account-login-api)    
  - Control Panel
    + [Campaign API](#campaign-api)
    + [Settings API](#settings-api)
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
  + Partner Site的验证方式
    - SSO
      * Cert
      * Endpoint
    - JWT
      * Cert

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

## Authority Managment API
  Partner可以在自己的用户管理界面中通过调用Comm100 RESTful API来配置自己系统中的账户在Comm100中权限，Comm100 Live Chat公开了下面的API来对站点下的权限资源进行操作：
  - Permission Managment  
    + `GET /api/v1/livechat/permisstions` -获取所有的Permission的信息   
    + `GET /api/v1/livechat/permisstions/{permission_id}` -获取指定的Permission的信息   
  - Permission Configuration
    + `GET /api/v1/livechat/agents/{agent_id}/permisstions` -获取当前agent的所有权限信息   
    + `POST /api/v1/livechat/agents/{agent_id}/permisstions` -给当前agent新增一个权限
    + `PUT /api/v1/livechat/agents/{agent_id}/permisstions/{permission_info}` -更新agent的某一个权限配置   
    + `DELETE /api/v1/livechat/agents/{agent_id}/permisstions/{permission_id}` -删除当前agent的某一个权限配置   

## Account Login API
   Comm100可以提供SSO的身份认证方式，让Partner的用户可以在登录自己的系统以后，直接使用嵌入在自己系统中的Comm100的页面、组件或Api，不需要再进行登录。Comm100提供了下面的API来进行SSO身份认证：   
   - `GET /api/v1/authentication/sso` -配置在Comm100的用户没有登录的情况下条状到特定的页面进行登录
   - `GET /api/v1/authentication/jwt` -Comm100
   - `POST /api/v1/authentication/jwt` -Comm100

## Account Login
  Comm100 提供两种登录验证集成的方式, 一种为基于SAML 2.0 的SSO, 另一种为JWT  
1. SSO

  endpoint：  
  `https://hosted.comm100.com/access/saml`

  流程
   - 配置SAML 
      + 一个SAML服务器，如MS AD或LDAP
      + SAML SSO登录地址
      + SAML证书
   - 用户在未授权的情况下，被重定向到SAML的SSO登录地址
   - 登录的用户访问一个远程资源，IDP会根据身份生成一个SAML Response，重定位到SP资源
   - SP解析SAML Response，验证用户是否合法并进行权限验证，成功则返回具体资源
2. JWT

 State - support cookie

  `https://hosted.comm100.com/access/jwt?jwt=xxx.xxx.xx&return_to=https://hosted.comm100.com/livechatdashboard/dashboard.aspx?siteId=111111`

  + 参数说明
    - jwt
      jwt中包含三部分内容：Header头部、[Payload负载](#jwt-payload)和Signature。将header和payload使用Base64编码，Signature根据编码后的header、payload和特定的密钥(Comm100为每个Partner生成的特定密钥)，使用header中指定的签名算法(HS256)进行签名。
    - `return_to` -身份验证通过后用户将看到的页面
  + 接口会做什么事情
    - 在启用SSO的情况下，对于未授权的用户直接根据配置进行登录页面的重定向
      * `https://hosted.comm100.com/access/sso` -配置在Comm100的用户没有登录的情况下跳转到特定的页面进行登录
    - 校验jwt的内容
      * Comm100会根据从JWT中解析的内容，在校验正确的情况下授权这个用户的会话
    - 会写cookie, 用来维护状态
  
### JWT Payload
  JWT的Payload中包含以下参数：
  * `iat` -JWT的发行时间
  * `jti` -JWT的唯一ID
  * `email` -登录用户的email地址
  * `name` -登录用户的名称
  * `externalId` -如果系统中不是通过email来唯一标识一个用户，则可用系统中的唯一id来标识这个用户
  * `phone` -电话号码
  * `user_fields` -json格式的其他自定义用户字段

## Campaigns API
  Comm100 Live Chat公开了下面的API来对站点下的[Campaign Object](#campaign-object)资源进行操作：  
`GET /api/v1/livechat/campaigns` -Get list of campaigns  
`GET /api/v1/livechat/campaigns/{id}` -Get a single campaign  
`DELETE /api/v1/livechat/campaigns/{id}` -Delete a campaign  

`GET /api/v1/livechat/campaigns/{campaign_id}/chatButton` -Get chatButton info for a campaign    
`GET /api/v1/livechat/campaigns/{campaign_id}/invitationButton` -Get invitationButton info for a campaign  
`GET /api/v1/livechat/campaigns/{campaign_id}/chatWindow` -Get chatWindow info for a campaign  
`GET /api/v1/livechat/campaigns/{campaign_id}/preChat` -Get preChat info for a campaign  
`GET /api/v1/livechat/campaigns/{campaign_id}/postChat` -Get postChat info for a campaign  
`GET /api/v1/livechat/campaigns/{campaign_id}/offlineMessage` -Get offlineMessage info for a campaign  
`GET /api/v1/livechat/campaigns/{campaign_id}/invitation` -Get invitation info for a campaign  
`GET /api/v1/livechat/campaigns/{campaign_id}/agentWrapup` -Get offlineMessage info for a campaign  
`GET /api/v1/livechat/campaigns/{campaign_id}/RoutingRules` -Get offlineMessage info for a campaign  
`GET /api/v1/livechat/campaigns/{campaign_id}/language` -Get offlineMessage info for a campaign  

`PUT /api/v1/livechat/campaigns/{campaign_id}/chatButton` -Update chatButton info for a campaign  
`PUT /api/v1/livechat/campaigns/{campaign_id}/invitationButton` -Update invitationButton info for a campaign  
`PUT /api/v1/livechat/campaigns/{campaign_id}/chatWindow` -Update chatWindow info for a campaign  
`PUT /api/v1/livechat/campaigns/{campaign_id}/preChat` -Update preChat info for a campaign  
`PUT /api/v1/livechat/campaigns/{campaign_id}/postChat` -Update postChat info for a campaign  
`PUT /api/v1/livechat/campaigns/{campaign_id}/offlineMessage` -Update offlineMessage info for a campaign  
`PUT /api/v1/livechat/campaigns/{campaign_id}/invitation` -Update invitation info for a campaign  
`PUT /api/v1/livechat/campaigns/{campaign_id}/agentWrapup` -Update offlineMessage info for a campaign  
`PUT /api/v1/livechat/campaigns/{campaign_id}/RoutingRules` -Update offlineMessage info for a campaign  
`PUT /api/v1/livechat/campaigns/{campaign_id}/language` -Update offlineMessage info for a campaign  

### Campaign Object
  Campaign对象包含以下属性：  
  - `id` -主键id
  - `siteId` -所属站点Id
  - [chatButton property](#chatButton-property)
  - [chatWindow property](#chatwindow-property)
  - [preChat property](#prechat-property)
  - [postChat property](#post-property)
  - [offlineMessage property](#offline-message-property)
  - [invitation property](#invitation-property)
  - [agentWrapup property](#agent-wrapup-property)
  - [routingRule property](#routing-rule-property)
  - [language property](#language-property)

#### ChatButton Property
  - `buttonType` -ChatButton的类型：0：ImageButton;1：LinkText;2：MonitorOnly;3: Adaptive
  - `ifFloat` -Chatbutton是否浮动
  - `buttonPosition` -Chatbutton的位置
  - `xOffset` -若XOffsetIfPixel=1则，该字段表示X坐标的偏移像素值;若XOffsetIfPixel=0则，该字段表示X坐标的偏移比例;
  - `xOffsetIfPixels` -ChatButtonXOffsetIfPixels	X坐标的偏移量是否为像素
  - `yOffset` -若YOffsetIfPixel =1则，该字段表示y坐标的偏移像素值;若YOffsetIfPixel =0则，该字段表示y坐标的偏移比例;
  - `yOffsetIfPixels` -Y坐标的偏移量是否为像素
  - `imageType` -ChatButtonImage的类型:0：Online;1：Offline;2：Invitation;3：InvitationAccept;4：InvitationRefuse;5：Brannding;6：Poweredby;7：WindowColorStyle
  - `onlineURL` -当Operator处于 online时chatbutton的链接
  - `onlineImageId` - 当Operator处于 online时chatbutton的图片
  - `offlineURL` -当Operator处于 offline时chatbutton的链接
  - `offlineImageId` -当Operator处于 offline时chatbutton的图片
  - `ifHideOffline` -Chatbutton在offline时是否隐藏
  - `routeToType` -Route类型：0：site;1: Department;2:RouteToOperator;
  - `routeToId` -如果route类型是2，则为OperatorId;如果route类型是1则为departmentId

#### ChatWindow Property
- `windowStyle`  -Chat window的类型：0 – Classic;1 – Circle;2 – Bubble
- `headerType`  -0 – Banner Image;1 – Operator Avatar & Company Logo;2:Agent Info
- `ifShowTitle`  -ChatWindowHeaderType为2时，该值有效:Chat Window Header是否显示Agent Title：0 – 不显示；1 – 显示
- `ifShowBio`  -ChatWindowHeaderType为2时，该值有效:Chat Window Header是否显示Agent Bio:0 – 不显示;1 – 显示
- `ifShowAvatar`  -ChatWindowHeaderType为1时，该值有效:0 – 不展示Avatar;1 – 展示Avatar
- `ifShowLogo`  -ChatWindowHeaderType为1时，该值有效:0 – 不展示Logo;1 – 展示Logo
- `logoImageId`  -Logo的ImageId
- `ifShowAvatar`  -Chat Window聊天内容区域是否显示Agent Avatar:0 – 不显示;1 – 显示
- `ifShowTexture`  -Chat Window聊天内容区域是否有背景:0 – 不显示;1 – 显示
- `contentTextureType`  -Chat Window聊天内容区域的背景类型
- `buttonColor`  -Adaptive Button的颜色
- `customCSSClassic`  -Classic的自定义CSS样式
- `customCSSCircle`  -Circle的自定义CSS样式
- `ifPrintTranscript`  -Chatwindow是否展示打印聊天记录
- `ifShowEmailButton`  -Chatwindow是否展示EmailButton
- `ifCanSwitchToOffline`  -Chatwindow能否转成offline
- `ifCanSendFile`  -Chatwindow能否传送文件
- `ifEnableAudioChat`  -Chat window是否开启Allow visitors to request audio chats
- `ifEnableVideoChat`  -Chat window是否开启Allow visitors to request video chats
- `ifEndChatWhenVisitorInactivity`  -Visitor处于Inactivity后是否结束chat
- `ifEnableSendTranscriptEmail`  -是否开启发送transcript
- `greetingMessage` -Greeting Message内容
- `ifEnableCustomJS`  -是否开启自定义js
- `customJS`  -用户自定义的JavaScript

#### PreChat Property
- `ifEnabled`  -是否允许Prechat
- `ifShowTeamName`  -Pre-Chat是否显示Team Name：0 – 不显示；1 – 显示
- `teamName` - Pre-Chat中team Name,PreChatHeaderIfShowTeamName为1时有效。
- `ifShowAgentAvatars`  -Pre-Chat是否显示Agent Avatars：0 – 不显示；1 – 显示
- `greetingMessage` -Greeting Message内容
- `socialLogin`	-社交媒体登录
  + `ifEnableGoogle`	-是否启用google登录
  + `ifEnableFacebook`	-是否启用Facebook登录
- `ifNotRecordCookie`	-Prechat是否记录cookie
- `windowFormStyle`	-ChatWindow表单样式
- `fields`  -Prechat页面自定义字段集合
  + [customField](#custom-field)  -自定义字段

##### Custom Field
- `id` -字段的主键
- `formType` -0-Pre-Chat Form;1-Offline Message Form;2-Post Chat Form;3-Wrap-up Form;4-PCI Form (在聊天结束后不存储，看不到该表单数据);5-Custom Variable
- `fieldId` -自定义字段Id
- `name` -自定义字段Name或者自定义变量的Name
- `value` -自定义字段的值或者自定义变量的值
- `url` -自定义变量的url

#### PostChat Property
- `ifEnabled`  -是否允许Postchat
- `greetingMessage` -Greeting Message内容
- `windowFormStyle`	-ChatWindow表单样式
- `fields`  -自定义字段集合
  + [customField](#custom-field)  -自定义字段

#### Offline Message Property
- `ifUseOfflineMessage`  -是否使用Comm100的OfflineMessage。0：不使用；1：使用
- `ifShowTeamName`  -OfflineMessageIfEnable为1时有效：Offline Message是否显示Team Name：0 – 不显示；1 – 显示
- `teamName` - Offline Message中team Name,OfflineMessageIfEnable为1时且PreChatHeaderIfShowTeamName为1时有效。
- `ifShowAgentAvatars`  -OfflineMessageIfEnable为1时有效：Offline Message是否显示Agent Avatars：0 – 不显示；1 – 显示
- `greetingMessage` -OfflineMessageIfEnable为1时有效：Greeting Message内容
- `windowFormStyle`	-OfflineMessageIfEnable为1时有效：ChatWindow表单样式
- `fields`  -OfflineMessageIfEnable为1时有效：自定义字段集合
  + [customFields](#custom-fields)  -自定义字段
- `ifOpenInNewWindow`  -OfflineMessageIfEnable为0时有效：OfflineMessage是否在新窗口打开
- `url`  -OfflineMessageIfEnable为0时有效：OfflineMessageURL

#### Invitation Property
- `invitationStyle` -邀请的样式：1：Bubble；2：Popup invitation image；3：Greeting message in chat window
- `autoInvitationRules` -自动邀请规则集合
  + [autoInvitation Rules](autoinvitation-rules) -自动邀请规则
- `manualInvitation` -手动邀请
  + [invitationButton property](#invitationbutton-property) -邀请按钮

##### InvitationButton Property
  - `invitationPosition` -邀请框的位置：0:Center with Overlay;1:Center;2:Top Left ;3:Top Middle; 4:Top Right;5:Bottom Left;6:Bottom Middle;7:Bottom Right
  - `xOffset` -若XOffsetIfPixel=1则，该字段表示X坐标的偏移像素值;若XOffsetIfPixel=0则，该字段表示X坐标的偏移比例;
  - `xOffsetIfPixels` -X坐标的偏移量是否为像素
  - `yOffset` -若YOffsetIfPixel =1则，该字段表示y坐标的偏移像素值;若YOffsetIfPixel =0则，该字段表示y坐标的偏移比例;
  - `yOffsetIfPixels` -Y坐标的偏移量是否为像素
  - `positionStyle` -Y坐标的偏移量是否为像素
  - `imageStyle` -图片类型：0：URL；1：from gallery  ；2：from my computer
  - `imageId` -图片ID
  - `noImageURL` -No图片的URL
  - `noImageId` -No图片ID
  - `yesImageURL` -Yes图片的URL
  - `yesImageId` -Yes图片ID
  - `closeAreaXOffset` -Close图标的x坐标
  - `closeAreaYOffset` -Close图标的y坐标
  - `closeAreaWidth`  -Close图标的宽度
  - `closeAreaHeight`  -Close图标的高度
  - `textAreaXOffset`  -Invitaion文本内容的x坐标
  - `textAreaYOffset`  -Invitaion文本内容的y坐标
  - `textAreaWidth`  -Invitaion文本内容的宽度
  - `textAreaHeight`  -Invitaion文本内容的高度
  - `text`  -Invitaion文本内容
  - `textFont`  -Invitaion文本内容字体
  - `textSize`  -Invitaion文本字体大小
  - `textIfBold`  -Invitaion文本内容是否加粗
  - `textIfItalic`  -Invitaion文本内容是否斜体
  - `textColor`  -Invitaion文本颜色

##### AutoInvitation Rule 
  - `id` -规则主键
  - `ifEnable` -是否启用
  - `order` -排序
  - [invitationButton property](#invitationbutton-property) -邀请按钮
  - `invitationConditions` -邀请条件集合
     + [condition Object](#condition-object)  -条件对象

##### Condition Object
  - `id` -条件主键
  - `enumRuleType` -0: DynamicCodePlan；1: RoutingRule；2:AutoInvitation；3:VisitorSegment
  - `ruleId` -对应rule的id
  - `displayId` -界面展示的rule序号
  - `variable` -条件的名称
  - `expression` -表达式枚举：0：is；1：contains；2：not contains；3：is more than；4：is less than；5：is not；6：not less than；7：not more than；8：regular expression
  - `value` -条件的值

#### Agent Wrapup Property
  - `wrapupFields`  -Wrapup页面自定义字段集合
    + [customField](#custom-field)  -自定义字段

#### Language Property
  - `language` -语言
  - `ifCustomizeLanguage` -是否使用自定义语言。0：不使用，使用默认语言 ；1：使用自定义语言
  - `ifRTL` -是否从右到左对齐，IfCustomizeLanguage为1时有效。
  - `buttonLanguages` -按钮对应的语言集合，IfCustomizeLanguage为1时有效。
    + `buttonLanguage` -按钮对应的语言。
      * `buttonName` -按钮的名字
      * `defaultText` -按钮显示的文字
      * `currentText` -按钮当前的文字
  - `fieldLanguages` -字段对应的语言集合，IfCustomizeLanguage为1时有效。
    + `fieldLanguage` -字段对应的语言。
      * `fieldName` -字段的名字
      * `defaultText` -字段显示的文字
      * `currentText` -字段当前的文字
  - `promptsLanguages` -提示对应的语言集合，IfCustomizeLanguage为1时有效。
    + `promptsLanguage` -提示对应的语言。
      * `prompt` -提示的名字
      * `defaultText` -提示显示的文字
      * `macro` -使用的宏
      * `currentText` -提示当前的文字
  - `systemMessageLanguages` -系统信息对应的语言集合，IfCustomizeLanguage为1时有效。
    + `systemMessageLanguage` -系统信息对应的语言。
      * `event` -事件的名字
      * `defaultText` -系统信息显示的文字
      * `macro` -使用的宏
      * `currentText` -系统信息当前的文字
  - `audioChatLanguages` -语言聊天对应的语言集合，IfCustomizeLanguage为1时有效。
    + `audioChatLanguage` -语言聊天对应的语言。
      * `audioChat` -语言聊天的名字
      * `defaultText` -语言聊天显示的文字
      * `macro` -使用的宏
      * `currentText` -语言聊天当前的文字
  - `videoChatLanguages` -视频聊天对应的语言集合，IfCustomizeLanguage为1时有效。
    + `videoChatLanguage` -视频聊天对应的语言。
      * `videoChat` -视频聊天的名字
      * `defaultText` -视频聊天显示的文字
      * `macro` -使用的宏
      * `currentText` -视频聊天当前的文字
  - `screenSharingLanguages` -屏幕分享时对应的语言集合，IfCustomizeLanguage为1时有效。
    + `screenSharingLanguage` -屏幕分享时对应的语言。
      * `screenSharing` -屏幕分享时的名字
      * `defaultText` -屏幕分享时显示的文字
      * `macro` -使用的宏
      * `currentText` -屏幕分享时当前的文字
  - `transcriptEmailtoVisitorsLanguages` -发送脚本邮件中对应的语言集合，IfCustomizeLanguage为1时有效。
    + `transcriptEmailtoVisitorsLanguage` -发送脚本邮件中对应的语言。
      * `transcriptEmail` -发送脚本邮件中的名字
      * `defaultText` -发送脚本邮件中显示的文字
      * `macro` -使用的宏
      * `currentText` -发送脚本邮件中当前的文字
  - `textonMobileBrowsersLanguages` -移动设备浏览器上中对应的语言集合，IfCustomizeLanguage为1时有效。
    + `textonMobileBrowsersLanguage` -移动设备浏览器上对应的语言。
      * `windowTitleOrOthers` -窗体标题或其他位置的名字
      * `defaultText` -默认显示的文字
      * `currentText` -当前的文字
  - `embeddedWindowLanguages` -嵌入窗体中对应的语言集合，IfCustomizeLanguage为1时有效。
    + `embeddedWindowLanguage` -嵌入窗体中对应的语言。
      * `embeddedWindow` -嵌入窗体的名字
      * `defaultText` -默认显示的文字
      * `macro` -使用的宏
      * `currentText` -当前的文字
  - `chatBotLanguages` -使用ChatBot时对应的语言集合，IfCustomizeLanguage为1时有效。
    + `chatBotLanguage` -使用ChatBot时对应的语言。
      * `chatBot` -使用ChatBot时对应时机的名字
      * `defaultText` -默认显示的文字
      * `macro` -使用的宏
      * `currentText` -当前的文字

#### Routing Rules Property
  - `ifEnableRoute` -是否启用路由规则
  - `routemethod` -0 - Route visitors to a specific department or operator；1 - Route visitors based on custom rules
  - [routeSpecificPoint](#route-specific-point) -路由到指定节点，Routemethod为0时有效
  - `routeRules` -路由规则集合，Routemethod为1时有效
    + [routeRule](#route-rule-object) -路由规则对象
  - `failRouteType` -0 – 未配置；1 – fail route to department；2 – fail route to operator；3 – redirect to offline message，Routemethod为1时有效
  - `failRouteId` - 失败时路由到的对应ID，Routemethod为1时有效
  - `failRouteMessageTo` -FailRouteType选择redirect to offline message时，填写的收邮件的Email，Routemethod为1时有效

##### Route Rule Object
  - `routeName` -当前路由的名称
  - `ifEnable` -是否启用当前这条路由规则
  - `order` -路由规则顺序
  - `routeConditions` -路由条件集合
     + [condition Object](#condition-object)  -条件对象
  - [routeSpecificPoint](#route-specific-point) -路由到指定节点  

##### Route Specific Point
  - `routeType` -路由类型：0:Department;1:Agent
  - `routeId` -路由到对应的id
  - `routePriority` -路由优先级:1:Lowest;2:Low;3:Normal;4:High;5:Highest

### Settings API
  Comm100 Live Chat公开了下面的API来进行站点的相关设置：
  - [Config API](#config-api)  
  - [Canned Messages API](#canned-messages-api)
  - [Custom Away Status API](#custom-away-status-api)
  - [Ban List API](#ban-list-api)
  - [Visitor Segmentation API](#visitor-segmentation-api)

#### Config API
  Comm100 Live Chat公开了下面的API对站点进行相关配置：
  - `GET /api/v1/livechat/configs` -获取站点的配置
  - `POST /api/v1/livechat/configs` -创建站点的配置
  - `PUT /api/v1/livechat/configs/{config_id}` -更新站点的配置

#### Config Object
  Comm100中Livechat的Config对象中包含以下属性：
  - `siteId` -站点编号
  - `ifDisplayTimeInfTranscript` -是否在聊天历史里面展示时间
  - `ifShowTypingContent` -是否显示正在输入的内容
  - `visitorHeartBeatDelayTime` -访客HeartBeat的持续时间
  - `ifAutoAcceptChat` -是否自动接受聊天
  - `ifSetMaxChatsCountForEachOperator` -是否为每个Operator设置最大聊天数
  - `maxChatsCountForAllOperator` -IfSetMaxChatsCountForEachOperator 为true，每个Operator默认取的最大聊天数
  - `ifPreferOperatorLastChattedWith` -随机路由时，是否允许分配给最近和你聊天的Operator
  - `ifDepartmentEnable` -是否允许使用DepartmentEnable
  - `ifCreateTicketWhenChatAccepted` -是否在接受聊天的时候创建Ticket
  - `ifCreateTicketWhenOfflineMessageSubmitted` -是否在提交留言的时候创建Ticket
  - `ifMultipleCodePlan` -是否开启多个Code Plan
  - `ifEnableSalesforce` -是否开启Sales force
  - `ifEnableCustomVariable` -是否开启自定义变量
  - `aPICallDailyLimit` -每天可以使用API的次数
  - `ifEnableZendesk` -是否开启Zendesk
  - `ifEnableGoogleAnalytics` -是否开启Google分析
  - `allocationbywhat` -用于判断Chat Auto-Allocation页面中Auto-allocate chat requests to operators based on下方列表如何显示：0 – department未开启，显示三个分配方式； 1 – department已开启，根据department显示一个列表
  - `allocationstrategy` -department未开启时，记录分配方式：0 - Load Balancing；1 - Round-Robin；2 - Capability Weighted
  - `ifEnableAutoAllocation` -是否开启Chat Auto-Allocation
  - `ifEnableChatTranslation` -是否开启Auto Translation
  - `ifEnableGoToMeeting` -是否开启GoToMeeting
  - `ifCustomAwayEnable` -是否开启Custom Away Status
  - `ifMaskCreditCardNum` -是否开启隐藏信用卡号
  - `ifEnableCustomerSegmentation` -是否开启访客分类
  - `operatorChatFileSizeLimit` -客服发送附件的大小限制(Mb)
  - `operatorChatFileCountDailyLimit` -客服每天发送附件的数量限制
  - `ifCanSelectHourlyMinute` -报表查询是否允许使用十分查询
  - `visitorMsgRestrict` -访客端发送文件限制的配置值
  - `ifRequireSessionWhenDownloadAttachment` -访客端下载附件时是否需要登录
  - `ifEnableJoinMeIntegration` -是否开启joinme
  - `defaultCodePlanId` -Dynamic功能的default codeplan
  - `ifEnableAdvancedCategoryMode` -是否开启高级模式的wrapup
  - `ifNotAllocateWhenVideoAudio` -是否不分配聊天给正在Audio/Video Chat中的Agent

#### Canned Messages API
  Comm100 Live Chat公开了下面的API来对[Canned Messaged Object](#canned-message-object)进行访问:
  - `GET /api/v1/livechat/cannedMessages` -获取站点下面的所有Canned Messages   
  - `GET /api/v1/livechat/cannedMessages/{cannedMessage_id}` -获取站点下面的一个特定的Canned Messages   
  - `POST /api/v1/livechat/cannedMessages` -新建一个Canned Messages   
  - `PUT /api/v1/livechat/cannedMessages/{cannedMessage_id}` -更新一个Canned Messages   
  - `DELETE /api/v1/livechat/cannedMessages/{cannedMessage_id}` -删除一个Canned Messages  
  
  - `GET /api/v1/livechat/categories` -获取站点下面的所有Canned Messages的category
  - `GET /api/v1/livechat/categories/{category_id}` -获取站点下面的一个特定的category  
  - `POST /api/v1/livechat/categories` -新建一个category   
  - `PUT /api/v1/livechat/categories/{category_id}` -更新一个category   
  - `DELETE /api/v1/livechat/categories/{category_id}` -删除一个category  
  
##### Canned Message Object
  Canned  Message对象包含以下属性：
  - `id` -主键id
  - `siteId` -所属站点
  - `title`  -标题
  - `categoryId` -所属类型的主键Id
  - `ifPrivate` -是否为私有
  - `operatorId` -Agent Id
  - `shortcuts` -快捷键

#### Custom Away Status API
  Comm100 Live Chat公开了下面的API来对自定义Away的状态进行访问：
  - `GET /api/v1/livechat/customAwayStatuses` -获取站点所有的自定义Away状态
  - `POST /api/v1/livechat/customAwayStatuses` -创建自定义Away状态
  - `PUT /api/v1/livechat/customAwayStatuses/{status_id}` -更新自定义Away状态

#### Visitor Segmentation API
  Comm100 Live Chat公开了下面的API来对用户细分进行访问：
  - `GET /api/v1/livechat/customerSegments` -获取站点所有自定义用户细分信息
  - `GET /api/v1/livechat/customerSegments/{segment_id}` -查询一个用户细分
  - `POST /api/v1/livechat/customerSegments` -新建一个用户细分
  - `PUT /api/v1/livechat/customerSegments/{segment_id}` -更新用户细分
  - `DELETE /api/v1/livechat/customerSegments/{segment_id}` -删除用户细分

#### Customer Segment Object
  用户细分对象中包含了下面的属性：
  - `id` -主键Id
  - `siteId` -SiteId
  - `name` -客户细分的名字
  - `description` -描述
  - `color` -客户细分的颜色配置
  - `ifEnable` -是否启用
  - `priority` -客户细分的优先级
  - `alertToType` -发送通知对象的类型：Department；Operator
  - `alertToIds` -发送通知的对象的Id列表：与Type相关，如果类型为Department则为DepartmentId，如果为Operator，则为OperatorId
  - `ifDeleted` -是否已经被删除
  - `enumConditionExpression` -Customer Segment的各个Condition之间的条件关系
  - `conditionExpression` -若EnumConditionExpression的值为2，各个条件之间的关系表达式

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
  + tabs
      * info  
          Partner的Agent可以在聊天页面查看当前聊天的信息
      * canned   
          Partner的Agent可以在聊天页面使用canned messages
      * wrap-up
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

 

