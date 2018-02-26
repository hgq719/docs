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
  - `chatButtonType` -ChatButton的类型：0：ImageButton;1：LinkText;2：MonitorOnly;3: Adaptive
  - `chatButtonIfFloat` -Chatbutton是否浮动
  - `chatButtonPosition` -Chatbutton的位置
  - `chatButtonXOffset` -若XOffsetIfPixel=1则，该字段表示X坐标的偏移像素值;若XOffsetIfPixel=0则，该字段表示X坐标的偏移比例;
  - `chatButtonXOffsetIfPixels` -ChatButtonXOffsetIfPixels	X坐标的偏移量是否为像素
  - `chatButtonYOffset` -若YOffsetIfPixel =1则，该字段表示y坐标的偏移像素值;若YOffsetIfPixel =0则，该字段表示y坐标的偏移比例;
  - `chatButtonYOffsetIfPixels` -Y坐标的偏移量是否为像素
  - `chatButtonImageType` -ChatButtonImage的类型:0：Online;1：Offline;2：Invitation;3：InvitationAccept;4：InvitationRefuse;5：Brannding;6：Poweredby;7：WindowColorStyle
  - `chatButtonOnlineURL` -当Operator处于 online时chatbutton的链接
  - `chatButtonOnlineImageId` - 当Operator处于 online时chatbutton的图片
  - `chatButtonOfflineURL` -当Operator处于 offline时chatbutton的链接
  - `chatButtonYOfflineImageId` -当Operator处于 offline时chatbutton的图片
  - `chatButtonIfHideOffline` -Chatbutton在offline时是否隐藏
  - `chatButtonRouteToType` -Route类型：0：site;1: Department;2:RouteToOperator;
  - `chatButtonRouteToId` -如果route类型是2，则为OperatorId;如果route类型是1则为departmentId

#### ChatWindow Property
- `chatWindowStyle`  -Chat window的类型：0 – Classic;1 – Circle;2 – Bubble
- `chatWindowHeaderType`  -0 – Banner Image;1 – Operator Avatar & Company Logo;2:Agent Info
- `chatWindowHeaderIfShowTitle`  -ChatWindowHeaderType为2时，该值有效:Chat Window Header是否显示Agent Title：0 – 不显示；1 – 显示
- `chatWindowHeaderIfShowBio`  -ChatWindowHeaderType为2时，该值有效:Chat Window Header是否显示Agent Bio:0 – 不显示;1 – 显示
- `chatWindowIfShowAvatar`  -ChatWindowHeaderType为1时，该值有效:0 – 不展示Avatar;1 – 展示Avatar
- `chatWindowIfShowLogo`  -ChatWindowHeaderType为1时，该值有效:0 – 不展示Logo;1 – 展示Logo
- `chatWindowLogoImageId`  -Logo的ImageId
- `chatContentIfShowAvatar`  -Chat Window聊天内容区域是否显示Agent Avatar:0 – 不显示;1 – 显示
- `chatContentIfShowTexture`  -Chat Window聊天内容区域是否有背景:0 – 不显示;1 – 显示
- `chatContentTextureType`  -Chat Window聊天内容区域的背景类型
- `chatButtonColor`  -Adaptive Button的颜色
- `chatWindowCustomCSSClassic`  -Classic的自定义CSS样式
- `chatWindowCustomCSSCircle`  -Circle的自定义CSS样式
- `chatWindowIfPrintTranscript`  -Chatwindow是否展示打印聊天记录
- `chatWindowIfShowEmailButton`  -Chatwindow是否展示EmailButton
- `chatWindowIfCanSwitchToOffline`  -Chatwindow能否转成offline
- `chatWindowIfCanSendFile`  -Chatwindow能否传送文件
- `ifEnableAudioChat`  -Chat window是否开启Allow visitors to request audio chats
- `ifEnableVideoChat`  -Chat window是否开启Allow visitors to request video chats
- `chatWindowIfEndChatWhenVisitorInactivity`  -Visitor处于Inactivity后是否结束chat
- `chatWindowIfEnableSendTranscriptEmail`  -是否开启发送transcript
- `chatWindowGreetingMessage` -Greeting Message内容
- `ifEnableCustomJS`  -是否开启自定义js
- `customJS`  -用户自定义的JavaScript

