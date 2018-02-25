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
  - [OfflineMessage property](#offlinemessage-property)
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