# General
|Object     | Path               | Support                                                                                                   
| ------------- |------------------------------- | -------------------------------------- 
| [Campaign](#campaign)        |/livechat/campaigns                    | 1       
| [Canned Message](#canned-message)       |/livechat/cannedMessages                    | 1       
| [Canned Message Category](#canned-message-category)       |/livechat/cannedMessageCategories                    | 1       
| [Department](#department)        |/livechat/departments                    | 1       
| [Auto Allocation](#auto-allocation)      |/livechat/autoAllocation               | 1       
| [Custom Away Status](#custom-away-status)  |/livechat/customAwayStatus                    | 1       
| [Ban](#ban)  |/livechat/bans                    | 1            
| [Conversion Action](#conversion-action)   |/livechat/conversionActions                    | 1            
| [Visitor Segmentation](#visitor-segmentation)   |/livechat/visitorSegments                    | 1
| [Visitor SSO Settings](#visitor-sso-settings) |/livechat/visitorSSO                    | 1
| [Site Config](#site-config) |/livechat/configs                    | 1
| [Secure Forms](#secure-form) |/livechat/secureForms                    | 1
| [Webhooks](#webhooks) |/livechat/webhooks                    | 1
| [Custom Variables](#custom-variables) |/livechat/customVariables                    | 1
| [Agent](#agent) |/livechat/agents                    | 1
| [Chat](#chat) |/livechat/chats                    | 1
| [Message](#message) |/livechat/messages                    | 1
      
## Campaign
  You need `Manage Campaigns` permission to manage campaigns and customize the settings for a campaigns.
  - `Campaigns` -Campaigns Manage
    + `GET /api/v1/livechat/campaigns` -Get list of campaigns
    + `POST /api/v1/livechat/campaigns` -Create a new campaign
    + `PUT /api/v1/livechat/campaigns/{id}` -Update a campaign
    + `DELETE /api/v1/livechat/campaigns/{id}` -Remove a campaign
  - `Campaign Settings` --setting of campaign
    + `GET /api/v1/livechat/campaigns/{id}/code` -Get installation code for a campaign
    + `GET /api/v1/livechat/campaigns/{id}/chatButton` -Get settings of ChatButton for a campaign
    + `PUT /api/v1/livechat/campaigns/{id}/chatButton` -Update settings of ChatButton for a campaign
    + `GET /api/v1/livechat/campaigns/{id}/chatWindow`  -Get settings of ChatWindow for a campaign
    + `PUT /api/v1/livechat/campaigns/{id}/chatWindow`  -Update settings of ChatWindow for a campaign
    + `GET /api/v1/livechat/campaigns/{id}/preChat`  -[Get settings of PreChat for a campaign](https://gist.github.com/chendesheng/50e9b63573f09a1c1a76c1f4ec074ac9#campaigns)
    + `PUT /api/v1/livechat/campaigns/{id}/preChat`  -Update settings of PreChat for a campaign
    + `GET /api/v1/livechat/campaigns/{id}/postChat` -[Get settings of PostChat for a campaign](https://gist.github.com/chendesheng/50e9b63573f09a1c1a76c1f4ec074ac9#campaigns)
    + `PUT /api/v1/livechat/campaigns/{id}/postChat` -Update settings of PostChat for a campaign
    + `GET /api/v1/livechat/campaigns/{id}/offlineMessage`  -[Get settings of OfflineMessage for a campaign](https://gist.github.com/chendesheng/50e9b63573f09a1c1a76c1f4ec074ac9#campaigns)
    + `PUT /api/v1/livechat/campaigns/{id}/offlineMessage`  -Update settings of OfflineMessage for a campaign
    + `GET /api/v1/livechat/campaigns/{id}/invitation`  -[Get settings of invitation for a campaign](https://gist.github.com/chendesheng/50e9b63573f09a1c1a76c1f4ec074ac9#campaigns)
    + `PUT /api/v1/livechat/campaigns/{id}/invitation`  -Update settings of invitation for a campaign
    + `GET /api/v1/livechat/campaigns/{id}/invitation/autoInvitations/{autoInvitation_id}`  -Get a autoInvitation for a campaign
    + `POST /api/v1/livechat/campaigns/{id}/invitation/autoInvitations`  -Create a new auto invitation for a campaign
    + `PUT /api/v1/livechat/campaigns/{id}/invitation/autoInvitations/{autoInvitation_id}`  -Update a auto invitation for a campaign
    + `GET /api/v1/livechat/campaigns/{id}/agentWrapup`  -[Get settings of Agent Wrap Up for a campaign](https://gist.github.com/chendesheng/50e9b63573f09a1c1a76c1f4ec074ac9#campaigns)
    + `PUT /api/v1/livechat/campaigns/{id}/agentWrapup`  -Update settings of Agent Wrap Up for a campaign
    + `GET /api/v1/livechat/campaigns/{id}/RoutingRules` -Get settings of Routing Rules for a campaign
    + `PUT /api/v1/livechat/campaigns/{id}/RoutingRules` -Update settings of Routing Rules for a campaign
    + `GET /api/v1/livechat/campaigns/{id}/RoutingRules/customRules/{customeRule_id}` -Get a custom rule for a campaign
    + `POST /api/v1/livechat/campaigns/{id}/RoutingRules/customRules` -Create a new custom rule for a campaign
    + `PUT /api/v1/livechat/campaigns/{id}/RoutingRules/customRules/{customeRule_id}` -Update a custom rule for a campaign
    + `GET /api/v1/livechat/campaigns/{id}/language`  Get settings of Language for a campaign
    + `PUT /api/v1/livechat/campaigns/{id}/language`  Update settings of Language for a campaign

### Campaign Json Format
 Campaign is represented as simple flat JSON objects with the following keys:  

|name     | Type               | Read-only    | Mandatory      |  Description                                                                                                   
| ------------- |--------------------- | ---------- | -------------------- | ------------------ 
| id | integer  | yes  | no| id of the campaign
| name| string  | no  | yes|name of the campaign
| description| string  | no  | no|description of the campaign
| language| string  | no  | yes|language of the campaign

### Get list of campaigns
- End Point      
  `GET /api/v1/livechat/campaigns`
    
- Parameters     
  No parameters
    
- Response      
  An array of Campaign Json Object.
       
### Create a new campaign
- End Point      
  `POST /api/v1/livechat/campaigns`
       
- Parameters     
  Campaign Json Object
       
- Response      
  Campaign Json Object
       
### Update a campaign
- End Point      
  `PUT /api/v1/livechat/campaigns/{id}`
       
- Parameters     
  Campaign Json Object
       
- Response      
  Campaign Json Object
       
### Remove a campaign 
- End Point      
  `DELETE /api/v1/livechat/campaigns/{id}`
       
- Parameters     
  No parameters.
    
- Response      
  Status: 200 OK   
      
### Get installation code for a campaign
- End Point      
  `GET /api/v1/livechat/campaigns/{id}/code`
      
- Parameters     
  No parameters
      
- Response      
  - `code` -installation code for the campaign.
      
### Chat Button Json Format
 Chat Button is represented as simple flat JSON objects with the following keys:  
      
|name     | Type               | Read-only    | Mandatory      |  Description                                                                                                   
| ------------- |--------------------- | ---------- | -------------------- | ------------------ 
|buttonType | string | no | yes |    type of the button,including `adaptive`、`image` and `textLink`.
|isHideOffline| boolean | no | no |    whether the chatButton is visible when no agent is online.`true` means that button is invisible..
|isEnableDomainRestriction| boolean | no | no |    whether the domain restriction is enable or not.
|allowedDomains| array | no | no |    an array of domains/urls,on which the chat button is visible.
|adaptive.themeColor| string | no | no |     the theme color of chatbutton,available when `buttonType` is `adaptive`.
|adaptive.icon| string | no | no |     icon of the chat button,available when `buttonType` is `adaptive`.
|image.type| string | no | no |     the type of the image ,including `gallery` and `upload`,available when `buttonType` is `image`.
|image.onlineImageId| integer | no | no |     id of the image when any agents are on line,available when `buttonType` is `image`.
|image.offlineImageId| integer | no | no |     id of the image when no agent is on line,available when `buttonType` is `image`.
|image.onlineImageUrl| string | no | no |     url of the image when any agents are on line,available when `buttonType` is `image`.
|image.offlineImageUrl| string | no | no |     url of the image when no agent is on line,available when `buttonType` is `image`.
|image.isFloat| boolean | no | no |    whether the chat button is float or not,available when `buttonType` is `image`.
|image.position.type| string | no | no |     position of the chat button,including `centered`、`topLeft`、`topMiddle`、`topRight`、`buttomLeft`、`buttomMiddle`、`buttomRight`、`leftMiddle` and `rightMiddle`,available when `buttonType` is `image`.
|image.x.isPixels| boolean | no | no |     whether the unit of coordinate x the button is pixel or percent, `true` means pixel and `false` means percent,available when `buttonType` is `image`.
|image.position.x| float | no | no |    coordinate x of the button,the unit acoording to `buttonXIsPixels`,available when `buttonType` is `image`.
|image.y.IsPixels| boolean | no | no |  whether the unit of coordinate Y the button is pixel or percent, `true` means pixel and `false` means percent,available when `buttonType` is `image`.
|image.position.y| float | no | no |    coordinate y of the button,the unit acoording to `buttonYIsPixels`,available when `buttonType` is `image`.
|image.mobile.Type| string | no | no |    the type of button on mobile device,including `text` and `image`,available when `buttonType` is `image`.
|image.mobile.onlineText| string | no | no |    the content of text on mobile device when any agents are on line,available when `mobileButtonType` is `text`and `buttonType` is `image`.
|image.mobile.offlineText| string | no | no |    the content of text on mobile device when no agent is on line,available when `mobileButtonType` is `text`and `buttonType` is `image`.
|image.mobile.themeColor| string | no | no |     the theme color of chatbutton on mobile device,available when `mobileButtonType` is `text`and `buttonType` is `image`.
|image.mobile.onlineImageUrl| string | no | no |    the url of image on mobile device when any agents are on line,available when `mobileButtonType` is `image`and `buttonType` is `image`.
|image.mobile.offlineImageUrl| string | no | no |    the url of image on mobile device when no agent is on line,available when `mobileButtonType` is `image` and `buttonType` is `image`.
|image.mobile.position.type| string | no | no |     position of the chat button on mobile device， including `bottomLeft`、`bottomMiddle`、`bottomRight`、`leftMiddle`、`RightMiddle`、`leftBottom` and `rightBottom`,available when `mobileButtonType` is `image` and `buttonType` is `image`.
|buttonText| string | no | no |    the content of the text link,available when `buttonType` is `textLink`.
      
### Get settings of ChatButton for a campaign
- End Point      
  `GET /api/v1/livechat/campaigns/{id}/chatButton`
      
- Parameters     
  No parameters
      
- Response      
  Chat Button Json Object.
      
### Update settings of ChatButton for a campaign
- End Point      
  `PUT /api/v1/livechat/campaigns/{id}/chatButton`
      
- Parameters     
  Chat Button Json Object
     
- Response      
  Chat Button Json Object.
     
### Chat Window Json Format
 Chat Window is represented as simple flat JSON objects with the following keys:  
     
|name     | Type               | Read-only    | Mandatory      |  Description                                                                                                   
| ------------- |--------------------- | ---------- | -------------------- | ------------------ 
|style| string | no | yes |    style of the window's theme,including `classic`、`simple` and `bubble`.
|color| string | no | yes |    color of the window's theme.
|type| string | no | yes |     type of the chat window,including `embedded` and `popup`.
|title| string | no | no |     title of the chat window,available when `windowType` is `popup`.
|visitor.isCanPrintChatDetail| boolean | no | no |    chat details can be printed 
|visitor.isShowEmail| boolean | no | no |    chat transcripts can be emailed to visitors 
|visitor.isUseOperatorEmailOrFromEmail| boolean | no | no |  whether email is setted from agent email or from a specified address.
|specifiedEmail| string | no | no |     a specified email for setting visitor's address.
|specifiedName| string | no | no |     a specified name for setting visitor's address.
|visitor.isCanSwitchToOffline| boolean | no | no |  allow visitors to switch to Offline Message Window while waiting for chat. 
|visitor.isCanSendFile| boolean | no | no |     whether the agent can send file or not.
|visitor.isCanHaveAudioChat| boolean | no | no |    whether the agent can use audio chat.
|visitor.isCanHaveVideoChat| boolean | no | no |    whether the agent can use video chat.
|isEndChatWhenVisitorInactivity| boolean | no | no |  whether chat ends automatically if visitors don't respond.
|timeEndChatDelayWhenVisitorInactivity| integer | no | no |    the time after the chat was end when visitor inactivity,the unit is second.
|isEnableSendTranscriptEmail| boolean | no | no |    whether the agent can send transcript email after chat ending.
|transcriptEmailAddress| string | no | no |    the email address for sending transcript email.
|transcriptEmailSubject| string | no | no |    the subject address for sending transcript email.
|greetingMessage| string | no | no |    the content of greeting message.
|isEnableCustomJS| boolean | no | no |    whether the agent can add custom js to chat window or not.
|customJS| string | no | no |    the content of custom javascript.
|customCSS| string | no | no |     the content of custom css.
|headerType| string | no | no |     type of the header,including `agentInfo`、`bannerImage` when `themeType` is `classic`,including `agentInfo`、`bannerImage` and `avatarAndCompanyLogo` when `themeType` is `simple`.
|header.isShowDisplayName| boolean | no | no |     whether the display name of the agent is visible or not,available when `themeType` is `classic`or `simple` and `headerType` is `agentInfo`.
|header.isShowAvatar| boolean | no | no |     whether the avatar of the agent is visible or not,available when `themeType` is `classic`or `simple` and `headerType` is `agentInfo` or `avatarAndCompanyLogo`.
|header.isShowTitle| boolean | no | no |      whether the title of the agent is visible or not,available when `themeType` is `classic`or `simple` and `headerType` is `agentInfo`.
|header.isShowBio| boolean | no | no |      whether the bio of the agent is visible or not,available when `themeType` is `classic`or `simple` and `headerType` is `agentInfo`.
|header.imageType| string | no | no |     the type of the image ,including `gallery` and `upload`,available when `themeType` is `classic`or `simple`.
|header.imageId| integer | no | no |     id of the image in the header of chat window,available when `themeType` is `classic`or `simple` and `headerType` is `bannerImage`.
|header.imageUrl| string | no | no |     url of the image in the header of chat window,available when `themeType` is `classic`or `simple` and `headerType` is `bannerImage`.
|header.isShowLogo| boolean | no | no |     whether the logo of the company is visible or not,available when `themeType` is `classic` and `headerType` is `avatarAndCompanyLogo`.
|header.companyImageId| string | no | no |     id of the company image in the header of chat window,available when `themeType` is `classic` and `headerType` is `avatarAndCompanyLogo` .
|header.companyImageUrl| string | no | no |     url of the company image in the header of chat window,available when `themeType` is `classic` and `headerType` is `avatarAndCompanyLogo`.
|body.isShowAvatarWithMessage| boolean | no | no |     whether the avatar of the agent is visible or not in the messsage body,available when `themeType` is `classic`or `simple`.
|body.isShowTextureWithMessage| boolean | no | no |     whether the texture and picture of the background is visible or not in the messsage body,available when `themeType` is `classic`or `simple`.
|body.backgroudImageId| integer | no | no |     id of the background image in the message body,available when `themeType` is `classic`or `simple`.
|body.backgroudImageUrl| string | no | no |     url of the company image in the message body,available when `themeType` is `classic`or `simple`.
     
### Get settings of ChatWindow for a campaign
- End Point      
  `GET /api/v1/livechat/campaigns/{id}/chatWindow`
     
- Parameters     
  No parameters
     
- Response      
  Chat Window Json Object
     
### Update settings of ChatWindow for a campaign
- End Point      
  `PUT /api/v1/livechat/campaigns/{id}/chatWindow`
     
- Parameters     
  Chat Window Json Object
     
- Response      
  Chat Window Json Object

### Pre-Chat Json Format
 Pre-Chat is represented as simple flat JSON objects with the following keys:  
     
|name     | Type               | Read-only    | Mandatory      |  Description                                                                                                   
| ------------- |--------------------- | ---------- | -------------------- | ------------------ 
|isEnable| boolean | no | yes |    whether the pre-chat is enable or not.
|header.isShowTeamName| boolean | no | no |    whether the name of the agent is visible or not in the header.
|header.isShowAvatar| boolean | no | no |    whether the avatar of the agent is visible or not in the header.
|greetingMessage| string | no | no |     content of greeting message.
|isEnableGoogle| boolean | no | no |    whether google is enable or not in social login.
|isEnableFacebook| boolean | no | no |    whether facebook is enable or not in social login.
|isRememberForm| boolean | no | no |    whether visitor info is remembered or not from pre-chat form.
|fieldLayoutStyle| string | no | yes |    the layout style of field,including `labelLeftSideInput` and `labelAboveInput`.
|fields| Array | no | no |     an array of [field](#field-json-format) object 

### Field Json Format
Field is represented as simple flat JSON objects with the following keys:  
     
|name     | Type               | Read-only    | Mandatory      |  Description                                                                                                   
| ------------- |--------------------- | ---------- | -------------------- | ------------------ 
|id| integer | yes | no |     id of the field
|name| string | no | yes |     name of the field
|[type](#field-type)| string | no | yes |     the type of the field
|isSystem| boolean | no | no |     whether the field is system field or not.
|isVisible| boolean | no | no |     whether the field is visible or not .
|isRequired| boolean | no | no |     whether the field is required or not when submiting the form
|options| string | no | no |     the options of the field.

### Field Type
  Field Type is one key of the following keys:    

|name          | isSystemField | isCustomField | description         
| ------------- |---------------- | ----- | ----- 
|name| yes | no |     Name field,available not in secure form.
|email| yes  | no |     Email field,available not in secure form.
|phone| yes  | no |     Phone field,available not in secure form.
|company| yes  | no |     Company field,available not in secure form.
|product| yes  | no |     Product and Service field,available not in secure form.
|department| yes  | no |     Department field,available not in secure form.
|ticket| yes  | no |     Ticket field,available not in secure form.
|rating| yes  | no |     Rating field,available not in secure form.
|comment| yes  | no |     Comment field,available not in secure form.
|subject| yes  | no |     Subject field,available not in secure form.
|content| yes  | no |     Content field,available not in secure form.
|attachment| yes  | no |     Attachment field,available not in secure form.
|cardNumber|  yes | no |     card number field ,available in secure form.
|expirationDate|  yes | no |     expiration date field,available in secure form.
|cscOrCvv|  yes | no |     csc/cvv field ,available in secure form.
|nameOnCard|  yes | no |     name on card field ,available in secure form.
|text|  no | yes |     Text field 
|textarea|  no | yes |     Textarea field 
|radio|  no | yes |     Radio Box field 
|checkbox|  no | yes |     Check Box field 
|select|  no | yes |     Drop Down List field 
|checkboxList | no | yes |     Check Box List field 
     
### Update settings of PreChat for a campaign
- End Point      
  `PUT /api/v1/livechat/campaigns/{id}/prechat`
     
- Parameters     
  Pre-Chat Json Object
     
- Response      
Pre-Chat Json Object
     
### Post-Chat Json Format
 Post-Chat is represented as simple flat JSON objects with the following keys:  
     
|name     | Type               | Read-only    | Mandatory      |  Description                                                                                                   
| ------------- |--------------------- | ---------- | -------------------- | ------------------ 
|isEnable| boolean | no | yes |    whether the post-chat is enable or not.
|greetingMessage| string | no | no |     content of greeting message.
|isEnableGoogle| boolean | no | no |    whether google is enable or not in social login.
|isEnableFacebook| boolean | no | no |    whether facebook is enable or not in social login.
|isRememberForm| boolean | no | no |    whether visitor info is remembered or not from post-chat form.
|fieldLayoutStyle| string | no | no |    the layout style of field,including `labelLeftSideInput` and `labelAboveInput`.
|fields| Array | no | no |     an array of [field](#field-json-format) object
     
### Update settings of PostChat for a campaign
- End Point      
  `PUT /api/v1/livechat/campaigns/{id}/postchat`
     
- Parameters     
  Post-Chat Json Object
     
- Response      
  Post-Chat Json Object
     
### Offline Message Json Format 
 Offline Message is represented as simple flat JSON objects with the following keys:  
     
|name     | Type               | Read-only    | Mandatory      |  Description                                                                                                   
| ------------- |--------------------- | ---------- | -------------------- | ------------------ 
|isUseCustomOfflinePage| boolean | no | yes |    whether the custom offline message page is used or not.
|greetingMessage| string | no | no |     content of greeting message.
|url| string | no | no |    url of custom offline message page.
|isOpenInNewWindow| boolean | no | no |    whether open page in a new window or not.
|header.isShowTeamName| boolean | no | no |    whether the name of the agent is visible or not in the header.
|header.isShowAvatar| boolean | no | no |    whether the avatar of the agent is visible or not in the header.
|fieldLayoutStyle| string | no | no |    the layout style of field,including `labelLeftSideInput` and `labelAboveInput`.
|fields| Array | no | no |     an array of [field](#field-json-format) object
     
### Update settings of offline message for a campaign
- End Point      
  `PUT /api/v1/livechat/campaigns/{id}/offlineMessage`
     
- Parameters     
Offline Message Json Object
     
- Response      
Offline Message Json Object

### Invitation Window Json Format    
 Invitation Window is represented as simple flat JSON objects with the following keys:  
     
|name     | Type               | Read-only    | Mandatory      |  Description                                                                                                   
| ------------- |--------------------- | ---------- | -------------------- | ------------------ 
|invitationMessage|string  | no  | no| content of invitation message.
|imageType|string  | no  | yes| the type of image source,including `gallery` or `upload`
|imageId|integer  | no  | no|id of invitation image.
|imageUrl|string  | no  | no|url of invitation image.
|invitationPosition|string  | no  | no| the position of invitation window,including `centered`、`centeredWithOverlay`、`topLeft`、`topMiddle`、`topRight`、`buttomLeft`、`buttomMiddle`、`buttomRight`、`leftMiddle` and `rightMiddle`.
|invitationXOffset|float  | no  | no|coordinate x of the button,the unit acoording to `buttonXIsPixels`
|invitationYOffset|float  | no  | no|coordinate y of the button,the unit acoording to `buttonYIsPixels`
|invitationXOffsetIfPixels|boolean  | no  | no|whether the unit of coordinate x the button is pixel or percent, `true` means pixel and `false` means percent.
|invitationYOffsetIfPixels|boolean  | no  | no| whether the unit of coordinate Y the button is pixel or percent, `true` means pixel and `false` means percent.
|textFont|string  | no  | no| the font of text.
|textIsBold|boolean  | no  | no| whether the text is bold or not.
|textSize|string  | no  | no| the size of text.
|textIsItalic|boolean  | no  | no| whether the text is italic or not.
|textColor|string  | no  | no| the color of text.
|closeAreaXOffset|float  | no  | no| coordinate x of the close area
|closeAreaYOffset|float  | no  | no| coordinate y of the close area
|closeAreaWidth|float  | no  | no| width of the close area
|closeAreaHeight|float  | no  | no| height of the close area
|textAreaXOffset|float  | no  | no| coordinate x of the text area
|textAreaYOffset|float  | no  | no| coordinate y of the text area
|textAreaWidth|float  | no  | no| width of the text area
|textAreaHeight|float  | no  | no| height of the text area
|invitationStyle|string  | no  | yes|the layout style of invitation window,including `bubble`、`popup` and `chatWindow`.

### Auto Invitation Json Format
Auto Invitation is represented as simple flat JSON objects with the following keys:  
     
|name     | Type               | Read-only    | Mandatory      |  Description                                                                                                   
| ------------- |--------------------- | ---------- | -------------------- | ------------------ 
|id|integer  | yes  | no| id of the auto invitation.
|name|string  | no  | yes| name of auto invitation.
|isEnable|boolean  | no  | yes| whether the auto invitation is enable or not.
|isPopupOnlyOneTime|boolean  | no  | no| whether pop up only one time during one visit
|invitationWindow|[invitationWindow](#invitation-window-json-format)  | no  | no| an invitation window json object.
|triggerCondition|[triggerCondition](#trigger-condition-json-format)  | no  | no| an trigger condition json object.

### Trigger Condition Json Format
Trigger Condition is represented as simple flat JSON objects with the following keys:  
     
|name     | Type               | Read-only    | Mandatory      |  Description                                                                                                   
| ------------- |--------------------- | ---------- | -------------------- | ------------------ 
|triggeredWhen|string  | no  | no| when the rule is triggered, including `all`、`any` and `logicalExpression` 
|logicalExpression|string  | no  | no| the logical expression of the conditions
|conditions|array  | no  | no|an array of [condition](#condition-json-format)

### condition Json Format
Condition is represented as simple flat JSON objects with the following keys:  
     
|name     | Type               | Read-only    | Mandatory      |  Description                                                                                                   
| ------------- |--------------------- | ---------- | -------------------- | ------------------ 
|variableName|string  | no  | yes| name of the variable,including comm100 system variable and custom variable
|expression|string  | no  | yes| expression of the condition
|value|string  | no  | yes| the value response to the variable

### Get settings of invitation for a campaign
- End Point      
  `GET /api/v1/livechat/campaigns/{id}/invitation`
     
- Parameters     
  No parameters
     
- Response      
  - `autoInvitations` - an array of [auto invitation](#auto-invitation-json-format) json object.
  - `manualInvitation` - [invitation window](#invitation-window-json-format) json object
     
## Update settings of invitation for a campaign
- End Point      
  `PUT /api/v1/livechat/campaigns/{id}/invitation`
      
- Parameters     
  - `autoInvitations` - an array of [auto invitation](#auto-invitation-json-format) json object.
  - `manualInvitation` - [invitation window](#invitation-window-json-format) json object
      
- Response      
  - `autoInvitations` - an array of [auto invitation](#auto-invitation-json-format) json object.
  - `manualInvitation` - [invitation window](#invitation-window-json-format) json object
      
### Get a autoInvitation for a campaign
- End Point      
  `GET /api/v1/livechat/campaigns/{id}/invitation/autoInvitations/{autoInvitation_id}`
      
- Parameters     
  No parameters
      
- Response      
  Auto Invitation Json Object
      
## Create a new auto invitation for a campaign
- End Point      
  `POST /api/v1/livechat/campaigns/{id}/invitation/autoInvitations`
       
- Parameters     
  Auto Invitation Json Object
       
- Response      
  Auto Invitation Json Object
       
## Update a auto invitation for a campaign
- End Point      
  `PUT /api/v1/livechat/campaigns/{id}/invitation/autoInvitations/{autoInvitation_id}`
       
- Parameters     
  Auto Invitation Json Object
       
- Response      
  Auto Invitation Json Object
       
### Update settings of agent wrap-up for a campaign
- End Point      
  `PUT /api/v1/livechat/campaigns/{id}/agentWrapup`
     
- Parameters     
  an array of field json object 
     
- Response      
  an array of field json object 
     
### Custom Rule Json Format
Custom Rule is represented as simple flat JSON objects with the following keys:  
     
|name     | Type               | Read-only    | Mandatory      |  Description                                                                                                   
| ------------- |--------------------- | ---------- | -------------------- | ------------------ 
|id|integer  | yes  | no| id of the custom rule
|name|string  | no  | yes |name of the custom rule
|triggerCondition|[triggerCondition](#trigger-condition-json-format)  | no  | no| an trigger condition json object.
|routeType|string  | no  | yes | type of the route,including `agent` and `department`, value `department` is available when config of department is open.
|routeOjbectId|integer  | yes  | yes | id of the route object
|priority|string  | no  | no | the priority of the route object,including `lowest`、`low`、`normal`、`high` and `highest`.
|isEnable|boolean  | no  | yes |whether the custom rule is enable or not.

### Route Rule Json Format
Route Rule is represented as simple flat JSON objects with the following keys:  
     
|name     | Type               | Read-only    | Mandatory      |  Description                                                                                                   
| ------------- |--------------------- | ---------- | -------------------- | ------------------ 
|isEnable|boolean  | no  | yes |whether the routing rules is enable or not.
|routingType|string  | no  | no |the type of routing,including `routeDepartmentOrAgent` and `routeCustomRules`.
|routeRule|string  | no  | no | the rule of route ,including `department` and `agent`
|routeOjbectId|integer  | yes  | no | id of the route object
|routePriority|string  | no  | no | the priority of the route object,including `lowest`、`low`、`normal`、`high` and `highest`.
|customRules|array  | no  | no | an array of [Custom Rule](#custom-rule-json-format) json object.
|failRoutingType|string  | no  | no |the type of fail routing,including `routeDepartmentOrAgent` and `routeCustomRules`.
|failRouteRule|string  | no  | no | the rule of fail route ,including `department` and `agent`
|failRouteOjbectId|integer  | yes  | no | id of the route object
|failRoutePriority|string  | no  | no | the priority of fail route object,including `lowest`、`low`、`normal`、`high` and `highest`.
|failToEmail|string  | no  | no | redirect them to Offline Message Window and forward their messages to the email

### Get settings of Routing Rules for a campaign
- End Point      
  `GET /api/v1/livechat/campaigns/{id}/RoutingRules`
     
- Parameters     
  No parameters
     
- Response      
Route Rule Json Object
     
### Update settings of Routing Rules for a campaign
- End Point      
  `PUT /api/v1/livechat/campaigns/{id}/RoutingRules`
    
- Parameters     
Route Rule Json Object
     
- Response      
Route Rule Json Object
     
### Get a custom rule for a campaign
- End Point      
  `GET /api/v1/livechat/campaigns/{id}/RoutingRules/customRules/{customeRule_id}`
     
- Parameters     
  No parameters
     
- Response      
Custom Rule Json Object
     
### Create a new custom rule for a campaign
- End Point      
  `POST /api/v1/livechat/campaigns/{id}/RoutingRules/customRules`
     
- Parameters     
Custom Rule Json Object 
     
- Response      
Custom Rule Json Object
     
### Update a custom rule for a campaign
- End Point      
  `PUT /api/v1/livechat/campaigns/{id}/RoutingRules/customRules/{customeRule_id}` 
     
- Parameters     
Custom Rule Json Object
     
- Response      
Custom Rule Json Object

### Custom Language Json Format   
Custom Language is represented as simple flat JSON objects with the following keys:  
     
|name     | Type               | Read-only    | Mandatory      |  Description                                                                                                   
| ------------- |--------------------- | ---------- | -------------------- | ------------------ 
|id |integer  | yes  | no |id of the custom language.
|module|string  | no  | yes | the module of custom language,including `Buttons`、`Fields`、`Prompts`、`SystemMessages`、`AudioChat`、`VideoChat`、`ScreenSharing`、`TranscriptEmail`、`TextOnMobile`、`EmbeddedWindow` and `Chatbot`. 
|name|string  | no  | yes |the name of field of the custom language.
|defaultText|string  | no  | no | the default text of field of the custom language.
|currentText|string  | no  | no | current text of field of the custom language.
|macros|string  | no  | no | macors which used in the field of the custom language.

### Language Json Format
Language is represented as simple flat JSON objects with the following keys:  
     
|name     | Type               | Read-only    | Mandatory      |  Description                                                                                                   
| ------------- |--------------------- | ---------- | -------------------- | ------------------
|language |string  | no  | yes |the main language.
|isCustomLanguage|boolean  | no  | yes | whether the custom language is used or not.
|isRTL|boolean | no  | no |whether the language is from right to left.
|customLanguages|array  | no  | no |an array of [Custom Language](#custom-language-json-format)

### Get settings of Language for a campaign
- End Point      
  `GET /api/v1/livechat/campaigns/{id}/language`
     
- Parameters     
  No parameters
     
- Response      
Language Json Object
    
### Update settings of Language for a campaign
- End Point      
  `PUT /api/v1/livechat/campaigns/{id}/language`
    
- Parameters     
Language Json
    
- Response      
Language Json
    
## Canned Message
  You need `Manage Pulbic Canned Messages` permission to manage canned message.
  + `GET /api/v1/livechat/cannedMessages` -get list of canned Message
  + `GET /api/v1/livechat/cannedMessages/{id}`  -get a single canned Message
  + `POST /api/v1/livechat/cannedMessages` -create a new canned Message
  + `PUT /api/v1/livechat/cannedMessages/{id}`  -update a canned Message
  + `DELETE /api/v1/livechat/cannedMessages/{id}`  -remove a canned Message
    
### Canned Message Json Format
Canned Message is represented as simple flat JSON objects with the following keys:  
     
|name     | Type               | Read-only    | Mandatory      |  Description                                                                                                   
| ------------- |--------------------- | ---------- | -------------------- | ------------------
|id |integer  | yes  | no |id of the canned message.
|name|string  | no  | yes |name of the canned message.
|message|string  | no  | yes |content of the canned message.
|shortcuts|string  | no  | no | shortcuts of the canned message.
|categoryId|integer  | no  | yes |id of the category of the canned message.
|isPrivate|boolean  | no  | yes | whether the canned message is private or not.
    
### Get list of canned messages 
- End Point       
  `GET /api/v1/livechat/cannedMessages`
     
- Parameters     
  No parameters
    
- Response      
 An array of Canned Message Json Object.
    
### Get a single canned message 
- End Point       
  `GET /api/v1/livechat/cannedMessages/{id}`
    
- Parameters     
  No parameters
    
- Response      
Canned Message Json Object
    
### Create a new canned message 
- End Point       
  `POST /api/v1/livechat/cannedMessages`
    
- Parameters     
Canned Message Json Object
    
- Response      
Canned Message Json Object
    
### Update a canned message 
- End Point       
  `PUT /api/v1/livechat/cannedMessages/{id}`
    
- Parameters     
Canned Message Json Object
    
- Response      
Canned Message Json Object
    
### Remove a canned message 
- End Point       
  `DELETE /api/v1/livechat/cannedMessages/{id}`
    
- Parameters     
  No parameters
    
- Response      
  Status: 200 OK   
    
## Canned Message Category
  You need `Manage Pulbic Canned Messages` permission to manage canned message category.
  + `GET /api/v1/livechat/cannedMessageCategories` -get list of canned Messages Categories
  + `GET /api/v1/livechat/cannedMessageCategories/{id}`  -get a single canned Messages Category
  + `POST /api/v1/livechat/cannedMessageCategories` -create a new canned Messages Category
  + `PUT /api/v1/livechat/cannedMessageCategories/{id}`  -update a canned Messages Category
  + `DELETE /api/v1/livechat/cannedMessageCategories/{id}`  -remove a canned Messages Category
    
### Canned Message Category Json Format
Canned Message Category is represented as simple flat JSON objects with the following keys:  
     
|name     | Type               | Read-only    | Mandatory      |  Description                                                                                                   
| ------------- |--------------------- | ---------- | -------------------- | ------------------
|id |integer  | yes  | no |id of the canned message category.
|name|string  | no  | yes |name of the canned message category.
|parentCategoryId|integer  | no  | yes | id of the parent category of the canned message category
|parentCategoryName|string  | no  | no |name of the parent category of the canned message category
|isPrivate|string  | no  | yes | whether the canned message category is private or not.
    
### Get list of canned message categories
- End Point       
  `GET /api/v1/livechat/cannedMessageCategories`
    
- Parameters     
  No parameters
    
- Response      
 An array of Canned Message Category Json Object.
    
### Get a single canned message category
- End Point    
  `GET /api/v1/livechat/cannedMessageCategories/{id}`
    
- Parameters     
  No parameters
    
- Response      
Canned Message Category Json Object.
    
### Create a new canned message category
- End Point    
  `POST /api/v1/livechat/cannedMessageCategories`
    
- Parameters     
Canned Message Category Json Object.
    
- Response      
Canned Message Category Json Object.
    
### Update a canned message category
- End Point    
  `PUT /api/v1/livechat/cannedMessageCategories/{id}`
    
- Parameters     
Canned Message Category Json Object.
    
- Response      
Canned Message Category Json Object.
    
### Remove a canned message category
- End Point    
  `DELETE /api/v1/livechat/cannedMessageCategories/{id}`
    
- Parameters     
  No parameters
    
- Response      
  Status: 200 OK   
    
## Department
  You need `Manage Settings` permission to manage department.
  + `GET /api/v1/livechat/departments` -get list of departments
  + `GET /api/v1/livechat/departments/{id}`  -get a single department
  + `POST /api/v1/livechat/departments` -create a new department
  + `PUT /api/v1/livechat/departments/{id}`  -update a department
  + `DELETE /api/v1/livechat/departments/{id}`  -remove a department
    
### Department Json Format
Department is represented as simple flat JSON objects with the following keys:  
     
|name     | Type               | Read-only    | Mandatory      |  Description                                                                                                   
| ------------- |--------------------- | ---------- | -------------------- | ------------------
|id |integer  | yes  | no |id of the department.
|name|string  | no  | yes |name of the department.
|description|string  | no  | no |description of the department.
|agents|array  | no  | no | an array of agent in the department.
|groups|array  | no  | no | an array of group in the department.
|allocationStratege|string  | no  | no | stratege of chat allocation,including `load banlancing` 、`round robin` and `capability weighted`.
|isLastChattedPreferred|boolean  | no  | no |whether last-chatted agent is prefer or not.
|backupDepartmentId|integer  | no  | no | id of back up department
|offlineMessageTo|string  | no  | no | object which mail offline messages of the department to,including `allAgents` and `emailAddresses`
|emailAddresses|string  | no  | no | the email addresses which mail offline messages of the department to
    
### Get list of departments 
- End Point    
  `GET /api/v1/livechat/departments`
    
- Parameters     
  No parameters
    
- Response      
An array of Department Json Object.
    
### Get a single department 
- End Point    
  `GET /api/v1/livechat/departments/{id}`
    
- Parameters     
  No parameters
    
- Response      
Department Json Object.
    
### Create a new department 
- End Point    
  `POST /api/v1/livechat/departments`
    
- Parameters     
Department Json Object.
     
- Response      
Department Json Object.
    
### Update a department 
- End Point    
  `PUT /api/v1/livechat/departments/{id}`
    
- Parameters     
Department Json Object.
    
- Response      
Department Json Object.
    
### Remove a department
- End Point    
  `DELETE /api/v1/livechat/departments/{id}`
    
- Parameters     
  No parameters
    
- Response      
  Status: 200 OK   
    
## Auto Allocation
You need `Manage Settings` permission to config auto allocation.
  + `GET /api/v1/livechat/autoAllocation` -Get settings of auto allocation.
  + `PUT /api/v1/livechat/autoAllocation`  -Update settings of auto allocation.
     
### Auto Allocation Json Format
Auto Allocation is represented as simple flat JSON objects with the following keys:  
     
|name     | Type               | Read-only    | Mandatory      |  Description                                                                                                   
| ------------- |--------------------- | ---------- | -------------------- | ------------------
|id |integer  | yes  | no |id of the auto allocation.
|isEnable|boolean  | no  | yes |whether the auto allocation is enable or not.
|allocationStratege|string  | no  | no | stratege of chat allocation,including `load banlancing` 、`round robin` and `capability weighted`, available when the `isEnableDepartment` is `false`.
|isLastChattedPreferred|boolean  | no  | no |whether last-chatted agent is prefer or not, available when the `isEnableDepartment` is `false`.
|isEnableAllocateWhenAudioVideo|boolean  | no  | no |whether auto allocate chats to agents who are having audio or video chats is enable or not.
     
### Get settings of auto allocation.
- End Point    
  `GET /api/v1/livechat/autoAllocation`
     
- Parameters     
  No parameters
     
- Response      
Auto Allocation Json Object.
     
### Update settings of auto allocation.
- End Point    
  `PUT /api/v1/livechat/autoAllocation`
     
- Parameters     
Auto Allocation Json Object.
     
- Response      
Auto Allocation Json Object.
     
## Custom Away Status
  You need `Manage Settings` permission to manage custom away status.
  + `GET /api/v1/livechat/customAwayStatus` -get list of custom away status
  + `GET /api/v1/livechat/customAwayStatus/{id}`  -get a single custom away status
  + `POST /api/v1/livechat/customAwayStatus` -create a new custom away status
  + `PUT /api/v1/livechat/customAwayStatus/{id}`  -update a custom away status
  + `DELETE /api/v1/livechat/customAwayStatus/{id}`  -remove a custom away status

### Custom Away Status Json Format
Custom Away Status is represented as simple flat JSON objects with the following keys:  
     
|name     | Type               | Read-only    | Mandatory      |  Description                                                                                                   
| ------------- |--------------------- | ---------- | -------------------- | ------------------
|id |integer  | yes  | no |id of the custom away status.
|name|string  | no  | yes |name of the custom away status.
|isVisible|boolean  | no  | no |whether the custom away status is visible or not.
|isSystem|boolean  | no  | no | whether the custom away status is system status or not.
     
### Get list of custom away status 
- End Point    
  `GET /api/v1/livechat/customAwayStatus`
     
- Parameters     
  No parameters
     
- Response      
An array of Custom Away Status Json Object.
     
### Get a single custom away status 
- End Point    
  `GET /api/v1/livechat/customAwayStatus/{id}`
     
- Parameters     
  No parameters
     
- Response      
  Custom Away Status Json Object.
     
### Create a new custom away status 
- End Point    
  `POST /api/v1/livechat/customAwayStatus`
     
- Parameters     
  Custom Away Status Json Object.
     
- Response      
Custom Away Status Json Object.
     
### Update a custom away status 
- End Point    
  `PUT /api/v1/livechat/customAwayStatus/{id}`
      
- Parameters     
Custom Away Status Json Object.
      
- Response      
Custom Away Status Json Object.
    
### Remove a custom away status 
- End Point    
  `DELETE /api/v1/livechat/customAwayStatus/{id}`
    
- Parameters     
  No parameters
    
- Response      
  Status: 200 OK   
    
## Ban
  You need `Manage Ban List` permission to manage ban list.
  + `GET /api/v1/livechat/bans` -get list of bans
  + `GET /api/v1/livechat/bans/{id}`  -get a single ban
  + `POST /api/v1/livechat/bans` -create a new ban
  + `PUT /api/v1/livechat/bans/{id}`  -update a ban
  + `DELETE /api/v1/livechat/bans/{id}`  -remove a ban

### Ban Json Format
Ban is represented as simple flat JSON objects with the following keys:  
     
|name     | Type               | Read-only    | Mandatory      |  Description                                                                                                   
| ------------- |--------------------- | ---------- | -------------------- | ------------------
|id |integer  | yes  | no |id of the ban.
|banType|string  | no  | yes |type of ban,including `visitorId`、`ip` and `ipArrange`.
|banValue1|string  | no  | yes | value of ban,it means `ip from` when `banType` is `ipArrange` 
|banValue2|string  | no  | no |ban end the ip ,available when the `banType` is `ipArrange`.
|comment|string  | no  | no | comment of the ban.
  
### Get list of bans
- End Point    
  `GET /api/v1/livechat/bans`

- Parameters     
  No parameters

- Response      
An array of Ban Json Object.

### Get a single ban
- End Point    
  `GET /api/v1/livechat/bans/{id}`

- Parameters     
  No parameters

- Response      
Ban Json Object.

### Create a new ban 
- End Point    
  `POST /api/v1/livechat/bans`

- Parameters     
Ban Json Object.

- Response      
Ban Json Object.

### Update a ban
- End Point    
  `PUT /api/v1/livechat/bans/{id}`

- Parameters     
Ban Json Object.

- Response      
Ban Json Object.

### Remove a ban
- End Point    
  `DELETE /api/v1/livechat/bans/{id}`

- Parameters     
  No parameters

- Response      
  Status: 200 OK   

## Conversion Action
  You need `Manage Settings` permission to manage conversion action.
  + `GET /api/v1/livechat/conversionsActions` -get list of visitor segments
  + `GET /api/v1/livechat/conversionsActions/{id}`  -get a visitor segment
  + `POST /api/v1/livechat/conversionsActions` -create a new visitor segment

### Conversion Action Json Format
Conversion Action is represented as simple flat JSON objects with the following keys:  
     
|name     | Type               | Read-only    | Mandatory      |  Description                                                                                                   
| ------------- |--------------------- | ---------- | -------------------- | ------------------
|id |integer  | yes  | no |id of the conversion action.
|name|string  | no  | yes |  name of the conversion action.
|isEnable|boolean  | no  | no | whether the conversion action is enable or not.
|type|string  | no  | no | type of the conversion action,including `url`、`customVariable` and `setByApi`.
|customVariable|string  | no  | no |  the name of the custom variable,available when `type` is `customVariable`.
|matchType|string  | no  | no |  match type of the conversion action,available when `type` is `customVariable` or `url`.
|matchValue|string  | no  | no |  match value of the conversion action,available when `type` is `customVariable` or `url`.
|isCaseSensitive|boolean  | no  | no |  whether the conversion action is case sensitive or not,available when `type` is `url`.
|isAssignValue|boolean  | no  | no |  whether a value is assigned for the conversion action or not.
|isValueOrCustomVariable|boolean  | no  | no |  whether the value for assigning to the conversion action is come from a assigned value or a custom variable,`true` means a assigned value.
|valueForAssigning|string  | no  | no |  the value assigned for the conversion action,available when `isAssignValue` is `true` and `isValueOrCustomVariable` is `true`.
|customVariableForAssigning|string  | no  | no |  the value come from the custom variable,available when `isAssignValue` is `true` and and `isValueOrCustomVariable` is `false`.

### Get list of conversion actions
- End Point    
  `GET /api/v1/livechat/conversionsActions`

- Parameters     
  No parameters

- Response      
An array of Conversion Action Json Object.

### Get a single conversion action
- End Point    
  `GET /api/v1/livechat/conversionsActions/{id}`

- Parameters     
  No parameters

- Response      
Conversion Action Json Object.

### Create a new conversion action
- End Point    
  `POST /api/v1/livechat/conversionsActions`

- Parameters     
Conversion Action Json Object.

- Response      
Conversion Action Json Object.

### Update a conversion action
- End Point    
  `PUT /api/v1/livechat/conversionsActions/{id}`

- Parameters     
Conversion Action Json Object.

- Response      
Conversion Action Json Object.

## Visitor Segmentation
  You need `Manage Settings` permission to manage visitor segmentation.
  + `GET /api/v1/livechat/visitorSegments` -get list of visitor segments
  + `GET /api/v1/livechat/visitorSegments/{id}`  -get a visitor segment
  + `POST /api/v1/livechat/visitorSegments` -create a new visitor segment
  + `PUT /api/v1/livechat/visitorSegments/{id}`  -update a visitor segment
  + `DELETE /api/v1/livechat/visitorSegments/{id}`  -remove a visitor segment

### Visitor Segmentation Json Format
Visitor Segmentation is represented as simple flat JSON objects with the following keys:  
     
|name     | Type               | Read-only    | Mandatory      |  Description                                                                                                   
| ------------- |--------------------- | ---------- | -------------------- | ------------------
|id |integer  | yes  | no |id of the visitor segment.
|name|string  | no  | yes | name of the visitor segment.
|color|string  | no  | no | color of the visitor segment
|isEnable|boolean  | no  | no | whether the visitor segment is enable or not.
|priority|string  | no  | no | priority of the visitor segment.
|description|string  | no  | no |  description of the visitor segment.
|triggerCondition|[triggerCondition](#trigger-condition)  | no  | no| an trigger condition json object.
|notificationType|string  | no  | no |  type of notification, including `departments`、`agents` and `none`. 
|notifyObjects|array  | no  | no |  an array of notify object,the object contains id and name.

### Get list of visitor segments
- End Point    
  `GET /api/v1/livechat/visitorSegments`

- Parameters     
  No parameters

- Response      
An array of Visitor Segmentation Json Object.

### Get a single visitor segment
- End Point    
  `GET /api/v1/livechat/visitorSegments/{id}`

- Parameters     
  No parameters

- Response      
Visitor Segmentation Json Object.

### Create a new visitor segment 
- End Point    
  `POST /api/v1/livechat/visitorSegments`

- Parameters     
Visitor Segmentation Json Object.

- Response      
Visitor Segmentation Json Object.

### Update a visitor segment
- End Point    
  `PUT /api/v1/livechat/visitorSegmentsbans/{id}`

- Parameters     
Visitor Segmentation Json Object.

- Response      
Visitor Segmentation Json Object.

### Remove a visitor segment
- End Point    
  `DELETE /api/v1/livechat/visitorSegments/{id}`

- Parameters     
  No parameters

- Response      
  Status: 200 OK   

## Visitor SSO Settings
  You need `Manage Settings` permission to setting sso for a site.
  + `GET /api/v1/livechat/visitorSSO` -Get sso settings of visitor
  + `PUT /api/v1/livechat/visitorSSO`  -Update configuration of visitor

### Data Mapping Json Format
Data Mapping is represented as simple flat JSON objects with the following keys:  
     
|name     | Type               | Read-only    | Mandatory      |  Description                                                                                                   
| ------------- |--------------------- | ---------- | -------------------- | ------------------
|id |integer  | yes  | no |id of the data mapping.
|userAttribute|string  | no  | yes | user attribute of the mapping.
|macro|string  | no  | yes | common 100 field correspond with the user attribute.

### SignIn Options Json Format
SignIn Options is represented as simple flat JSON objects with the following keys:  
     
|name     | Type               | Read-only    | Mandatory      |  Description                                                                                                   
| ------------- |--------------------- | ---------- | -------------------- | ------------------
|id |integer  | yes  | no |id of the options.
|campaignId |integer  | yes  | no |id of the campaign.
|signInType|string  | no  | no | type of the sign in,including `no`、`optional` and `required`.
|isSkipPrechat|boolean  | no  | no | whether the pre-chat form is skipped when visitors sign in, available when the `signInType` is not `no`.

### Visitor SSO Settings Json Format
Visitor SSO Settings is represented as simple flat JSON objects with the following keys:  
     
|name     | Type               | Read-only    | Mandatory      |  Description                                                                                                   
| ------------- |--------------------- | ---------- | -------------------- | ------------------
|id |integer  | yes  | no |id of the sso settings.
|siteId |integer  | yes  | no |id of the site which the visitor sso belongs to.
|isEnable|boolean  | no  | yes |  whether visitor sso is enable or not.
|signInUrl|string  | no  | no | url which visitor sign in
|vertificationCertificate|string  | no  | no | infomation of the Identity Provider Verification Certificate.
|certificateFileName|string  | no  | no |  file name of the certificate.
|dataMappings|array  | no  | no |  an array of [data mapping](#data-mapping-json-format) json object.
|signInOptions|array  | no  | no |  an array of [SignIn Options](#singin-options-json-format) json object.

### Get sso settings of visitor
- End Point    
  `GET /api/v1/livechat/visitorSSO`

- Parameters     
  No parameters

- Response      
Visitor SSO Settings Json Object.

### Update sso settings of visitor
- End Point    
  `PUT /api/v1/livechat/visitorSSO`

- Parameters     
  Visitor SSO Settings Json Object.

- Response      
Visitor SSO Settings Json Object.

## Site Config
  You need `Manage Settings` permission to config for a site.
  + `GET /api/v1/livechat/configs` -Get configuration for a site
  + `PUT /api/v1/livechat/configs`  -Update configuration of a site

### Site Config Json Format
Site Config is represented as simple flat JSON objects with the following keys:  
     
|name     | Type               | Read-only    | Mandatory      |  Description                                                                                                   
| ------------- |--------------------- | ---------- | -------------------- | ------------------
|siteId |integer  | yes  | no |id of the site which the configuration belongs to.
|isEnableMultipleCampaigns| boolean  | no  | no |  whether multiple campaigns are enable or not in the site.
|isEnableAutoAllocation| boolean  | no  | no | whether auto allocation is enable or not in the site.
|isEnableCustomAwayStatus| boolean  | no  | no | whether custom away status is enable or not in the site.
|isEnableDepartment| boolean  | no  | no | whether department is enable or not in the site.
|isEnableAutoTranslation| boolean  | no  | no |  whether auto translation is enable or not in the site.
|isEnableAudioAndVideoChat| boolean  | no  | no |  whether audio&video chat is enable or not in the site.
|isEnableVisitorSegmentation| boolean  | no  | no |  whether visitor segmentation is enable or not in the site.
|isEnableVisitorSSO| boolean  | no  | no |  whether visitor SSO is enable or not in the site.
|isEnableCreditCardMasking| boolean  | no  | no |  whether Credit card masking is enable or not in the site.
|isEnableCustomVariables| boolean  | no  | no |  whether custom variables are enable or not in the site.
|isEnableSalesforce| boolean  | no  | no |  whether Salesforce integration is enable or not in the site.
|isEnableZendesk| boolean  | no  | no |  whether Zendesk integration is enable or not in the site.
|isEnableGoogleAnalytics| boolean  | no  | no |  whether Google Analytics integration is enable or not in the site.
|isEnableGotoMeeting| boolean  | no  | no |  whether GotoMeeting integration is enable or not in the site.
|isEnableJoinme| boolean  | no  | no |  whether Joinme integration is enable or not in the site.

### Get configurationuration for a site
- End Point    
  `GET /api/v1/livechat/configs`

- Parameters     
  No parameters

- Response      
Site Config Json Object.

### Update configuration of a site
- End Point    
  `PUT /api/v1/livechat/configs`

- Parameters     
Site Config Json Object.

- Response      
Site Config Json Object.

## Secure Form
  + `GET /api/v1/livechat/secureForms` -get list of secure forms
  + `GET /api/v1/livechat/secureForms/{id}`  -get a secure form
  + `POST /api/v1/livechat/secureForms` -create a new secure form
  + `PUT /api/v1/livechat/secureForms/{id}`  -update a secure form
  + `DELETE /api/v1/livechat/secureForms/{id}`  -remove a secure form

### Secure Form Json Format
Secure Form is represented as simple flat JSON objects with the following keys:  
     
|name     | Type               | Read-only    | Mandatory      |  Description                                                                                                   
| ------------- |--------------------- | ---------- | -------------------- | ------------------
|id |integer  | yes  | no |id of the secure form.
|name| string  | no  | yes |  name of the secure form.
|description| string  | no  | no |  description of the secure form.
|fields| Array | no | no |     an array of [field](#field) object

### Get list of secure forms
- End Point    
  `GET /api/v1/livechat/secureForms`

- Parameters     
  No parameters

- Response      
An array of Secure Form Json Object.

### Get a single secure form
- End Point    
  `GET /api/v1/livechat/secureForms/{id}`

- Parameters     
  No parameters

- Response      
Secure Form Json Object.

### Create a new secure form
- End Point    
  `POST /api/v1/livechat/secureForms`

- Parameters     
Secure Form Json Object.

- Response      
Secure Form Json Object.

### Update a secure form
- End Point    
  `PUT /api/v1/livechat/secureForms/{id}`

- Parameters     
Secure Form Json Object.
    
- Response      
Secure Form Json Object.

### Remove a secure form
- End Point    
  `DELETE /api/v1/livechat/secureForms/{id}`

- Parameters     
  No parameters

- Response      
  Status: 200 OK   

## Webhook
  + `GET /api/v1/livechat/webhooks` -Get list of webhooks
  + `POST /api/v1/livechat/webhooks` -Create a new webhook
  + `DELETE /api/v1/livechat/webhooks/{id}`  -Remove a webhook

### Webhook Json Format
Webhook is represented as simple flat JSON objects with the following keys:  
     
|name     | Type               | Read-only    | Mandatory      |  Description                                                                                                   
| ------------- |--------------------- | ---------- | -------------------- | ------------------
|id |integer  | yes  | no |id of the webhook.
|event| string  | no  | yes | event of webhook,including `offlineMessageSubmitted`、`chatStarted`、`chatEnded` and `chatWrapedUp`.
|targetUrl| string  | no  | yes |  target url of the webhook.

### Get list of webhooks
- End Point    
  `GET /api/v1/livechat/webhooks`

- Parameters     
  No parameters

- Response      
An array of Webhook Json Object.

### Create a new webhook
- End Point    
  `POST /api/v1/livechat/webhooks`

- Parameters     
Webhook Json Object.

- Response      
Webhook Json Object.

### Remove a webhook
- End Point    
  `DELETE /api/v1/livechat/webhooks/{id}`

- Parameters     
  No parameters

- Response      
  Status: 200 OK   

## Custom Variables
  + `GET /api/v1/livechat/customVariables` -Get list of custom variables
  + `POST /api/v1/livechat/customVariables` -Create a new custom variable
  + `PUT /api/v1/livechat/customVariables/{id}`  -Update a custom variable
  + `DELETE /api/v1/livechat/customVariables/{id}`  -Remove a custom variable

### Custom Variable Json Format
Custom Variable is represented as simple flat JSON objects with the following keys:  
     
|name     | Type               | Read-only    | Mandatory      |  Description                                                                                                   
| ------------- |--------------------- | ---------- | -------------------- | ------------------
|id |integer  | yes  | no |id of the custom variable.
|name| string  | no  | yes | name of the custom variable.
|type| string  | no  | yes | type of the custom variable.,including `text`、`integer` and `decimal`.
|value| string  | no  | nos | value of the custom variable.
|hyperlink| string  | no  | no |  hyperlink of the custom variable.

### Get list of Custom Variables
- End Point    
  `GET /api/v1/livechat/customVariables`

- Parameters     
  No parameters

- Response      
An array of Custom Variable Json Object.

### Create a new Custom Variable
- End Point    
  `POST /api/v1/livechat/customVariables`

- Parameters     
Custom Variable Json Object.

- Response      
Custom Variable Json Object.

### Update a Custom Variable
- End Point    
  `PUT /api/v1/livechat/customVariables/{id}`

- Parameters     
  Custom Variable Json Object.

- Response      
  Custom Variable Json Object.

### Remove a Custom Variable
- End Point    
  `DELETE /api/v1/livechat/customVariables/{id}`

- Parameters     
  No parameters

- Response      
  Status: 200 OK   

## Agent 
  - `GET /api/v1/livechat/agents/{id}` -Get agent info in livechat  
  - `PUT /api/v1/livechat/agents/{id}` -Update agent info in livechat

### Agent Json Format
 Agent is represented as simple flat JSON objects with the following keys:  

|name     | Type               | Read-only    | Mandatory      |  Description                                                                                                   
| ------------- |--------------------- | ---------- | -------------------- | ------------------ 
|id | integer  | yes  | yes|id of the agent.
|status| string  | no  | no| status of the agent, including online、away、offline
|ongoingChats| string  | yes  | no| total number of ongoing chats the agent has
|departments| array  | yes  | no| an array of department json object
|maxChatsCount| integer  | no  | no| the maximum number of concurrent chats that will be automatically routed to the agent when Auto Accept Chat Requests is enabled

### Get agent info in livechat  
- End Point    
  `GET /api/v1/livechat/agents/{id}`

- Parameters     
  No parameters

- Response      
  Agent Json Object.

### Update agent info in livechat
- End Point    
  `PUT /api/v1/livechat/agents/{id}`

- Parameters     
  Agent Json Object.

- Response      
  Agent Json Object.

## Chat
  + `Get /api/v1/livechat/chats` -Get chats list.
  + `Get /api/v1/livechat/chats/{chat_id}` -Get a single chat.
  + `Get /api/v1/livechat/chats/missedAndRefused` -Get missed and refused chats list.
  + `Get /api/v1/livechat/chats/agentChats` -Get agents' chats list.

### Custom Field Json Format
 Custom field is represented as simple flat JSON objects with the following keys:  

|name     | Type               | Read-only    | Mandatory      |  Description                                                                                                   
| ------------- |--------------------- | ---------- | -------------------- | ------------------ 
|id | integer  | yes  | no|id of the custom field.
|name| string | no  | yes| |name of the custom field.
|value| string | no  | no| |value of the custom field.

### Custom Variable Json Format
 Custom field is represented as simple flat JSON objects with the following keys:  

|name     | Type               | Read-only    | Mandatory      |  Description                                                                                                   
| ------------- |--------------------- | ---------- | -------------------- | ------------------ 
|id | integer  | yes  | no|id of the custom variable.
|name| string | no  | yes| |name of the custom variable.
|value| string | no  | no| |value of the custom variable.

## Attachment Json Foramt
 Attachment is represented as simple flat JSON objects with the following keys:  

|name     | Type               | Read-only    | Mandatory      |  Description                                                                                                   
| ------------- |--------------------- | ---------- | -------------------- | ------------------ 
|id | integer  | yes  | no|id of the attachment.
|name| string | no  | yes| |name of the attachment.
|uri| string | no  | no| |uri of the attachment.

### Chat Json Format 
 Chat is represented as simple flat JSON objects with the following keys:  

|name     | Type               | Read-only    | Mandatory      |  Description                                                                                                   
| ------------- |--------------------- | ---------- | -------------------- | ------------------ 
|id | integer  | yes  | yes|id of the chat.
|ssoUserId| integer | yes  | no| |user id of sso.
|summary| string | no  | no| |summary of the chat.
|category| string | no  | no| | the category which the chat belongs to, including `inquiry`、`suggestion` 、`complaint` and `junk`.
|name| string | no  | no| | name of the visitor
|email| string | no  | no| | email of the visitor
|phone| string | no  | no| | phone of the visitor
|productService| string | no  | no| | product/service the visitor selected in the pre-chat window. Agent can also update the value while chatting with visitors.
|department| string | no  | no| | department the visitor selected in the pre-chat window. Agent can also update the value while chatting with visitors.
|agents| string | no  | no| | agent who participate in the chat, separated by comma
|customFields| Array | no  | no| | values of custom fields entered by visitors in the pre-chat window. An array of [Custom Field](#custom-field-json-format).
|customVariable| Array | no  | no| | information of custom variables captured from the web page visitors viewed. An array of [Custom Variable](#custom-variable-json-format).
|startTime| string | no  | no| | time when the chat started
|waitingTime| string | no  | no| | amount of time a visitor has been waiting before his/her chat request was accepted
|endTime| string | no  | no| | time when the chat ended
|chatTranscript| string | no  | no| | content of the chat
|attachments| Array | no  | no| | files the operator send to the visitor or vice versa as well as the screenshots sent to the operator by the visitor through Comm100 Screen Capture. An array of [Attachment Json](#attachment-json-foramt)
|rating| string | no  | no| | rating on the Agent submitted by the visitor
|ratingComment| string | no  | no| | comment on Agent's customer service submitted by the visitor
|operatorComment| string | no  | no| | notes added for this chat by the operator

### Get chats list
- End Point      
  `Get /api/v1/livechat/chats`

- Parameters     
  - `dateInterval` - the date interval of the chat.
  optional：
  - `agentId` - id of the agent who participate in the chat.
  - `departmentId` - id of the department which the chat belongs to.
  - `category` - the category which the chat belongs to, including `inquiry`、`suggestion` 、`complaint` and `junk`.
  - `keywords` - the key words of inquiring the chat
  - `conditions` - the condition list of inquiring the chat
    + `fieldName` - field name of the condition.
    + `match` - match expression of the condition.
    + `value` - the value correspond with the field
  - `pageIndex` -the page index of query.

- Response      
  - `total` -total count of the list.
  - `previousPage` -url of the previous page.
  - `nextPage` -url of the next page.
  - `chats` - an array of [Chat](#chat-json-format)

### Get a single chat
- End Point      
  `Get /api/v1/livechat/chats/{id}`

- Parameters     
  No parameter.

- Response      
  Chat Json Object

### Get missed and refused chats list
- End Point      
  `Get /api/v1/livechat/chats/missedAndRefused`

- Parameters     
  - `dateInterval` - the date interval of the message.
  optional：
  - `type` - type of the chat,including `missed` and `refused`.
  - `campaignId` - id of the campaign which the message of the chat happened in.
  - `visitorSegmentId` - id of the visitor segment which visitor belongs to.
  - `pageIndex` -the page index of query.

- Response      
  - `total` -total count of the list.
  - `previousPage` -url of the previous page.
  - `nextPage` -url of the next page.
  - `messages` -messages list
    + `id` - id of the chat.
    + `type` - type of the chat,including `missed` and `refused`.
    + `time` -time when the chat happened.
    + `ssoUserId` -user id of sso.
    + `visitorName` -name of the visitor.
    + `visitorEmail` -email of the visitor.
    + `agents` -name of agents who participate in the chat.
    + `waitingTime` -wait time of the chat.
    + `comment` -comment of the chat.

### Agent chats list
- End Point      
  `Get /api/v1/livechat/chats/agentChats`

- Parameters     
  - `dateInterval` - the date interval of the message.
  optional：
  - `agentId` - id of the agent who paticipate in the chat.
  - `keywords` - the key words of inquiring the chat
  - `pageIndex` -the page index of query.

- Response      
  - `total` -total count of the list.
  - `previousPage` -url of the previous page.
  - `nextPage` -url of the next page.
  - `messages` -messages list
    + `agentFrom` - name of the agent from who send the meesage.
    + `agentTo` - name of the agent from who received the meesage.
    + `summary` -summary of the chat.

## Message
  + `Get /api/v1/livechat/messages` -Get messages list.

### Get messages list
- End Point      
  `Get /api/v1/livechat/messages` 

- Parameters     
  - `dateInterval` - the date interval of the message.
  optional：
  - `campaignId` - id of the campaign which the message of the chat happened in
  - `agentId` - id of the agent who participate in the chat.
  - `visitorSegmentId` - id of the visitor segment which visitor belongs to.
  - `keywords` - the key words of inquiring the message.
  - `pageIndex` -the page index of query.

- Response      
  - `total` -total count of the list.
  - `previousPage` -url of the previous page.
  - `nextPage` -url of the next page.
  - `messages` -messages list
    + `id` - id of the chat which the message belongs to.
    + `time` -time when the chat happened.
    + `ssoUserId` -user id of sso.
    + `visitorName` -name of the visitor.
    + `visitorEmail` -email of the visitor.
    + `agents` -name of agents who participate in the chat.
    + `content` -content of the message.