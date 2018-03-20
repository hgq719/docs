# General
 1. [Authentication](#authentication)  
 2. [Acount API](#account-api)  
 3. [LiveChat API](#livechat-api)

## Authentication
  Comm100对于Restful的Api采取标准的OAuth2.0的方式对调用者进行身份验证，具体方式参考[Auth Authorization](https://github.com/hgq719/docs/blob/master/open-platform.md#oauth-authorization)。   

## Account API
  开发者可以通过Account API来获取和设置下面这些资源：
  - [Agent Object](#agent-object)
  - [Group Object](#group-object)
  - [Permission Object](#Permission-object)
  - [Agent Permission Object](#agent-permission-object)
  - [Group Permission Object](#group-permission-object)

### Agent Object
  Comm100中Agent对象包含下面这些信息：
  - `email` -电子邮箱
  - `firstName` -名
  - `lastName` -姓
  - `displayName` -显示名字
  - `phone` -电话号码
  - `title` -头衔
  - `bio` -个人介绍
  - `avatar` -头像
  - `isAdmin` -是否是管理员
  - `isActive` -是否可用
  - `api_key` -使用这个key来换取调用api的access_token

### Agent API 
  开发者可通过下面的API来操作Agent资源：
  + `GET /api/v1/account/agents` -获取agent列表   
  + `GET /api/v1/account/agents/{agent_id}` -获取特定的agent   
  + `POST /api/v1/account/agents` -新增一个agent
  + `PUT /api/v1/account/agents/{agent_id}` -更新agent   
  + `PUT /api/v1/account/agents/{agent_id}/reset_api_key` -重置api_key   
  + `DELETE /api/v1/account/agents/{agent_id}` -删除agent   

### Group Object
  Comm100中Group对象包含下面这些信息：
  - `name` -电子邮箱
  - `description` -组的描述
  - `agents` - 所包含的agent列表
    + [agent](#agent-object)

### Group API 
  开发者可通过下面的API来操作Group资源：
  + `GET /api/v1/account/groups` -获取group列表   
  + `GET /api/v1/account/groups/{group_id}` -获取特定的group   
  + `POST /api/v1/account/groups` -新增一个group
  + `PUT /api/v1/account/groups/{group_id}` -更新group   
  + `DELETE /api/v1/account/groups/{group_id}` -删除group   

### Permission Object
  Permission对象包含以下属性：
  - `name` -权限名字
  - `module` -所属模块
  - `subject` -权限主题
  - `description` -权限描述

### Permission API
  开发者可以通过下面的API来操作权限资源：
  + `GET /api/v1/account/permissions` -获取所有的权限信息   
  + `GET /api/v1/account/permissions/{permission_id}` -获取指定的权限的信息   
  + `POST /api/v1/account/permissions` -新增一个权限信息
  + `PUT /api/v1/account/permissions/{permission_id}` -更新一个权限信息   
  + `DELETE /api/v1/account/permissions/{permission_id}` -删除一个权限信息 

### List All Permissions
Gets the list of permissions.

#### Path
  `GET https://hosted.comm100.com/api/v1/account/permissions`

#### Parameters
None.  

#### Response
| Name | Description
| --- | ---
| `name ` | name of the permission.
| `module` | the module which the permission belong to
| `subject` | the subject of the permission
| `description` | the description of the permission

#### Example
Sample request:

  `curl -u tester@comm100.com:ef43f9362aac4f60ad428cb4d072f2c8 -X GET \`   
  `"https://hosted.comm100.com/api/v1/account/permissions"`

Sample response:

```json
    {
      "permissions": [
        {
          "name":"Accept Chats",
          "module":"LiveChat",
          "subject":"Chat",
          "descprition":[
            "Accept my department's chat requests",
            "Accept chat requests which do not belong to any departments"
          ]
        },
        {
          "name":"Manage Users",
          "module":"User&Contact",
          "subject":"users",
          "descprition":[
            "View user list and user details",
            "Create/edit/export/delete users",
            "Restore deleted users form the Recycle Bin",
            "Add/delete call logs, notes and attachments ",
            "View user list and user details",
            "Promote visitors to users"
          ]
        }
      ]
    }
```          

### Agent Permission Object
  Agent的权限对象包含以下属性:
  - `agentId` -agent的id
  - `permission` -权限对象列表
    + [Permission Object](#permission-object) -权限对象

### Agent Permission API
  开发者可以通过下面的API来操作agent的权限资源:
  + `GET /api/v1/account/agents/{agent_id}/permissions` -获取当前agent的所有权限信息   
  + `POST /api/v1/account/agents/{agent_id}/permissions` -给当前agent新增一个权限
  + `PUT /api/v1/account/agents/{agent_id}/permissions/{permission_info}` -更新agent的某一个权限配置   
  + `DELETE /api/v1/account/agents/{agent_id}/permissions/{permission_id}` -删除当前agent的某一个权限配置   

#### Add A Permission For The Agent
add a permission for the agent.

### Path
  `POST https://hosted.comm100.com/api/v1/account/agents/{agent_id}/permissions`

### Parameters
| Name | Description
| --- | ---
| `agentId` | required, the id of the agent
| `permissionId` | required, the id of the permission

### Response
Returns the details of the newly added agent permission.

| Name | Description
| --- | ---
| `id` | the id of the newly added agent permission.
| `agentId` | the id of the agent
| `permissionId` | the id of the permission

### Example
Sample request:

  `curl -u tester@comm100.com:ef43f9362aac4f60ad428cb4d072f2c8 -X POST \`  
  `-d permissionId=35`   
  `"https://hosted.comm100.com/api/v1/account/agents/123/permissions"`

Sample response:

```json
    {
      "id": 6,
      "agentId": "123",
      "permissionId": "35"
    }
```

### Group Permission Object
  Group的权限对象包含以下属性:
  - `groupId` -group的id
  - `permission` -权限对象列表
    + [Permission Object](#permission-object) -权限对象

### Group Permission API
  开发者可以通过下面的API来操作group的权限资源:
  + `GET /api/v1/account/groups/{group_id}/permissions` -获取当前group的所有权限信息   
  + `POST /api/v1/account/groups/{group_id}/permissions` -给当前group新增一个权限
  + `PUT /api/v1/account/groups/{group_id}/permissions/{permission_info}` -更新group的某一个权限配置   
  + `DELETE /api/v1/account/groups/{group_id}/permissions/{permission_id}` -删除当前group的某一个权限配置   

## LiveChat API
  Comm100 Live Chat中可以获取或设置下面的资源：
  - [Campaign Object](#campaign-object)
    + [ChatButton Object](#chatbutton-object)
    + [ChatWindow Object](#chatwindow-object)
    + [PreChat Object](#prechat-object)
    + [PostChat Object](#postchat-object)
    + [OfflineMessage Object](#offline-message-object)
    + [AutoInvitation Object](#autoInvitation-object)
    + [AgentWrapup Object](#agent-wrapup-object)
    + [RoutingRule Object](#routing-rule-object)
    + [Language Object](#language-object)
  - [Config Object](#config-object)
  - [Canned Messages Object](#canned-messages-object)
  - [Custom Away Status Object](#custom-away-status-object)
  - [Ban List Object](#ban-list-object)
  - [Visitor Segmentation Object](#visitor-segmentation-object)

### Campaign Object
  Campaign对象包含以下属性：  
  - `name` -Campaign的名字
  - `description` -描述
  - [chatButton](#chatButton-object)
  - [chatWindow](#chatwindow-object)
  - [preChat](#prechat-object)
  - [postChat](#post-object)
  - [offlineMessage](#offline-message-object)
  - [invitation](#invitation-object)
  - [agentWrapup](#agent-wrapup-object)
  - [routingRule](#routing-rule-object)
  - [language](#language-object)

#### Image Button Object
  - `imageUrl` -图片地址
  - `showButtonType` -按钮显示类型：static;float;
  - `buttonPosition` -Chatbutton的位置：centered;topLeft;topMiddle;topRight;buttomLeft;buttomMiddle;buttomRight;leftMiddle;rightMiddle;
  - `xOffset` -若XOffsetIfPixel=pixels则，该字段表示X坐标的偏移像素值;若XOffsetIfPixel=percent则，该字段表示X坐标的偏移比例;
  - `xOffsetIfPixels` -ChatButtonXOffsetIfPixels	X坐标的偏移量单位：pixels；percent
  - `yOffset` -若YOffsetIfPixel=pixels则，该字段表示y坐标的偏移像素值;若YOffsetIfPixel=percent则，该字段表示y坐标的偏移比例;
  - `yOffsetIfPixels` -Y坐标的偏移量单位：pixels；percent

#### ChatButton Object
  - `buttonType` -ChatButton的类型：Adaptive;ImageButton;TextLink;
  - `adaptive` -chatButton为Adaptive时的配置
    + `buttonColor` -按钮的主体颜色
    + `iconUrl` -图标的地址
  - `imageButton` -chatButton为ImageButton时的配置
    + [desktopView](#image-button-object) -桌面版按钮配置
    + `mobileView` -移动版按钮配置
      * `showType` -显示类型：text；image
      * `textOnline` -showType为text时，在线的时候显示文字
      * `textOffline` -showType为text时，离线的时候显示文字
      * `backgroundColor` -showType为text时，背景颜色
      * `imageUrl` -showType为image时，图片路径
      * `imagePosition` -showType为image时，图片位置:bottomLeft;bottomMiddle;bottomRight;leftMiddle;RightMiddle;leftBottom;rightBottom;
  - `textLink` -chatButton为TextLink时的配置
    + `textContent` -显示文本的内容
  - `isHideOffline` -Chatbutton在offline时是否隐藏
  - `sepcifiedDomainsOrUrls` -指定只在当前这些域名或者地址下显示聊天按钮，为一个字符串列表

#### ChatWindow Object
- `windowStyle`  -Chat window的类型：Classic;Circle;Bubble
- `mainColor`  -聊天窗口的主体颜色
- `header`
  + `headerType`  -bannerImage – Banner Image;operatorAvatar – Operator Avatar & Company Logo;agentInfo:Agent Info
  + `isShowTitle`  -headerType为agentInfo时，该值有效:Chat Window Header是否显示Agent Title：false – 不显示；true – 显示
  + `isShowBio`  -headerType为agentInfo时，该值有效:Chat Window Header是否显示Agent Bio:false – 不显示;true – 显示
  + `bannerImageUrl` -headerType为bannerImage时，该值有效,值为头部banner的图片地址
  + `isShowAvatar`  -headerType为agentInfo和operatorAvatar时，该值有效:false – 不展示Avatar;true – 展示Avatar
  + `isShowLogo`  -headerType为operatorAvatar时，该值有效:false – 不展示Logo;true – 展示Logo
  + `logoImageUrl`  -Logo的图片地址
- `body`
  + `isShowAvatar`  -Chat Window聊天内容区域是否显示Agent Avatar:false – 不显示;true – 显示
  + `isShowTexture`  -Chat Window聊天内容区域是否有背景:false – 不显示;true – 显示
  + `contentTextureType`  -Chat Window聊天内容区域的背景类型
- `customCSSClassic`  -Classic的自定义CSS样式
- `customCSSCircle`  -Circle的自定义CSS样式
- `isPrintTranscript`  -Chatwindow是否展示打印聊天记录
- `isShowEmailButton`  -Chatwindow是否展示EmailButton
- `isCanSwitchToOffline`  -Chatwindow能否转成offline
- `isCanSendFile`  -Chatwindow能否传送文件
- `isEnableAudioChat`  -Chat window是否开启Allow visitors to request audio chats
- `isEnableVideoChat`  -Chat window是否开启Allow visitors to request video chats
- `isEndChatWhenVisitorInactivity`  -Visitor处于Inactivity后是否结束chat
- `isEnableSendTranscriptEmail`  -是否开启发送transcript
- `greetingMessage` -Greeting Message内容
- `isEnableCustomJS`  -是否开启自定义js
- `customJS`  -用户自定义的JavaScript

#### PreChat Object
- `ifEnabled`  -是否允许Prechat
- `greetingMessage` -Greeting Message内容
- `socialLogin`	-社交媒体登录
  + `ifEnableGoogle`	-是否启用google登录：true/false
  + `ifEnableFacebook`	-是否启用Facebook登录：true/false
- `isRememberForm`	-Prechat是否记录cookie
- `fieldLayoutStyle`	-访客端（prechat、offlineMessage、postChat）窗口中字段的样式：vertical；horizontal
- `fields`  -Prechat页面自定义字段集合
  + [customField](#custom-field)  -自定义字段

##### Custom Field
- `id` -字段的主键
- `name` -自定义字段Name或者自定义变量的Name
- `type`       

| | Type | Description
| --- | --- | ---
| System Field | name | Name field
| | email | Email field
| | phone | Phone field
| | company | Company field
| | product | Product and Service field, used in pre-chat form
| | department | Department field
| | ticket | Ticket field
| | rating | Rating field, available in post chat form
| | comment | Comment field
| | subject | Subject field, available in offline message form
| | content | Content field, available in offline message form
| | attachment | Attachment field, available in offline message form
| | category | Category field, available in agent wrap-up form
| Custom Field | text | Text field
| | textarea | Textarea field
| | radio | Radio Box field
| | checkbox | Check Box field
| | select | Drop Down List field
| | checkboxList | Check Box List field

- `isSystem` -是否是系统字段:true;false;
- `isVisible` -是否显示:true;false;
- `isRequired` -是否必须:true;false;
- `options` -下来菜单的选项列表

#### PostChat Object
- `ifEnabled`  -是否允许Postchat
- `greetingMessage` -Greeting Message内容
- `fieldLayoutStyle`	-访客端（prechat、offlineMessage、postChat）窗口中字段的样式：vertical；horizontal
- `fields`  -自定义字段集合
  + [customField](#custom-field)  -自定义字段

#### Offline Message Object
- `isUseOfflineMessage`  -是否使用Comm100的OfflineMessage。false：不使用；true：使用
- `customOfflinePage`  -isUseOfflineMessage为true时有效  
  + `isOpenInNewWindow`  -OfflineMessage是否在新窗口打开
  + `url`  -新窗口打开的地址
- `greetingMessage` -isUseOfflineMessage为true时有效：Greeting Message内容
- `fieldLayoutStyle`	-访客端（prechat、offlineMessage、postChat）窗口中字段的样式：vertical；horizontal
- `fields`  -isUseOfflineMessage为true时有效：自定义字段集合
  + [customFields](#custom-fields)  -自定义字段
   
#### InvitationButton Object
  - `invitationPosition` -邀请框的位置：Center with Overlay;Center;Top Left ;Top Middle; Top Right;Bottom Left;Bottom Middle;Bottom Right
  - `imageUrl` -邀请按钮图片url
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
  - `invitationMessage`  -邀请显示的内容
  - `textFont`  -Invitaion文本内容字体
  - `textSize`  -Invitaion文本字体大小
  - `textIsBold`  -Invitaion文本内容是否加粗
  - `textIsItalic`  -Invitaion文本内容是否斜体
  - `textColor`  -Invitaion文本颜色

#### AutoInvitation Object 
  - `id` - invitation id
  - `name` -invitation name
  - `isEnable` -是否启用
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

#### Agent Wrapup Object
  - `wrapupFields`  -Wrapup页面自定义字段集合
    + [customField](#custom-field)  -自定义字段

#### Language Object
  - `language` -语言
  - `isCustomizeLanguage` -是否使用自定义语言。false：不使用，使用默认语言 ；true：使用自定义语言
  - `isRTL` -是否从右到左对齐，IsCustomizeLanguage为true时有效。
  - `languageSettingsDetail` 语言配置详情列表
    + [Language Settings](language-settings-object)

#### Language Settings Object
  - `type` -类型：Buttons；Fields；Prompts；SystemMessages；AudioChat；VideoChat；ScreenSharing；TranscriptEmail；TextOnMobile；EmbeddedWindow；Chatbot
  - `name` -当前字段名
  - `defaultText` -默认显示信息
  - `CurrentText` -当前显示信息
  - `macros` -宏

#### Routing Rules Property
  - `isEnableRoute` -是否启用路由规则
  - `routemethod` -department - Route visitors to a specific department or operator；rules - Route visitors based on custom rules
  - [routeSpecificPoint](#route-specific-point) -路由到指定节点，Routemethod为0时有效
  - `routeRules` -路由规则集合，Routemethod为1时有效
    + [routeRule](#route-rule-object) -路由规则对象
  - `failRouteType` -none – 未配置；department – fail route to department；operator – fail route to operator；offlineMessage – redirect to offline message，Routemethod为department时有效
  - `failRouteId` - 失败时路由到的对应ID，Routemethod为department时有效
  - `failRouteMessageTo` -FailRouteType选择redirect to offline message时，填写的收邮件的Email，Routemethod为1时有效

##### Route Rule Object
  - `routeName` -当前路由的名称
  - `isEnable` -是否启用当前这条路由规则
  - `order` -路由规则顺序
  - `routeConditions` -路由条件集合
     + [condition Object](#condition-object)  -条件对象
  - [routeSpecificPoint](#route-specific-point) -路由到指定节点  

##### Route Specific Point
  - `routeType` -路由类型：0:Department;1:Agent
  - `routeId` -路由到对应的id
  - `routePriority` -路由优先级:Lowest;Low;Normal;High;Highest

### Campaign API
  Comm100 Live Chat公开了下面的API来对站点下的Campaign资源进行操作.

| Method | Name | Path
| --- | --- | ---
| GET | [List All Campaigns](https://github.com/Comm100/restful-api/blob/master/settings-api.md#list-all-campaigns) | `/api/v1/livechat/campaigns`
| GET | [Details of ChatButton](#details-of-chatbutton) | `/api/v1/livechat/campaigns/{id}/chatButton`  
| GET | [Details of InvitationButton](#details-of-invitationbutton) | `/api/v1/livechat/campaigns/{id}/invitationButton`  
| GET | [Details of ChatWindow](#details-of-chatwindow) | `/api/v1/livechat/campaigns/{id}/chatWindow`  
| GET | [Details of PreChat](https://github.com/Comm100/restful-api/blob/master/settings-api.md#pre-chat) | `/api/v1/livechat/campaigns/{id}/preChat`  
| GET | [Details of PostChat](https://github.com/Comm100/restful-api/blob/master/settings-api.md#post-chat) | `/api/v1/livechat/campaigns/{id}/postChat`  
| GET | [Details of OfflineMessage](#dhttps://github.com/Comm100/restful-api/blob/master/settings-api.md#offline-message) | `/api/v1/livechat/campaigns/{id}/offlineMessage`  
| GET | [Details of AutoInvitation](https://github.com/Comm100/restful-api/blob/master/settings-api.md#auto-invitation) | `/api/v1/livechat/campaigns/{id}/autoInvitation`  
| GET | [Details of ManualInvitation](#details-of-manualinvitation) | `/api/v1/livechat/campaigns/{id}/manualInvitation`  
| GET | [Details of Agent Wrap Up](https://github.com/Comm100/restful-api/blob/master/settings-api.md#agent-wrap-up) | `/api/v1/livechat/campaigns/{id}/agentWrapup`  
| GET | [Details of Routing Rules](#details-of-routing-rules) | `/api/v1/livechat/campaigns/{id}/RoutingRules`  
| GET | [Details of Language](#details-of-language) | `/api/v1/livechat/campaigns/{id}/language`  

### Details of ChatButton
Gets the details of ChatButton.

#### Path
  `GET https://hosted.comm100.com/api/v1/livechat/campaigns/{id}/chatButton`

#### Parameters
| Name | Description
| --- | ---
| `id`| the id of the campaign, which can be obtained from the [list of all campaigns](#list-all-campaigns)

#### Response
| Name | Description
| --- | ---
| `buttonType ` | the type of button,contains `Adaptive`、`ImageButton` and `TextLink`.
| `buttonColor` | the main color of button,available when buttonType is adaptive
| `iconUrl` | the url of icon,available when buttonType is adaptive
| `imageButton` | the information of image button in desktop app view,available when buttonType is imageButton
| `textContent` | the content of text,available when buttonType is textLink
| `isHideOffline` | whether to hide the chat button when agent is offline
| `sepcifiedDomainsOrUrls` | display the chat button on specified domains or urls 

#### Example
Sample request:

  `curl -u tester@comm100.com:ef43f9362aac4f60ad428cb4d072f2c8 -X GET \`   
  `"https://hosted.comm100.com/api/v1/livechat/campaigns/1/chatButton"`

Sample response:

```json
    {
        "buttonType": "ImageButton",
        "imageButton": {
          "desktopView":{
            "imageUrl":{
              "online":"****/online.jpg",
              "offline":"****/offline.jpg"
            },
            "showButtonType":"float",
            "buttonPosition":"rightMiddle",
            "xOffset":"10",
            "xOffsetIfPixels":"percent",
            "yOffset":"10",
            "yOffsetIfPixels":"percent"
          },
          "mobileView":{
            "showType":"text",
            "textOnline":"on line",
            "textOffline":"offline",
            "backgroundColor":"#FFFFFF"
          }
        },
        "isHideOffline":true,
        "sepcifiedDomainsOrUrls":"www.myCompany.com"
    }
```    

#### Config Object
  Comm100中Livechat的Config对象中包含以下属性：
  - `siteId` -站点编号
  - `isDisplayTimeInfTranscript` -是否在聊天历史里面展示时间
  - `isShowTypingContent` -是否显示正在输入的内容
  - `visitorHeartBeatDelayTime` -访客HeartBeat的持续时间
  - `isAutoAcceptChat` -是否自动接受聊天
  - `isSetMaxChatsCountForEachOperator` -是否为每个Operator设置最大聊天数
  - `maxChatsCountForAllOperator` -IsSetMaxChatsCountForEachOperator 为true，每个Operator默认取的最大聊天数
  - `isPreferOperatorLastChattedWith` -随机路由时，是否允许分配给最近和你聊天的Operator
  - `isDepartmentEnable` -是否允许使用DepartmentEnable
  - `isCreateTicketWhenChatAccepted` -是否在接受聊天的时候创建Ticket
  - `isCreateTicketWhenOfflineMessageSubmitted` -是否在提交留言的时候创建Ticket
  - `isMultipleCodePlan` -是否开启多个Code Plan
  - `isEnableSalesforce` -是否开启Sales force
  - `isEnableCustomVariable` -是否开启自定义变量
  - `aPICallDailyLimit` -每天可以使用API的次数
  - `isEnableZendesk` -是否开启Zendesk
  - `isEnableGoogleAnalytics` -是否开启Google分析
  - `allocationbywhat` -用于判断Chat Auto-Allocation页面中Auto-allocate chat requests to operators based on下方列表如何显示：false – department未开启，显示三个分配方式；true  – department已开启，根据department显示一个列表
  - `allocationstrategy` -department未开启时，记录分配方式：Load Balancing；Round-Robin；Capability Weighted
  - `isEnableAutoAllocation` -是否开启Chat Auto-Allocation
  - `isEnableChatTranslation` -是否开启Auto Translation
  - `isEnableGoToMeeting` -是否开启GoToMeeting
  - `isCustomAwayEnable` -是否开启Custom Away Status
  - `isMaskCreditCardNum` -是否开启隐藏信用卡号
  - `isEnableCustomerSegmentation` -是否开启访客分类
  - `operatorChatFileSizeLimit` -客服发送附件的大小限制(Mb)
  - `operatorChatFileCountDailyLimit` -客服每天发送附件的数量限制
  - `isCanSelectHourlyMinute` -报表查询是否允许使用十分查询
  - `visitorMsgRestrict` -访客端发送文件限制的配置值
  - `isRequireSessionWhenDownloadAttachment` -访客端下载附件时是否需要登录
  - `isEnableJoinMeIntegration` -是否开启joinme
  - `defaultCodePlanId` -Dynamic功能的default codeplan
  - `isEnableAdvancedCategoryMode` -是否开启高级模式的wrapup
  - `isNotAllocateWhenVideoAudio` -是否不分配聊天给正在Audio/Video Chat中的Agent

#### Config API
  Comm100 Live Chat公开了下面的API对站点进行相关配置：
  - `GET /api/v1/livechat/configs` -获取站点的配置
  - `POST /api/v1/livechat/configs` -创建站点的配置
  - `PUT /api/v1/livechat/configs/{config_id}` -更新站点的配置

#### Canned Message Object
  Canned  Message对象包含以下属性：
  - `id` -主键id
  - `message`  -内容
  - `categoryId` -所属类型的主键Id
  - `isPrivate` -是否为私有
  - `shortcuts` -快捷键

#### Canned Messages API
  Comm100 Live Chat公开了下面的API来对[Canned Messaged Object](#canned-message-object)进行访问:
  - `GET /api/v1/livechat/cannedMessages` -获取站点下面的所有Canned Messages   
  - `GET /api/v1/livechat/cannedMessages/{cannedMessage_id}` -获取站点下面的一个特定的Canned Messages   
  - `POST /api/v1/livechat/cannedMessages` -新建一个Canned Messages   
  - `PUT /api/v1/livechat/cannedMessages/{cannedMessage_id}` -更新一个Canned Messages   
  - `DELETE /api/v1/livechat/cannedMessages/{cannedMessage_id}` -删除一个Canned Messages  
  
  - `GET /api/v1/livechat/cannedMessageCategories` -获取站点下面的所有Canned Messages的category
  - `GET /api/v1/livechat/cannedMessageCategories/{category_id}` -获取站点下面的一个特定的category  
  - `POST /api/v1/livechat/cannedMessageCategories` -新建一个category   
  - `PUT /api/v1/livechat/cannedMessageCategories/{category_id}` -更新一个category   
  - `DELETE /api/v1/livechat/cannedMessageCategories/{category_id}` -删除一个category  

### Custom Away Status API
  Comm100 Live Chat公开了下面的API来对自定义Away的状态进行访问：
  - `GET /api/v1/livechat/customAwayStatuses` -获取站点所有的自定义Away状态
  - `POST /api/v1/livechat/customAwayStatuses` -创建自定义Away状态
  - `PUT /api/v1/livechat/customAwayStatuses/{status_id}` -更新自定义Away状态

#### Customer Segment Object
  用户细分对象中包含了下面的属性：
  - `id` -主键Id
  - `siteId` -SiteId
  - `name` -客户细分的名字
  - `description` -描述
  - `color` -客户细分的颜色配置
  - `isEnable` -是否启用
  - `priority` -客户细分的优先级
  - `alertToType` -发送通知对象的类型：Department；Operator
  - `alertToIds` -发送通知的对象的Id列表：与Type相关，如果类型为Department则为DepartmentId，如果为Operator，则为OperatorId
  - `isDeleted` -是否已经被删除
  - `enumConditionExpression` -Customer Segment的各个Condition之间的条件关系
  - `conditionExpression` -各个条件之间的关系表达式

### Visitor Segmentation API
  Comm100 Live Chat公开了下面的API来对用户细分进行访问：
  - `GET /api/v1/livechat/customerSegments` -获取站点所有自定义用户细分信息
  - `GET /api/v1/livechat/customerSegments/{segment_id}` -查询一个用户细分
  - `POST /api/v1/livechat/customerSegments` -新建一个用户细分
  - `PUT /api/v1/livechat/customerSegments/{segment_id}` -更新用户细分
  - `DELETE /api/v1/livechat/customerSegments/{segment_id}` -删除用户细分
