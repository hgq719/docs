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
  - [InvitationButton property](#invitationButton-property)
  - [ChatWindow property](#chatwindow-property)
  - [PreChat property](#prechat-property)
  - [PostChat property](#post-property)
  - [OfflineMessage property](#offline-message-property)
  - [Invitation property](#invitation-property)
  - [AgentWrapup property](#agentwrapup-property)
  - [RoutingRule property](#routingrule-property)
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

#### InvitationButton Property
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
- [PreChatFields](#custom-fields)  -Prechat页面自定义字段

##### Custom Fileds
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
- [PostChatFields](#custom-fields)  -自定义字段

#### Offline Message Property
- `OfflineMessageIfUse`  -是否使用Comm100的OfflineMessage。0：不使用；1：使用
- `OfflineMessageHeaderIfShowTeamName`  -OfflineMessageIfEnable为1时有效：Offline Message是否显示Team Name：0 – 不显示；1 – 显示
- `OfflineMessageTeamName` - Offline Message中team Name,OfflineMessageIfEnable为1时且PreChatHeaderIfShowTeamName为1时有效。
- `OfflineMessageHeaderIfShowAgentAvatars`  -OfflineMessageIfEnable为1时有效：Offline Message是否显示Agent Avatars：0 – 不显示；1 – 显示
- `OfflineMessageGreetingMessage` -OfflineMessageIfEnable为1时有效：Greeting Message内容
- `OfflineMessageWindowFormStyle`	-OfflineMessageIfEnable为1时有效：ChatWindow表单样式
- [OfflineMessageFields](#custom-fields)  -OfflineMessageIfEnable为1时有效：自定义字段
- `OfflineMessageIfOpenInNewWindow`  -OfflineMessageIfEnable为0时有效：OfflineMessage是否在新窗口打开
- `OfflineMessageUrl`  -OfflineMessageIfEnable为0时有效：OfflineMessageURL

#### Invitation Property

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