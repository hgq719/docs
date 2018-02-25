# General

## Campaigns Object
  Comm100 Live Chat中公开了下面的API来对Campaign资源进行操作：  
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


### Campaign Properties
  - [ChatButton property](#chatButton-property)
  - [ChatWindow property](#chatwindow-property)
  - [PreChat property](#prechat-property)
  - [PostChat property](#post-property)
  - [OfflineMessage property](#offline-message-property)
  - [Invitation property](#invitation-property)
  - [AgentWrapup property](#agent-wrapup-property)
  - [RoutingRule property](#routing-rule-property)
  - [Language property](#language-property)

#### ChatButton Property
  - `ChatButtonType` -ChatButton的类型：0：ImageButton;1：LinkText;2：MonitorOnly;3: Adaptive
  - `ChatButtonIfFloat` -Chatbutton是否浮动
  - `ChatButtonPosition` -Chatbutton的位置
  - `ChatButtonXOffset` -若XOffsetIfPixel=1则，该字段表示X坐标的偏移像素值;若XOffsetIfPixel=0则，该字段表示X坐标的偏移比例;
  - `ChatButtonXOffsetIfPixels` -ChatButtonXOffsetIfPixels	X坐标的偏移量是否为像素
  - `ChatButtonYOffset` -若YOffsetIfPixel =1则，该字段表示y坐标的偏移像素值;若YOffsetIfPixel =0则，该字段表示y坐标的偏移比例;
  - `ChatButtonYOffsetIfPixels` -Y坐标的偏移量是否为像素
  - `ChatButtonImageType` -ChatButtonImage的类型:0：Online;1：Offline;2：Invitation;3：InvitationAccept;4：InvitationRefuse;5：Brannding;6：Poweredby;7：WindowColorStyle
  - `ChatButtonOnlineURL` -当Operator处于 online时chatbutton的链接
  - `ChatButtonOnlineImageId` - 当Operator处于 online时chatbutton的图片
  - `ChatButtonOfflineURL` -当Operator处于 offline时chatbutton的链接
  - `ChatButtonYOfflineImageId` -当Operator处于 offline时chatbutton的图片
  - `ChatButtonIfHideOffline` -Chatbutton在offline时是否隐藏
  - `ChatButtonRouteToType` -Route类型：0：site;1: Department;2:RouteToOperator;
  - `ChatButtonRouteToId` -如果route类型是2，则为OperatorId;如果route类型是1则为departmentId

#### ChatWindow Property
- `ChatWindowStyle`  -Chat window的类型：0 – Classic;1 – Circle;2 – Bubble
- `ChatWindowHeaderType`  -0 – Banner Image;1 – Operator Avatar & Company Logo;2:Agent Info
- `ChatWindowHeaderIfShowTitle`  -ChatWindowHeaderType为2时，该值有效:Chat Window Header是否显示Agent Title：0 – 不显示；1 – 显示
- `ChatWindowHeaderIfShowBio`  -ChatWindowHeaderType为2时，该值有效:Chat Window Header是否显示Agent Bio:0 – 不显示;1 – 显示
- `ChatWindowIfShowAvatar`  -ChatWindowHeaderType为1时，该值有效:0 – 不展示Avatar;1 – 展示Avatar
- `ChatWindowIfShowLogo`  -ChatWindowHeaderType为1时，该值有效:0 – 不展示Logo;1 – 展示Logo
- `ChatWindowLogoImageId`  -Logo的ImageId
- `ChatContentIfShowAvatar`  -Chat Window聊天内容区域是否显示Agent Avatar:0 – 不显示;1 – 显示
- `ChatContentIfShowTexture`  -Chat Window聊天内容区域是否有背景:0 – 不显示;1 – 显示
- `ChatContentTextureType`  -Chat Window聊天内容区域的背景类型
- `ChatButtonColor`  -Adaptive Button的颜色
- `ChatWindowCustomCSSClassic`  -Classic的自定义CSS样式
- `ChatWindowCustomCSSCircle`  -Circle的自定义CSS样式
- `ChatWindowIfPrintTranscript`  -Chatwindow是否展示打印聊天记录
- `ChatWindowIfShowEmailButton`  -Chatwindow是否展示EmailButton
- `ChatWindowIfCanSwitchToOffline`  -Chatwindow能否转成offline
- `ChatWindowIfCanSendFile`  -Chatwindow能否传送文件
- `IfEnableAudioChat`  -Chat window是否开启Allow visitors to request audio chats
- `IfEnableVideoChat`  -Chat window是否开启Allow visitors to request video chats
- `ChatWindowIfEndChatWhenVisitorInactivity`  -Visitor处于Inactivity后是否结束chat
- `ChatWindowIfEnableSendTranscriptEmail`  -是否开启发送transcript
- `ChatWindowGreetingMessage` -Greeting Message内容
- `IfEnableCustomJS`  -是否开启自定义js
- `CustomJS`  -用户自定义的JavaScript

#### PreChat Property
- `PreChatIfEnabled`  -是否允许Prechat
- `PreChatHeaderIfShowTeamName`  -Pre-Chat是否显示Team Name：0 – 不显示；1 – 显示
- `PreChatTeamName` - Pre-Chat中team Name,PreChatHeaderIfShowTeamName为1时有效。
- `PreChatHeaderIfShowAgentAvatars`  -Pre-Chat是否显示Agent Avatars：0 – 不显示；1 – 显示
- `prechatsocialmedia`	-是否选中socialMedia：0 – none;1 – google;2 – facebook;3 – both;
- `PreChatIfNotRecordCookie`	-Prechat是否记录cookie
- `PreChatWindowFormStyle`	-ChatWindow表单样式
- `PreChatFields`  -Prechat页面自定义字段集合
  + [CustomField](#custom-field)  -自定义字段

##### Custom Filed
- `Id` -字段的主键
- `TranscriptType` -0-Chat;1-Offline Message
- `TranscriptId` -Transcritp的主键
- `FormType` -0-Pre-Chat Form;1-Offline Message Form;2-Post Chat Form;3-Wrap-up Form;4-PCI Form (在聊天结束后不存储，看不到该表单数据);5-Custom Variable
- `FieldId` -自定义字段Id
- `Name` -自定义字段Name或者自定义变量的Name
- `Value` -自定义字段的值或者自定义变量的值
- `Url` -自定义变量的url

#### PostChat Property
- `PostChatIfEnabled`  -是否允许Postchat
- `PostChatGreetingMessage` -Greeting Message内容
- `PostChatWindowFormStyle`	-ChatWindow表单样式
- `PostChatFields`  -自定义字段集合
  + [CustomField](#custom-field)  -自定义字段

#### Offline Message Property
- `OfflineMessageIfUse`  -是否使用Comm100的OfflineMessage。0：不使用；1：使用
- `OfflineMessageHeaderIfShowTeamName`  -OfflineMessageIfEnable为1时有效：Offline Message是否显示Team Name：0 – 不显示；1 – 显示
- `OfflineMessageTeamName` - Offline Message中team Name,OfflineMessageIfEnable为1时且PreChatHeaderIfShowTeamName为1时有效。
- `OfflineMessageHeaderIfShowAgentAvatars`  -OfflineMessageIfEnable为1时有效：Offline Message是否显示Agent Avatars：0 – 不显示；1 – 显示
- `OfflineMessageGreetingMessage` -OfflineMessageIfEnable为1时有效：Greeting Message内容
- `OfflineMessageWindowFormStyle`	-OfflineMessageIfEnable为1时有效：ChatWindow表单样式
- `OfflineMessageFields`  -OfflineMessageIfEnable为1时有效：自定义字段集合
  + [CustomFields](#custom-fields)  -自定义字段
- `OfflineMessageIfOpenInNewWindow`  -OfflineMessageIfEnable为0时有效：OfflineMessage是否在新窗口打开
- `OfflineMessageUrl`  -OfflineMessageIfEnable为0时有效：OfflineMessageURL

#### Invitation Property
- `InvitationStyle` -邀请的样式：1：Bubble；2：Popup invitation image；3：Greeting message in chat window
- `AutoInvitationRules` -自动邀请规则集合
  + [AutoInvitation Rules](autoinvitation-rules) -自动邀请规则
- `ManualInvitation` -手动邀请
  + [InvitationButton property](#invitationbutton-property) -邀请按钮

##### InvitationButton Property
  - `InvitationPosition` -邀请框的位置：0:Center with Overlay;1:Center;2:Top Left ;3:Top Middle; 4:Top Right;5:Bottom Left;6:Bottom Middle;7:Bottom Right
  - `InvitationXOffset` -若XOffsetIfPixel=1则，该字段表示X坐标的偏移像素值;若XOffsetIfPixel=0则，该字段表示X坐标的偏移比例;
  - `InvitationXOffsetIfPixels` -X坐标的偏移量是否为像素
  - `InvitationYOffset` -若YOffsetIfPixel =1则，该字段表示y坐标的偏移像素值;若YOffsetIfPixel =0则，该字段表示y坐标的偏移比例;
  - `InvitationYOffsetIfPixels` -Y坐标的偏移量是否为像素
  - `InvitationPositionStyle` -Y坐标的偏移量是否为像素
  - `InvitationImageStyle` -图片类型：0：URL；1：from gallery  ；2：from my computer
  - `InvitationImageId` -图片ID
  - `InvitationNoImageURL` -No图片的URL
  - `InvitationNoImageId` -No图片ID
  - `InvitationYesImageURL` -Yes图片的URL
  - `InvitationYesImageId` -Yes图片ID
  - `InvitationCloseAreaXOffset` -Close图标的x坐标
  - `InvitationCloseAreaYOffset` -Close图标的y坐标
  - `InvitationCloseAreaWidth`  -Close图标的宽度
  - `InvitationCloseAreaHeight`  -Close图标的高度
  - `InvitationTextAreaXOffset`  -Invitaion文本内容的x坐标
  - `InvitationTextAreaYOffset`  -Invitaion文本内容的y坐标
  - `InvitationTextAreaWidth`  -Invitaion文本内容的宽度
  - `InvitationTextAreaHeight`  -Invitaion文本内容的高度
  - `InvitationText`  -Invitaion文本内容
  - `InvitationTextFont`  -Invitaion文本内容字体
  - `InvitationTextSize`  -Invitaion文本字体大小
  - `InvitationTextIfBold`  -Invitaion文本内容是否加粗
  - `InvitationTextIfItalic`  -Invitaion文本内容是否斜体
  - `InvitationTextColor`  -Invitaion文本颜色

##### AutoInvitation Rule 
  - `Id` -规则主键
  - `IfEnable` -是否启用
  - `Order` -排序
  - [InvitationButton property](#invitationbutton-property) -邀请按钮
  - `InvitationConditions` -邀请条件集合
     + [Condition Object](#condition-object)  -条件对象

##### Condition Object
  - `Id` -条件主键
  - `EnumRuleType` -0: DynamicCodePlan；1: RoutingRule；2:AutoInvitation；3:VisitorSegment
  - `RuleId` -对应rule的id
  - `DisplayId` -界面展示的rule序号
  - `Variable` -条件的名称
  - `Expression` -表达式枚举：0：is；1：contains；2：not contains；3：is more than；4：is less than；5：is not；6：not less than；7：not more than；8：regular expression
  - `Value` -条件的值

#### Agent Wrapup Property
  - `WrapupFields`  -Wrapup页面自定义字段集合
    + [CustomField](#custom-field)  -自定义字段

#### Language Property
  - `language` -语言
  - `IfCustomizeLanguage` -是否使用自定义语言。0：不使用，使用默认语言 ；1：使用自定义语言
  - `IfRTL` -是否从右到左对齐，IfCustomizeLanguage为1时有效。
  - `ButtonLanguages` -按钮对应的语言集合，IfCustomizeLanguage为1时有效。
    + `ButtonLanguage` -按钮对应的语言。
      * `ButtonName` -按钮的名字
      * `DefaultText` -按钮显示的文字
      * `CurrentText` -按钮当前的文字
  - `FieldLanguages` -字段对应的语言集合，IfCustomizeLanguage为1时有效。
    + `FieldLanguage` -字段对应的语言。
      * `FieldName` -字段的名字
      * `DefaultText` -字段显示的文字
      * `CurrentText` -字段当前的文字
  - `PromptsLanguages` -提示对应的语言集合，IfCustomizeLanguage为1时有效。
    + `PromptsLanguage` -提示对应的语言。
      * `Prompt` -提示的名字
      * `DefaultText` -提示显示的文字
      * `Macro` -使用的宏
      * `CurrentText` -提示当前的文字
  - `SystemMessageLanguages` -系统信息对应的语言集合，IfCustomizeLanguage为1时有效。
    + `SystemMessageLanguage` -系统信息对应的语言。
      * `Event` -事件的名字
      * `DefaultText` -系统信息显示的文字
      * `Macro` -使用的宏
      * `CurrentText` -系统信息当前的文字
  - `AudioChatLanguages` -语言聊天对应的语言集合，IfCustomizeLanguage为1时有效。
    + `AudioChatLanguage` -语言聊天对应的语言。
      * `AudioChat` -语言聊天的名字
      * `DefaultText` -语言聊天显示的文字
      * `Macro` -使用的宏
      * `CurrentText` -语言聊天当前的文字
  - `VideoChatLanguages` -视频聊天对应的语言集合，IfCustomizeLanguage为1时有效。
    + `VideoChatLanguage` -视频聊天对应的语言。
      * `VideoChat` -视频聊天的名字
      * `DefaultText` -视频聊天显示的文字
      * `Macro` -使用的宏
      * `CurrentText` -视频聊天当前的文字
  - `ScreenSharingLanguages` -屏幕分享时对应的语言集合，IfCustomizeLanguage为1时有效。
    + `ScreenSharingLanguage` -屏幕分享时对应的语言。
      * `ScreenSharing` -屏幕分享时的名字
      * `DefaultText` -屏幕分享时显示的文字
      * `Macro` -使用的宏
      * `CurrentText` -屏幕分享时当前的文字
  - `TranscriptEmailtoVisitorsLanguages` -发送脚本邮件中对应的语言集合，IfCustomizeLanguage为1时有效。
    + `TranscriptEmailtoVisitorsLanguage` -发送脚本邮件中对应的语言。
      * `TranscriptEmail` -发送脚本邮件中的名字
      * `DefaultText` -发送脚本邮件中显示的文字
      * `Macro` -使用的宏
      * `CurrentText` -发送脚本邮件中当前的文字
  - `TextonMobileBrowsersLanguages` -移动设备浏览器上中对应的语言集合，IfCustomizeLanguage为1时有效。
    + `TextonMobileBrowsersLanguage` -移动设备浏览器上对应的语言。
      * `WindowTitleOrOthers` -窗体标题或其他位置的名字
      * `DefaultText` -默认显示的文字
      * `CurrentText` -当前的文字
  - `EmbeddedWindowLanguages` -嵌入窗体中对应的语言集合，IfCustomizeLanguage为1时有效。
    + `EmbeddedWindowLanguage` -嵌入窗体中对应的语言。
      * `EmbeddedWindow` -嵌入窗体的名字
      * `DefaultText` -默认显示的文字
      * `Macro` -使用的宏
      * `CurrentText` -当前的文字
  - `ChatBotLanguages` -使用ChatBot时对应的语言集合，IfCustomizeLanguage为1时有效。
    + `ChatBotLanguage` -使用ChatBot时对应的语言。
      * `ChatBot` -使用ChatBot时对应时机的名字
      * `DefaultText` -默认显示的文字
      * `Macro` -使用的宏
      * `CurrentText` -当前的文字

#### Routing Rules Property
  - `IfEnableRoute` -是否启用路由规则
  - `Routemethod` -0 - Route visitors to a specific department or operator；1 - Route visitors based on custom rules
  - [RouteSpecificPoint](#route-specific-point) -路由到指定节点，Routemethod为0时有效
  - `RouteRules` -路由规则集合，Routemethod为1时有效
    + [RouteRule](#route-rule-object) -路由规则对象
  - `FailRouteType` -0 – 未配置；1 – fail route to department；2 – fail route to operator；3 – redirect to offline message，Routemethod为1时有效
  - `FailRouteId` - 失败时路由到的对应ID，Routemethod为1时有效
  - `FailRouteMessageTo` -FailRouteType选择redirect to offline message时，填写的收邮件的Email，Routemethod为1时有效

##### Route Rule Object
  - `RouteName` -当前路由的名称
  - `IfEnable` -是否启用当前这条路由规则
  - `Order` -路由规则顺序
  - `RouteConditions` -路由条件集合
     + [Condition Object](#condition-object)  -条件对象
  - [RouteSpecificPoint](#route-specific-point) -路由到指定节点  

##### Route Specific Point
  - `RouteType` -路由类型：0:Department;1:Agent
  - `RouteId` -路由到对应的id
  - `RoutePriority` -路由优先级:1:Lowest;2:Low;3:Normal;4:High;5:Highest

## Config Object 
`GET /api/v1/livechat/campaign/configs` -Get campaign config  
`GET /api/v1/livechat/chatButton/configs` -Get chatButton config  
`GET /api/v1/livechat/chatWindow/configs` -Get chatWindow config  
`GET /api/v1/livechat/preChat/configs` -Get prechat config  
`GET /api/v1/livechat/postChat/configs` -Get postchat config  
`GET /api/v1/livechat/offlineMessage/configs` -Get offlineMessage config  
`GET /api/v1/livechat/invitation/configs` -Get invitation config  
`GET /api/v1/livechat/agentWrapup/configs` -Get agentWrapup config  
`GET /api/v1/livechat/routingRule/configs` -Get routingRule config  
`GET /api/v1/livechat/language/configs` -Get language config  