#### PreChat Property
- `preChatIfEnabled`  -是否允许Prechat
- `preChatHeaderIfShowTeamName`  -Pre-Chat是否显示Team Name：0 – 不显示；1 – 显示
- `preChatTeamName` - Pre-Chat中team Name,PreChatHeaderIfShowTeamName为1时有效。
- `preChatHeaderIfShowAgentAvatars`  -Pre-Chat是否显示Agent Avatars：0 – 不显示；1 – 显示
- `preChatGreetingMessage` -Greeting Message内容
- `prechatsocialmedia`	-是否选中socialMedia：0 – none;1 – google;2 – facebook;3 – both;
- `preChatIfNotRecordCookie`	-Prechat是否记录cookie
- `preChatWindowFormStyle`	-ChatWindow表单样式
- `preChatFields`  -Prechat页面自定义字段集合
  + [customField](#custom-field)  -自定义字段

##### Custom Filed
- `id` -字段的主键
- `formType` -0-Pre-Chat Form;1-Offline Message Form;2-Post Chat Form;3-Wrap-up Form;4-PCI Form (在聊天结束后不存储，看不到该表单数据);5-Custom Variable
- `fieldId` -自定义字段Id
- `name` -自定义字段Name或者自定义变量的Name
- `value` -自定义字段的值或者自定义变量的值
- `url` -自定义变量的url

#### PostChat Property
- `postChatIfEnabled`  -是否允许Postchat
- `postChatGreetingMessage` -Greeting Message内容
- `postChatWindowFormStyle`	-ChatWindow表单样式
- `postChatFields`  -自定义字段集合
  + [customField](#custom-field)  -自定义字段

#### Offline Message Property
- `offlineMessageIfUse`  -是否使用Comm100的OfflineMessage。0：不使用；1：使用
- `offlineMessageHeaderIfShowTeamName`  -OfflineMessageIfEnable为1时有效：Offline Message是否显示Team Name：0 – 不显示；1 – 显示
- `offlineMessageTeamName` - Offline Message中team Name,OfflineMessageIfEnable为1时且PreChatHeaderIfShowTeamName为1时有效。
- `offlineMessageHeaderIfShowAgentAvatars`  -OfflineMessageIfEnable为1时有效：Offline Message是否显示Agent Avatars：0 – 不显示；1 – 显示
- `offlineMessageGreetingMessage` -OfflineMessageIfEnable为1时有效：Greeting Message内容
- `offlineMessageWindowFormStyle`	-OfflineMessageIfEnable为1时有效：ChatWindow表单样式
- `offlineMessageFields`  -OfflineMessageIfEnable为1时有效：自定义字段集合
  + [customFields](#custom-fields)  -自定义字段
- `offlineMessageIfOpenInNewWindow`  -OfflineMessageIfEnable为0时有效：OfflineMessage是否在新窗口打开
- `offlineMessageUrl`  -OfflineMessageIfEnable为0时有效：OfflineMessageURL

#### Invitation Property
- `invitationStyle` -邀请的样式：1：Bubble；2：Popup invitation image；3：Greeting message in chat window
- `autoInvitationRules` -自动邀请规则集合
  + [autoInvitation Rules](autoinvitation-rules) -自动邀请规则
- `manualInvitation` -手动邀请
  + [invitationButton property](#invitationbutton-property) -邀请按钮

##### InvitationButton Property
  - `invitationPosition` -邀请框的位置：0:Center with Overlay;1:Center;2:Top Left ;3:Top Middle; 4:Top Right;5:Bottom Left;6:Bottom Middle;7:Bottom Right
  - `invitationXOffset` -若XOffsetIfPixel=1则，该字段表示X坐标的偏移像素值;若XOffsetIfPixel=0则，该字段表示X坐标的偏移比例;
  - `invitationXOffsetIfPixels` -X坐标的偏移量是否为像素
  - `invitationYOffset` -若YOffsetIfPixel =1则，该字段表示y坐标的偏移像素值;若YOffsetIfPixel =0则，该字段表示y坐标的偏移比例;
  - `invitationYOffsetIfPixels` -Y坐标的偏移量是否为像素
  - `invitationPositionStyle` -Y坐标的偏移量是否为像素
  - `invitationImageStyle` -图片类型：0：URL；1：from gallery  ；2：from my computer
  - `invitationImageId` -图片ID
  - `invitationNoImageURL` -No图片的URL
  - `invitationNoImageId` -No图片ID
  - `invitationYesImageURL` -Yes图片的URL
  - `invitationYesImageId` -Yes图片ID
  - `invitationCloseAreaXOffset` -Close图标的x坐标
  - `invitationCloseAreaYOffset` -Close图标的y坐标
  - `invitationCloseAreaWidth`  -Close图标的宽度
  - `invitationCloseAreaHeight`  -Close图标的高度
  - `invitationTextAreaXOffset`  -Invitaion文本内容的x坐标
  - `invitationTextAreaYOffset`  -Invitaion文本内容的y坐标
  - `invitationTextAreaWidth`  -Invitaion文本内容的宽度
  - `invitationTextAreaHeight`  -Invitaion文本内容的高度
  - `invitationText`  -Invitaion文本内容
  - `invitationTextFont`  -Invitaion文本内容字体
  - `invitationTextSize`  -Invitaion文本字体大小
  - `invitationTextIfBold`  -Invitaion文本内容是否加粗
  - `invitationTextIfItalic`  -Invitaion文本内容是否斜体
  - `invitationTextColor`  -Invitaion文本颜色

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
