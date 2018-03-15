# General
 1. [Authentication](#authentication)  
 2. [Authority Manage API](#authority-managment-api)  
 3. [Campaign API](#campaign-api)
 4. [Settings API](#settings-api)

## Authentication
  开发者可以通过下面的步骤来调用相应的API:
  - [Request Access Token](#request-access-token)
  - [Call API](#call-api)

### Request Access Token
  开发者需要通过下面的API来向Comm100请求访问API的token。

  `GET https://hosted.comm100.com/oauth/token`

  Request Parameters:
  - `response_type` -授权类型，默认值`token`，必须指定。
  - `redirect_url` -指定用户授权以后的重定向页面，该url必须是一个绝对地址。必须指定。
  - `client_id` -客户端id，如partnerId，必须指定。
  - `client_secret` - 客户端身份密钥，用于换取`Access_token`来访问Comm100的Api
  - `scope` -指定Comm100资源的访问权限列表，包括`read`、`write`，还可以指定访问特定的资源或所有资源，具体参考[Request Scope Setting](#request-scope-setting)，必须指定。
  - `state` -客户端的当前状态，任意值，认证服务器会原封不动的返回。

  Response示例：
  ```json
    Status: 200 OK

    {
      "access_token":"98asjdfka172dsfsd9s2342sdfs",
      "expires_in": "3600",
      "token_type": "bearer",
      "scope": "read"
    }
  ```

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

### Call API
  开发者可以通过上面获取的`access_token`来进行API调用，格式如下：  

  `Authorization": "bearer {access_token}"`

## Authority Managment API
  Partner可以在自己的用户管理界面中通过调用Comm100 RESTful API来配置自己系统中的账户在Comm100中权限，Comm100 Live Chat公开了下面的API来对站点下的权限资源进行操作：
  - Permission Managment  
    + `GET /api/v1/livechat/permissions` -获取所有的[Permission Object](#permission-object)的信息   
    + `GET /api/v1/livechat/permissions/{permission_id}` -获取指定的[Permission Object](#permission-object)的信息   
  - Permission Configuration
    + `GET /api/v1/livechat/agents/{agent_id}/permissions` -获取当前agent的所有[Permission](agent-permission-object)信息   
    + `POST /api/v1/livechat/agents/{agent_id}/permissions` -给当前agent新增一个[Permission](agent-permission-object)
    + `PUT /api/v1/livechat/agents/{agent_id}/permissions/{permission_info}` -更新agent的某一个[Permission](agent-permission-object)配置   
    + `DELETE /api/v1/livechat/agents/{agent_id}/permissions/{permission_id}` -删除当前agent的某一个[Permission](agent-permission-object)配置   

### Permission Object
  Permission对象包含以下属性：
  - `id` -主键id
  - `name` -权限名字
  - `module` -所属模块
  - `subject` -权限主题
  - `description` -权限描述

### Agent Permission Object
  Agent的权限对象包含以下属性:
  - `id` -主键id
  - `agentId` -agent的id
  - `siteId` -站点id
  - `permission` -权限对象列表
    + [Permission Object](#permission-object) -权限对象

## Campaign API
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

## Settings API
  Comm100 Live Chat公开了下面的API来进行站点的相关设置：
  - [Config API](#config-api)  
  - [Canned Messages API](#canned-messages-api)
  - [Custom Away Status API](#custom-away-status-api)
  - [Ban List API](#ban-list-api)
  - [Visitor Segmentation API](#visitor-segmentation-api)

### Config API
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

### Canned Messages API
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

### Custom Away Status API
  Comm100 Live Chat公开了下面的API来对自定义Away的状态进行访问：
  - `GET /api/v1/livechat/customAwayStatuses` -获取站点所有的自定义Away状态
  - `POST /api/v1/livechat/customAwayStatuses` -创建自定义Away状态
  - `PUT /api/v1/livechat/customAwayStatuses/{status_id}` -更新自定义Away状态

### Visitor Segmentation API
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
