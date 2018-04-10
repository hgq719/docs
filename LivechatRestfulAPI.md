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
| [Secure Forms](#secure-forms) |/livechat/secureForms                    | 1
| [Chats History](#chats-history) |/livechat/chatsHistories                    | 1
| [Messages History](#messages-history) |/livechat/messagesHistories                    | 1
| [Missed& Refused History](#missed-refused-history) |/livechat/MissedAndRefusedHistories                    | 1
| [Agent Chats History](#agent-chats-history) |/livechat/agentChatsHistories                    | 1
| [MaximumOn Logs](#maximumon-logs) |/livechat/maximumonLogs                    | 1
      
## Campaign
  You need `Manage Campaigns` permission to manage campaigns and customize the settings for a campaigns.
  - `Campaigns` -Campaigns Manage
    + `GET /api/v1/livechat/campaigns` -Get list of campaigns
    + `POST /api/v1/livechat/campaigns` -Create a new campaign
    + `PUT /api/v1/livechat/campaigns/{id}` -Update a campaign
    + `DELETE /api/v1/livechat/campaigns/{id}` -Remove a campaign
  - `Campaign Settings` --setting of campaign
    + `GET /api/v1/livechat/campaigns/{id}/installationCode` -Get installation code for a campaign
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

## Get list of campaigns
### End Point
  `GET /api/v1/livechat/campaigns`

### Parameters
  No parameters

### Response
  Campaign list, including
  - `id ` -id of the campaign.
  - `name` -name of the campaign.
  - `description` -description of the campaign.

## Create a new campaign
### End Point
  `POST /api/v1/livechat/campaigns`

### Parameters
  - `name` -name of the campaign.
  - `description` -description of the campaign.

### Response
  - `id ` -id of the campaign.
  - `name` -name of the campaign.
  - `description` -description of the campaign.

## Update a campaign
### End Point
  `PUT /api/v1/livechat/campaigns/{id}`

### Parameters
  - `name` -name of the campaign.
  - `description` -description of the campaign.

### Response
  - `id ` -id of the campaign.
  - `name` -name of the campaign.
  - `description` -description of the campaign.

## Remove a campaign 
### End Point
  `DELETE /api/v1/livechat/campaigns/{id}`

### Parameters
  No parameters.

### Response
  - `result ` -the result of operating

## Get installation code for a campaign
### End Point
  `GET /api/v1/livechat/campaigns/{id}/installationCode`

### Parameters
  No parameters

### Response
  - `code` -installation code for the campaign.

## Get settings of ChatButton for a campaign
### End Point
  `GET /api/v1/livechat/campaigns/{id}/chatButton`

### Parameters
  No parameters

### Response
  - `buttonType ` -type of the button,including `adaptive`、`image` and `textLink`.
  - `isHideOffline` -whether the chatButton is visible when no agent is online.`true` means that button is invisible.
  - `isEnableDomainRestriction` -whether the domain restriction is enable
  - `allowedDomains` -display the chat button on specified domains/URLs only.
  Optional:  
  - `adaptiveSettings` - settings when `buttonType` is `adaptive`
    + `themeColor` - the theme color of chatbutton
    + `icon` - icon of the chat button
  - `imageSettings` -settings when `buttonType` is `image`
    + `imageType` - the type of the image ,including `gallery` and `upload`
    + `onlineImageId` - id of the image when any agents are on line
    + `offlineImageId` - id of the image when no agent is on line
    + `onlineImageUrl` - url of the image when any agents are on line
    + `offlineImageUrl` - url of the image when no agent is on line
    + `isFloat` -whether the chat button is float
    + `buttonXIsPixels` - whether the unit of coordinate x the button is pixel or percent, `true` means pixel and `false` means percent.
    + `buttonX` -coordinate x of the button,the unit acoording to `buttonXIsPixels`
    + `buttonYIsPixels`- whether the unit of coordinate Y the button is pixel or percent, `true` means pixel and `false` means percent.
    + `buttonY` -coordinate y of the button,the unit acoording to `buttonYIsPixels`
    + `buttonPosition` - position of the chat button,including `centered`、`topLeft`、`topMiddle`、`topRight`、`buttomLeft`、`buttomMiddle`、`buttomRight`、`leftMiddle` and `rightMiddle`.
    + `mobileButtonType` -the type of button on mobile device,including `text` and `image`.
    + `mobileOnlineText` -the content of text on mobile device when any agents are on line,available when `mobileButtonType` is `text`.
    + `mobileOfflineText` -the content of text on mobile device when no agent is on line,available when `mobileButtonType` is `text`.
    + `mobileThemeColor` - the theme color of chatbutton on mobile device,available when `mobileButtonType` is `text`.
    + `mobileOnlineImageUrl` -the url of image on mobile device when any agents are on line,available when `mobileButtonType` is `image`.
    + `mobileOfflineImageUrl` -the url of image on mobile device when no agent is on line,available when `mobileButtonType` is `image`.
    + `mobileImagePosition` - position of the chat button on mobile device， including `bottomLeft`、`bottomMiddle`、`bottomRight`、`leftMiddle`、`RightMiddle`、`leftBottom` and `rightBottom`,available when `mobileButtonType` is `image`.
  - `textLinkSettings` -settings when `buttonType` is `textLink`
    + `buttonText` -the content of the text link

## Update settings of ChatButton for a campaign
### End Point
  `PUT /api/v1/livechat/campaigns/{id}/chatButton`

### Parameters
  Required parameters: 
  - `buttonType ` -type of the button,including `adaptive`、`image` and `textLink`.
  Optional parameters:    
  + `isHideOffline` -whether the chatButton is visible when no agent is online.`true` means that button is invisible.
  + `isEnableDomainRestriction` -whether the domain restriction is enable
  + `allowedDomains` -display the chat button on specified domains/URLs only.  
  + `themeColor` - the theme color of chatbutton
  + `icon` - icon of the chat button
  + `imageType` - the type of the image ,including `gallery` and `upload`
  + `onlineImageId` - id of the image when any agents are on line
  + `offlineImageId` - id of the image when no agent is on line
  + `onlineImageUrl` - url of the image when any agents are on line
  + `offlineImageUrl` - url of the image when no agent is on line
  + `isFloat` -whether the chat button is float
  + `buttonXIsPixels` - whether the unit of coordinate x the button is pixel or percent, `true` means pixel and `false` means percent.
  + `buttonX` -coordinate x the button,the unit acoording to `buttonXIsPixels`
  + `buttonYIsPixels`- whether the unit of coordinate Y the button is pixel or percent, `true` means pixel and `false` means percent.
  + `buttonY` -coordinate y the button,the unit acoording to `buttonYIsPixels`
  + `buttonPosition` - position of the chat button,including `centered`、`topLeft`、`topMiddle`、`topRight`、`buttomLeft`、`buttomMiddle`、`buttomRight`、`leftMiddle`  and `rightMiddle`.
  + `mobileButtonType` -the type of button on mobile device,including `text` and `image`.
    + `mobileOnlineText` -the content of text on mobile device when any agents are on line,available when `mobileButtonType` is `text`.
    + `mobileOfflineText` -the content of text on mobile device when no agent is on line,available when `mobileButtonType` is `text`.
    + `mobileThemeColor` - the theme color of chatbutton on mobile device,available when `mobileButtonType` is `text`.
    + `mobileOnlineImageUrl` -the url of image on mobile device when any agents are on line,available when `mobileButtonType` is `image`.
    + `mobileOfflineImageUrl` -the url of image on mobile device when no agent is on line,available when `mobileButtonType` is `image`.
    + `mobileImagePosition` - position of the chat button on mobile device， including `bottomLeft`、`bottomMiddle`、`bottomRight`、`leftMiddle`、`RightMiddle`、`leftBottom` and `rightBottom`,available when `mobileButtonType` is `image`.
  + `buttonText` -the content of the text link

### Response
  - `buttonType ` -type of the button,including `adaptive`、`image` and `textLink`.
  - `isHideOffline` -whether the chatButton is visible when no agent is online.`true` means that button is invisible.
  - `isEnableDomainRestriction` -whether the domain restriction is enable
  - `allowedDomains` -display the chat button on specified domains/URLs only.
  Optional:  
  - `adaptiveSettings` - settings when `buttonType` is `adaptive`
    + `themeColor` - the theme color of chatbutton
    + `icon` - icon of the chat button
  - `imageSettings` -settings when `buttonType` is `image`
    + `imageType` - the type of the image ,including `gallery` and `upload`
    + `onlineImageId` - id of the image when any agents are on line
    + `offlineImageId` - id of the image when no agent is on line
    + `onlineImageUrl` - url of the image when any agents are on line
    + `offlineImageUrl` - url of the image when no agent is on line
    + `isFloat` -whether the chat button is float
    + `buttonXIsPixels` - whether the unit of coordinate x the button is pixel or percent, `true` means pixel and `false` means percent.
    + `buttonX` -coordinate x the button,the unit acoording to `buttonXIsPixels`
    + `buttonYIsPixels`- whether the unit of coordinate Y the button is pixel or percent, `true` means pixel and `false` means percent.
    + `buttonY` -coordinate y the button,the unit acoording to `buttonYIsPixels`
    + `buttonPosition` - position of the chat button,including `centered`、`topLeft`、`topMiddle`、`topRight`、`buttomLeft`、`buttomMiddle`、`buttomRight`、`leftMiddle` and `rightMiddle`.
    + `mobileButtonType` -the type of button on mobile device,including `text` and `image`.
    + `mobileOnlineText` -the content of text on mobile device when any agents are on line,available when `mobileButtonType` is `text`.
    + `mobileOfflineText` -the content of text on mobile device when no agent is on line,available when `mobileButtonType` is `text`.
    + `mobileThemeColor` - the theme color of chatbutton on mobile device,available when `mobileButtonType` is `text`.
    + `mobileOnlineImageUrl` -the url of image on mobile device when any agents are on line,available when `mobileButtonType` is `image`.
    + `mobileOfflineImageUrl` -the url of image on mobile device when no agent is on line,available when `mobileButtonType` is `image`.
    + `mobileImagePosition` - position of the chat button on mobile device， including `bottomLeft`、`bottomMiddle`、`bottomRight`、`leftMiddle`、`RightMiddle`、`leftBottom` and `rightBottom`,available when `mobileButtonType` is `image`.
  - `textLinkSettings` -settings when `buttonType` is `textLink`
    + `buttonText` -the content of the text link


## Get settings of ChatWindow for a campaign
### End Point
  `GET /api/v1/livechat/campaigns/{id}/chatWindow`

### Parameters
  No parameters

### Response
  - `themeType` -type of the window's theme,including `classic`、`simple` and `bubble`.
  - `themecolor` -color of the window's theme.
  - `windowType` - type of the chat window,including `embedded` and `popup`.
  - `windowtitle` - title of the chat window.
  - `isCanPrintChatDetail` -whether the print button is visible or not.
  - `isShowEmail` -whether the email button is visible or not.
  - `isUseOperatorEmailOrFromEmail` -set email from address
  - `fromEmail_email` - set email from email address.
  - `fromEmail_name` - set emial from email name
  - `isCanSwitchToOffline` -allow visitors to switch to Offline Message Window while waiting for chat.
  - `isCanSendFile` - whether the agent can send file or not.
  - `isCanHaveAudioChat` -whether the agent can use audio chat.
  - `isCanHaveVideoChat` -whether the agent can use video chat.
  - `isEndChatWhenVisitorInactivity` -automatically end chats if visitors don't respond.
  - `timeEndChatDelayWhenVisitorInactivity` -the time after the chat was end when visitor inactivity.
  - `isEnableSendTranscriptEmail` -whether the agent can send transcript email after chat ending.
  - `sendTranscriptEmailAddress` -the email address for sending transcript email.
  - `sendTranscriptEmailSubject` -the subject address for sending transcript email.
  - `greetingMessage` -the content of greeting message.
  - `isEnableCustomJS` -whether the agent can add custom js to chat window or not.
  - `customJS` -the content of custom javascript.
  - `headerType` - type of the header,including `agentInfo`、`bannerImage` and `avatarAndCompanyLogo`.
  - `isShowDisplayName` - whether the display name of the agent is visible or not. 
  - `isShowAvatar` - whether the avatar of the agent is visible or not.
  - `isShowTitle` -  whether the title of the agent is visible or not.
  - `isShowBio` -  whether the bio of the agent is visible or not.
  - `imageType` - the type of the image ,including `gallery` and `upload`
  - `imageId` - id of the image in the header of chat window.
  - `imageUrl` - url of the image in the header of chat window.
  - `isShowAvatar` - whether the avatar of the agent is visible or not.
  - `isShowLogo` - whether the logo of the company is visible or not.
  - `companyImageId` - id of the company image in the header of chat window.
  - `companyImageUrl` - url of the company image in the header of chat window.
  - `isShowAvatarWithMessage` - whether the avatar of the agent is visible or not in the messsage body.
  - `isShowTextureWithMessage` - whether the texture and picture of the background is visible or not in the messsage body.
  - `backgroudImageId` - id of the background image in the message body.
  - `backgroudImageUrl` - url of the company image in the message body.
  - `customCSS` - the content of custom css.

## Update settings of ChatWindow for a campaign
### End Point
  `PUT /api/v1/livechat/campaigns/{id}/chatWindow`

### Parameters
    - `themeType` -type of the window's theme,including `classic`、`simple` and `bubble`.
  - `themecolor` -color of the window's theme.
  - `windowType` - type of the chat window,including `embedded` and `popup`.
  - `windowtitle` - title of the chat window.
  - `isCanPrintChatDetail` -whether the print button is visible or not.
  - `isShowEmail` -whether the email button is visible or not.
  - `isUseOperatorEmailOrFromEmail` -set email from address
  - `fromEmail_email` - set email from email address.
  - `fromEmail_name` - set emial from email name
  - `isCanSwitchToOffline` -allow visitors to switch to Offline Message Window while waiting for chat.
  - `isCanSendFile` - whether the agent can send file or not.
  - `isCanHaveAudioChat` -whether the agent can use audio chat.
  - `isCanHaveVideoChat` -whether the agent can use video chat.
  - `isEndChatWhenVisitorInactivity` -automatically end chats if visitors don't respond.
  - `timeEndChatDelayWhenVisitorInactivity` -the time after the chat was end when visitor inactivity.
  - `isEnableSendTranscriptEmail` -whether the agent can send transcript email after chat ending.
  - `sendTranscriptEmailAddress` -the email address for sending transcript email.
  - `sendTranscriptEmailSubject` -the subject address for sending transcript email.
  - `greetingMessage` -the content of greeting message.
  - `isEnableCustomJS` -whether the agent can add custom js to chat window or not.
  - `customJS` -the content of custom javascript.
  Optional:  
  - `headerType` - type of the header,including `agentInfo`、`bannerImage` and `avatarAndCompanyLogo`.
  - `isShowDisplayName` - whether the display name of the agent is visible or not. 
  - `isShowAvatar` - whether the avatar of the agent is visible or not.
  - `isShowTitle` -  whether the title of the agent is visible or not.
  - `isShowBio` -  whether the bio of the agent is visible or not.
  - `imageType` - the type of the image ,including `gallery` and `upload`
  - `imageId` - id of the image in the header of chat window.
  - `imageUrl` - url of the image in the header of chat window.
  - `isShowAvatar` - whether the avatar of the agent is visible or not.
  - `isShowLogo` - whether the logo of the company is visible or not.
  - `companyImageId` - id of the company image in the header of chat window.
  - `companyImageUrl` - url of the company image in the header of chat window.
  - `isShowAvatarWithMessage` - whether the avatar of the agent is visible or not in the messsage body.
  - `isShowTextureWithMessage` - whether the texture and picture of the background is visible or not in the messsage body.
  - `backgroudImageId` - id of the background image in the message body.
  - `backgroudImageUrl` - url of the company image in the message body.
  - `customCSS` - the content of custom css.

### Response
    - `themeType` -type of the window's theme,including `classic`、`simple` and `bubble`.
  - `themecolor` -color of the window's theme.
  - `windowType` - type of the chat window,including `embedded` and `popup`.
  - `windowtitle` - title of the chat window.
  - `isCanPrintChatDetail` -whether the print button is visible or not.
  - `isShowEmail` -whether the email button is visible or not.
  - `isUseOperatorEmailOrFromEmail` -set email from address
  - `fromEmail_email` - set email from email address.
  - `fromEmail_name` - set emial from email name
  - `isCanSwitchToOffline` -allow visitors to switch to Offline Message Window while waiting for chat.
  - `isCanSendFile` - whether the agent can send file or not.
  - `isCanHaveAudioChat` -whether the agent can use audio chat.
  - `isCanHaveVideoChat` -whether the agent can use video chat.
  - `isEndChatWhenVisitorInactivity` -automatically end chats if visitors don't respond.
  - `timeEndChatDelayWhenVisitorInactivity` -the time after the chat was end when visitor inactivity.
  - `isEnableSendTranscriptEmail` -whether the agent can send transcript email after chat ending.
  - `sendTranscriptEmailAddress` -the email address for sending transcript email.
  - `sendTranscriptEmailSubject` -the subject address for sending transcript email.
  - `greetingMessage` -the content of greeting message.
  - `isEnableCustomJS` -whether the agent can add custom js to chat window or not.
  - `customJS` -the content of custom javascript.
  - `headerType` - type of the header,including `agentInfo`、`bannerImage` and `avatarAndCompanyLogo`.
  - `isShowDisplayName` - whether the display name of the agent is visible or not. 
  - `isShowAvatar` - whether the avatar of the agent is visible or not.
  - `isShowTitle` -  whether the title of the agent is visible or not.
  - `isShowBio` -  whether the bio of the agent is visible or not.
  - `imageType` - the type of the image ,including `gallery` and `upload`
  - `imageId` - id of the image in the header of chat window.
  - `imageUrl` - url of the image in the header of chat window.
  - `isShowAvatar` - whether the avatar of the agent is visible or not.
  - `isShowLogo` - whether the logo of the company is visible or not.
  - `companyImageId` - id of the company image in the header of chat window.
  - `companyImageUrl` - url of the company image in the header of chat window.
  - `isShowAvatarWithMessage` - whether the avatar of the agent is visible or not in the messsage body.
  - `isShowTextureWithMessage` - whether the texture and picture of the background is visible or not in the messsage body.
  - `backgroudImageId` - id of the background image in the message body.
  - `backgroudImageUrl` - url of the company image in the message body.
  - `customCSS` - the content of custom css.

## Update settings of PreChat for a campaign
### End Point
  `PUT /api/v1/livechat/campaigns/{id}/prechat`

### Parameters
  - `isEnable` -whether the pre-chat is enable or not.
  - `greetingMessage` - content of greeting message.
  - `isEnableGoogle` -whether google is enable or not in social login.
  - `isEnableFacebook` -whether facebook is enable or not in social login.
  - `isRememberForm` -whether visitor info is remembered or not from pre-chat form.
  - `fieldLayoutStyle` -the layout style of field.
  - `fields` - fields list
    + `id` - id of the field
    + `name` - name of the field
    + `type` - type of the field
      * `name` - Name field (system field)
      * `email` - Email field (system field)
      * `phone` - Phone field (system field)
      * `company` - Company field (system field)
      * `product` - Product and Service field (system field)
      * `department` - Department field (system field)
      * `ticket` - Ticket field (system field)
      * `rating` - Rating field (system field)
      * `comment` - Comment field (system field)
      * `subject` - Subject field (system field)
      * `content` - Content field (system field)
      * `attachment` - Attachment field (system field)
      * `text` - Text field (custom field)
      * `textarea` - Textarea field (custom field)
      * `radio` - Radio Box field (custom field)
      * `checkbox` - Check Box field (custom field)
      * `select` - Drop Down List field (custom field)
      * `checkboxList` - Check Box List field (custom field)
    + `isSystem` - whether the field is system field or not.
    + `isVisible` - whether the field is visible or not in the pre-chat form.
    + `isRequired` - whether the field is required or not when submiting the form,including `vertical` and `horizontal`.
    + `options` - the options of the field, available when the `type` is not `department`.

### Response
  - `isEnable` -whether the pre-chat is enable or not.
  - `greetingMessage` - content of greeting message.
  - `isEnableGoogle` -whether google is enable or not in social login.
  - `isEnableFacebook` -whether facebook is enable or not in social login.
  - `isRememberForm` -whether visitor info is remembered or not from pre-chat form.
  - `fieldLayoutStyle` -the layout style of field.
  - `fields` - fields list
    + `id` - id of the field
    + `name` - name of the field
    + `type` - type of the field
    + `isSystem` - whether the field is system field or not.
    + `isVisible` - whether the field is visible or not in the pre-chat form.
    + `isRequired` - whether the field is required or not when submiting the form.
    + `options` - the options of the field

## Update settings of PostChat for a campaign
### End Point
  `PUT /api/v1/livechat/campaigns/{id}/postchat`

### Parameters
  - `isEnable` -whether the post-chat is enable or not.
  - `greetingMessage` - content of greeting message.
  - `isEnableGoogle` -whether google is enable or not in social login.
  - `isEnableFacebook` -whether facebook is enable or not in social login.
  - `isRememberForm` -whether visitor info is remembered or not from post-chat form.
  - `fieldLayoutStyle` -the layout style of field,including `labelLeftSideInput` and `labelAboveInput`
  - `fields` - fields list
    + `id` - id of the field
    + `name` - name of the field
    + `type` - type of the field
      * `name` - Name field (system field)
      * `email` - Email field (system field)
      * `phone` - Phone field (system field)
      * `company` - Company field (system field)
      * `product` - Product and Service field (system field)
      * `department` - Department field (system field)
      * `ticket` - Ticket field (system field)
      * `rating` - Rating field (system field)
      * `comment` - Comment field (system field)
      * `subject` - Subject field (system field)
      * `content` - Content field (system field)
      * `attachment` - Attachment field (system field)
      * `text` - Text field (custom field)
      * `textarea` - Textarea field (custom field)
      * `radio` - Radio Box field (custom field)
      * `checkbox` - Check Box field (custom field)
      * `select` - Drop Down List field (custom field)
      * `checkboxList` - Check Box List field (custom field)
    + `isSystem` - whether the field is system field or not.
    + `isVisible` - whether the field is visible or not.
    + `isRequired` - whether the field is required or not when submiting the form.
    + `options` - the options of the field

### Response
  - `isEnable` -whether the pre-chat is enable or not.
  - `greetingMessage` - content of greeting message.
  - `isEnableGoogle` -whether google is enable or not in social login.
  - `isEnableFacebook` -whether facebook is enable or not in social login.
  - `isRememberForm` -whether visitor info is remembered or not from post-chat form.
  - `fieldLayoutStyle` -the layout style of field.
  - `fields` - fields list
    + `id` - id of the field
    + `name` - name of the field
    + `type` - type of the field
    + `isSystem` - whether the field is system field or not.
    + `isVisible` - whether the field is visible or not.
    + `isRequired` - whether the field is required or not when submiting the form.
    + `options` - the options of the field

## Update settings of offline message for a campaign
### End Point
  `PUT /api/v1/livechat/campaigns/{id}/offlineMessage`

### Parameters
  - `isUseCustomOfflinePage` -whether the custom offline message page is used or not.
  - `greetingMessage` - content of greeting message.
  - `url` -url of custom offline message page.
  - `isOpenInNewWindow` -whether open page in a new window or not.
  - `isShowTeamName` - whether the name of the agent is visible or not in the header.
  - `isShowAvatar` - whether the avatar of the agent is visible or not in the header.
  - `fieldLayoutStyle` -the layout style of field,including `labelLeftSideInput` and `labelAboveInput`
  - `fields` - fields list
    + `id` - id of the field
    + `name` - name of the field
    + `type` - type of the field
      * `name` - Name field (system field)
      * `email` - Email field (system field)
      * `phone` - Phone field (system field)
      * `company` - Company field (system field)
      * `product` - Product and Service field (system field)
      * `department` - Department field (system field)
      * `ticket` - Ticket field (system field)
      * `rating` - Rating field (system field)
      * `comment` - Comment field (system field)
      * `subject` - Subject field (system field)
      * `content` - Content field (system field)
      * `attachment` - Attachment field (system field)
      * `text` - Text field (custom field)
      * `textarea` - Textarea field (custom field)
      * `radio` - Radio Box field (custom field)
      * `checkbox` - Check Box field (custom field)
      * `select` - Drop Down List field (custom field)
      * `checkboxList` - Check Box List field (custom field)
    + `isSystem` - whether the field is system field or not.
    + `isVisible` - whether the field is visible or not .
    + `isRequired` - whether the field is required or not when submiting the form.
    + `options` - the options of the field

### Response
  - `isUseCustomOfflinePage` -whether the custom offline message page is used or not.
  - `greetingMessage` - content of greeting message.
  - `customOfflinePage` -settings of custom offline message page.
    + `url` -url of custom offline message page.
    + `isOpenInNewWindow` -whether open page in a new window or not.
  - `isShowTeamName` - whether the name of the agent is visible or not in the header.
  - `isShowAvatar` - whether the avatar of the agent is visible or not in the header.
  - `fieldLayoutStyle` -the layout style of field.
  - `fields` - fields list
    + `id` - id of the field
    + `name` - name of the field
    + `type` - type of the field
    + `isSystem` - whether the field is system field or not.
    + `isVisible` - whether the field is visible or not .
    + `isRequired` - whether the field is required or not when submiting the form.
    + `options` - the options of the field

## Get settings of invitation for a campaign
### End Point
  `GET /api/v1/livechat/campaigns/{id}/invitation`

### Parameters
  No parameters

### Response
  - `autoInvitations` - auto invitation list.
    + `id` - id of auto invitation
    + `name` -name of auto invitation
    + `isEnable` - whether the auto invitation is enable or not.
  - `manualInvitationMessage` - content of manual invitation message.
  - `imageType` - the type of image source,including `gallery` or `upload`
  - `imageId` -id of invitation image.
  - `imageUrl` -url of invitation image.
  - `invitationPosition` - the position of invitation window,including `centered`、`centeredWithOverlay`、`topLeft`、`topMiddle`、`topRight`、`buttomLeft`、`buttomMiddle`、`buttomRight`、`leftMiddle` and `rightMiddle`.
  - `invitationXOffset` -coordinate x of the button,the unit acoording to `buttonXIsPixels`
  - `invitationYOffset` -coordinate y of the button,the unit acoording to `buttonYIsPixels`
  - `invitationXOffsetIfPixels` -whether the unit of coordinate x the button is pixel or percent, `true` means pixel and `false` means percent.
  - `invitationYOffsetIfPixels` - whether the unit of coordinate Y the button is pixel or percent, `true` means pixel and `false` means percent.
  - `textFont` - the font of text.
  - `textIsBold` - whether the text is bold or not.
  - `textSize` - the size of text.
  - `textIsItalic` - whether the text is italic or not.
  - `textColor` - the color of text.
  - `closeAreaXOffset` - coordinate x of the close area
  - `closeAreaYOffset` - coordinate y of the close area
  - `closeAreaWidth` - width of the close area
  - `closeAreaHeight` - height of the close area
  - `textAreaXOffset` - coordinate x of the text area
  - `textAreaYOffset` - coordinate y of the text area
  - `textAreaWidth` - width of the text area
  - `textAreaHeight` - height of the text area
  - `invitationStyle` -the layout style of invitation window,including `bubble`、`popup` and `chatWindow`.

## Update settings of invitation for a campaign
### End Point
  `PUT /api/v1/livechat/campaigns/{id}/invitation`

### Parameters
  optional:
  - `autoInvitations` - auto invitation list.
    + `id` - id of auto invitation
    + `isEnable` - whether the auto invitation is enable or not.
  - `manualInvitationMessage` - content of manual invitation message.
  - `imageType` - the type of image source,including `gallery` or `upload`
  - `imageId` -id of invitation image.
  - `imageUrl` -url of invitation image.
  - `invitationPosition` - the position of invitation window,including `centered`、`centeredWithOverlay`、`topLeft`、`topMiddle`、`topRight`、`buttomLeft`、`buttomMiddle`、`buttomRight`、`leftMiddle` and `rightMiddle`.
  - `invitationXOffset` -coordinate x of the button,the unit acoording to `buttonXIsPixels`
  - `invitationYOffset` -coordinate y of the button,the unit acoording to `buttonYIsPixels`
  - `invitationXOffsetIfPixels` -whether the unit of coordinate x the button is pixel or percent, `true` means pixel and `false` means percent.
  - `invitationYOffsetIfPixels` - whether the unit of coordinate Y the button is pixel or percent, `true` means pixel and `false` means percent.
  - `textFont` - the font of text.
  - `textIsBold` - whether the text is bold or not.
  - `textSize` - the size of text.
  - `textIsItalic` - whether the text is italic or not.
  - `textColor` - the color of text.
  - `closeAreaXOffset` - coordinate x of the close area
  - `closeAreaYOffset` - coordinate y of the close area
  - `closeAreaWidth` - width of the close area
  - `closeAreaHeight` - height of the close area
  - `textAreaXOffset` - coordinate x of the text area
  - `textAreaYOffset` - coordinate y of the text area
  - `textAreaWidth` - width of the text area
  - `textAreaHeight` - height of the text area
  - `invitationStyle` -the layout style of invitation window,including `bubble`、`popup` and `chatWindow`.

### Response
  - `autoInvitations` - auto invitation list.
    + `id` - id of auto invitation
    + `name` -name of auto invitation
    + `isEnable` - whether the auto invitation is enable or not.
  - `manualInvitationMessage` - content of manual invitation message.
  - `imageType` - the type of image source,including `gallery` or `upload`
  - `imageId` -id of invitation image.
  - `imageUrl` -url of invitation image.
  - `invitationPosition` - the position of invitation window,including `centered`、`centeredWithOverlay`、`topLeft`、`topMiddle`、`topRight`、`buttomLeft`、`buttomMiddle`、`buttomRight`、`leftMiddle` and `rightMiddle`.
  - `invitationXOffset` -coordinate x of the button,the unit acoording to `buttonXIsPixels`
  - `invitationYOffset` -coordinate y of the button,the unit acoording to `buttonYIsPixels`
  - `invitationXOffsetIfPixels` -whether the unit of coordinate x the button is pixel or percent, `true` means pixel and `false` means percent.
  - `invitationYOffsetIfPixels` - whether the unit of coordinate Y the button is pixel or percent, `true` means pixel and `false` means percent.
  - `textFont` - the font of text.
  - `textIsBold` - whether the text is bold or not.
  - `textSize` - the size of text.
  - `textIsItalic` - whether the text is italic or not.
  - `textColor` - the color of text.
  - `closeAreaXOffset` - coordinate x of the close area
  - `closeAreaYOffset` - coordinate y of the close area
  - `closeAreaWidth` - width of the close area
  - `closeAreaHeight` - height of the close area
  - `textAreaXOffset` - coordinate x of the text area
  - `textAreaYOffset` - coordinate y of the text area
  - `textAreaWidth` - width of the text area
  - `textAreaHeight` - height of the text area
  - `invitationStyle` -the layout style of invitation window,including `bubble`、`popup` and `chatWindow`.

## Get a autoInvitation for a campaign
### End Point
  `GET /api/v1/livechat/campaigns/{id}/invitation/autoInvitations/{autoInvitation_id}`

### Parameters
  No parameters

### Response
  - `id` -id of the auto invitation
  - `isEnable` - whether the auto invitation is enable or not.
  - `autoInvitationMessage` - content of auto invitation message.
  - `name` -name of the auto invitation
  - `imageType` - the type of image source,including `gallery` or `upload`
  - `imageId` -id of invitation image.
  - `imageUrl` -url of invitation image.
  - `invitationPosition` - the position of invitation window,including `centered`、`centeredWithOverlay`、`topLeft`、`topMiddle`、`topRight`、`buttomLeft`、`buttomMiddle`、`buttomRight`、`leftMiddle` and `rightMiddle`.
  - `invitationXOffset` -coordinate x of the button,the unit acoording to `buttonXIsPixels`
  - `invitationYOffset` -coordinate y of the button,the unit acoording to `buttonYIsPixels`
  - `invitationXOffsetIfPixels` -whether the unit of coordinate x the button is pixel or percent, `true` means pixel and `false` means percent.
  - `invitationYOffsetIfPixels` - whether the unit of coordinate Y the button is pixel or percent, `true` means pixel and `false` means percent.
  - `textFont` - the font of text.
  - `textIsBold` - whether the text is bold or not.
  - `textSize` - the size of text.
  - `textIsItalic` - whether the text is italic or not.
  - `textColor` - the color of text.
  - `closeAreaXOffset` - coordinate x of the close area
  - `closeAreaYOffset` - coordinate y of the close area
  - `closeAreaWidth` - width of the close area
  - `closeAreaHeight` - height of the close area
  - `textAreaXOffset` - coordinate x of the text area
  - `textAreaYOffset` - coordinate y of the text area
  - `textAreaWidth` - width of the text area
  - `textAreaHeight` - height of the text area
  - `isPopupOnlyOneTime` - pop up only one time during one visit
  - `triggeredWhen` - when the rule is triggered, including `all`、`any` and `logicalExpression` 
  - `logicalExpression` - the logical expression of the conditions
  - `conditions` -condition list
    + `variableName` - name of the variable,including comm100 system variable and custom variable
    + `expression` - expression of the condition
    + `value` - the value response to the variable

## Create a new auto invitation for a campaign
### End Point
  `POST /api/v1/livechat/campaigns/{id}/invitation/autoInvitations`

### Parameters
  - `isEnable` - whether the auto invitation is enable or not.
  - `autoInvitationMessage` - content of auto invitation message.
  - `name` -name of the auto invitation
  - `imageType` - the type of image source,including `gallery` or `upload`
  - `imageId` -id of invitation image.
  - `imageUrl` -url of invitation image.
  - `invitationPosition` - the position of invitation window,including `centered`、`centeredWithOverlay`、`topLeft`、`topMiddle`、`topRight`、`buttomLeft`、`buttomMiddle`、`buttomRight`、`leftMiddle` and `rightMiddle`.
  - `invitationXOffset` -coordinate x of the button,the unit acoording to `buttonXIsPixels`
  - `invitationYOffset` -coordinate y of the button,the unit acoording to `buttonYIsPixels`
  - `invitationXOffsetIfPixels` -whether the unit of coordinate x the button is pixel or percent, `true` means pixel and `false` means percent.
  - `invitationYOffsetIfPixels` - whether the unit of coordinate Y the button is pixel or percent, `true` means pixel and `false` means percent.
  - `textFont` - the font of text.
  - `textIsBold` - whether the text is bold or not.
  - `textSize` - the size of text.
  - `textIsItalic` - whether the text is italic or not.
  - `textColor` - the color of text.
  - `closeAreaXOffset` - coordinate x of the close area
  - `closeAreaYOffset` - coordinate y of the close area
  - `closeAreaWidth` - width of the close area
  - `closeAreaHeight` - height of the close area
  - `textAreaXOffset` - coordinate x of the text area
  - `textAreaYOffset` - coordinate y of the text area
  - `textAreaWidth` - width of the text area
  - `textAreaHeight` - height of the text area
  - `isPopupOnlyOneTime` - pop up only one time during one visit
  - `triggeredWhen` - when the rule is triggered, including `all`、`any` and `logicalExpression` 
  - `logicalExpression` - the logical expression of the conditions
  - `conditions` -condition list
    + `variableName` - name of the variable,including comm100 system variable and custom variable
    + `expression` - expression of the condition
    + `value` - the value response to the variable

### Response
  - `id` -id of the auto invitation
  - `isEnable` - whether the auto invitation is enable or not.
  - `autoInvitationMessage` - content of auto invitation message.
  - `name` -name of the auto invitation
  - `imageType` - the type of image source,including `gallery` or `upload`
  - `imageId` -id of invitation image.
  - `imageUrl` -url of invitation image.
  - `invitationPosition` - the position of invitation window,including `centered`、`centeredWithOverlay`、`topLeft`、`topMiddle`、`topRight`、`buttomLeft`、`buttomMiddle`、`buttomRight`、`leftMiddle` and `rightMiddle`.
  - `invitationXOffset` -coordinate x of the button,the unit acoording to `buttonXIsPixels`
  - `invitationYOffset` -coordinate y of the button,the unit acoording to `buttonYIsPixels`
  - `invitationXOffsetIfPixels` -whether the unit of coordinate x the button is pixel or percent, `true` means pixel and `false` means percent.
  - `invitationYOffsetIfPixels` - whether the unit of coordinate Y the button is pixel or percent, `true` means pixel and `false` means percent.
  - `textFont` - the font of text.
  - `textIsBold` - whether the text is bold or not.
  - `textSize` - the size of text.
  - `textIsItalic` - whether the text is italic or not.
  - `textColor` - the color of text.
  - `closeAreaXOffset` - coordinate x of the close area
  - `closeAreaYOffset` - coordinate y of the close area
  - `closeAreaWidth` - width of the close area
  - `closeAreaHeight` - height of the close area
  - `textAreaXOffset` - coordinate x of the text area
  - `textAreaYOffset` - coordinate y of the text area
  - `textAreaWidth` - width of the text area
  - `textAreaHeight` - height of the text area
  - `isPopupOnlyOneTime` - pop up only one time during one visit
  - `triggeredWhen` - when the rule is triggered, including `all`、`any` and `logicalExpression` 
  - `logicalExpression` - the logical expression of the conditions
  - `conditions` -condition list
    + `variableName` - name of the variable,including comm100 system variable and custom variable
    + `expression` - expression of the condition
    + `value` - the value response to the variable

## Update a auto invitation for a campaign
### End Point
  `PUT /api/v1/livechat/campaigns/{id}/invitation/autoInvitations/{autoInvitation_id}`

### Parameters
  - `isEnable` - whether the auto invitation is enable or not.
  - `autoInvitationMessage` - content of auto invitation message.
  - `name` -name of the auto invitation
  - `imageType` - the type of image source,including `gallery` or `upload`
  - `imageId` -id of invitation image.
  - `imageUrl` -url of invitation image.
  - `invitationPosition` - the position of invitation window,including `centered`、`centeredWithOverlay`、`topLeft`、`topMiddle`、`topRight`、`buttomLeft`、`buttomMiddle`、`buttomRight`、`leftMiddle` and `rightMiddle`.
  - `invitationXOffset` -coordinate x of the button,the unit acoording to `buttonXIsPixels`
  - `invitationYOffset` -coordinate y of the button,the unit acoording to `buttonYIsPixels`
  - `invitationXOffsetIfPixels` -whether the unit of coordinate x the button is pixel or percent, `true` means pixel and `false` means percent.
  - `invitationYOffsetIfPixels` - whether the unit of coordinate Y the button is pixel or percent, `true` means pixel and `false` means percent.
  - `textFont` - the font of text.
  - `textIsBold` - whether the text is bold or not.
  - `textSize` - the size of text.
  - `textIsItalic` - whether the text is italic or not.
  - `textColor` - the color of text.
  - `closeAreaXOffset` - coordinate x of the close area
  - `closeAreaYOffset` - coordinate y of the close area
  - `closeAreaWidth` - width of the close area
  - `closeAreaHeight` - height of the close area
  - `textAreaXOffset` - coordinate x of the text area
  - `textAreaYOffset` - coordinate y of the text area
  - `textAreaWidth` - width of the text area
  - `textAreaHeight` - height of the text area
  - `isPopupOnlyOneTime` - pop up only one time during one visit
  - `triggeredWhen` - when the rule is triggered, including `all`、`any` and `logicalExpression` 
  - `logicalExpression` - the logical expression of the conditions
  - `conditions` -condition list
    + `variableName` - name of the variable,including comm100 system variable and custom variable
    + `expression` - expression of the condition
    + `value` - the value response to the variable

### Response
  - `id` -id of the auto invitation
  - `isEnable` - whether the auto invitation is enable or not.
  - `autoInvitationMessage` - content of auto invitation message.
  - `name` -name of the auto invitation
  - `imageType` - the type of image source,including `gallery` or `upload`
  - `imageId` -id of invitation image.
  - `imageUrl` -url of invitation image.
  - `invitationPosition` - the position of invitation window,including `centered`、`centeredWithOverlay`、`topLeft`、`topMiddle`、`topRight`、`buttomLeft`、`buttomMiddle`、`buttomRight`、`leftMiddle` and `rightMiddle`.
  - `invitationXOffset` -coordinate x of the button,the unit acoording to `buttonXIsPixels`
  - `invitationYOffset` -coordinate y of the button,the unit acoording to `buttonYIsPixels`
  - `invitationXOffsetIfPixels` -whether the unit of coordinate x the button is pixel or percent, `true` means pixel and `false` means percent.
  - `invitationYOffsetIfPixels` - whether the unit of coordinate Y the button is pixel or percent, `true` means pixel and `false` means percent.
  - `textFont` - the font of text.
  - `textIsBold` - whether the text is bold or not.
  - `textSize` - the size of text.
  - `textIsItalic` - whether the text is italic or not.
  - `textColor` - the color of text.
  - `closeAreaXOffset` - coordinate x of the close area
  - `closeAreaYOffset` - coordinate y of the close area
  - `closeAreaWidth` - width of the close area
  - `closeAreaHeight` - height of the close area
  - `textAreaXOffset` - coordinate x of the text area
  - `textAreaYOffset` - coordinate y of the text area
  - `textAreaWidth` - width of the text area
  - `textAreaHeight` - height of the text area
  - `isPopupOnlyOneTime` - pop up only one time during one visit
  - `triggeredWhen` - when the rule is triggered, including `all`、`any` and `logicalExpression` 
  - `logicalExpression` - the logical expression of the conditions
  - `conditions` -condition list
    + `variableName` - name of the variable,including comm100 system variable and custom variable
    + `expression` - expression of the condition
    + `value` - the value response to the variable

## Update settings of agent wrap-up for a campaign
### End Point
  `PUT /api/v1/livechat/campaigns/{id}/agentWrapup`

### Parameters
  - `fields` - fields list
    + `id` - id of the field
    + `name` - name of the field
    + `type` - type of the field
      * `name` - Name field (system field)
      * `email` - Email field (system field)
      * `phone` - Phone field (system field)
      * `company` - Company field (system field)
      * `product` - Product and Service field (system field)
      * `department` - Department field (system field)
      * `ticket` - Ticket field (system field)
      * `rating` - Rating field (system field)
      * `comment` - Comment field (system field)
      * `subject` - Subject field (system field)
      * `content` - Content field (system field)
      * `attachment` - Attachment field (system field)
      * `text` - Text field (custom field)
      * `textarea` - Textarea field (custom field)
      * `radio` - Radio Box field (custom field)
      * `checkbox` - Check Box field (custom field)
      * `select` - Drop Down List field (custom field)
      * `checkboxList` - Check Box List field (custom field)
    + `isSystem` - whether the field is system field or not.
    + `isVisible` - whether the field is visible or not .
    + `isRequired` - whether the field is required or not when submiting the form.
    + `options` - the options of the field

### Response
  - `fields` - fields list
    + `id` - id of the field
    + `name` - name of the field
    + `type` - type of the field
    + `isSystem` - whether the field is system field or not.
    + `isVisible` - whether the field is visible or not .
    + `isRequired` - whether the field is required or not when submiting the form.
    + `options` - the options of the field


## Get settings of Routing Rules for a campaign
### End Point
  `GET /api/v1/livechat/campaigns/{id}/RoutingRules`

### Parameters
  No parameters

### Response
  - `isEnable` -whether the routing rules is enable or not.
  - `routingType` -the type of routing,including `routeDepartmentOrAgent` and `routeCustomRules`.
  - `routeRule` - the rule of route ,including `department` and `agent`
  - `departmentId` - id of the department
  - `departmentPriority` - the priority of the department,including `lowest`、`low`、`normal`、`high` and `highest`.
  - `agentId` - id of the agent
  - `agentPriority` - the priority of the agent,including `lowest`、`low`、`normal`、`high` and `highest`.
  - `customRules` - custom rules list
    + `id` -id of the custom rule
    + `name` -name of the custom rule
    + `conditions` -conditions of the custom rule
    + `routeOjbect` - name of the route object
    + `priority` - the priority for the route
    + `isEnable` -whether the custom rule is enable or not.
  - `failRoutingType` -the type of fail routing,including `routeDepartmentOrAgent` and `routeCustomRules`.
  - `failRouteRule` - the rule of fail route ,including `department` and `agent`
  - `failRouteDepartmentId` - id of the department for fail routing
  - `failRouteDepartmentPriority` - the priority of the department for fail routing,including `lowest`、`low`、`normal`、`high` and `highest`.
  - `failRouteAgentId` - id of the agent for fail routing
  - `failRouteAgentPriority` - the priority of the agent for fail routing,including `lowest`、`low`、`normal`、`high` and `highest`.
  - `failToEmail` - redirect them to Offline Message Window and forward their messages to the email

## Update settings of Routing Rules for a campaign
### End Point
  Optional:
  - `isEnable` -whether the routing rules is enable or not.
  - `routingType` -the type of routing,including `routeDepartmentOrAgent` and `routeCustomRules`.
  - `routeRule` - the rule of route ,including `department` and `agent`
  - `departmentId` - id of the department
  - `departmentPriority` - the priority of the department,including `lowest`、`low`、`normal`、`high` and `highest`.
  - `agentId` - id of the agent
  - `agentPriority` - the priority of the agent,including `lowest`、`low`、`normal`、`high` and `highest`.
  - `customRules` - custom rules list
    + `id` -id of the custom rule
    + `name` -name of the custom rule
    + `conditions` -conditions of the custom rule
    + `routeOjbect` - name of the route object
    + `priority` - the priority for the route
    + `isEnable` -whether the custom rule is enable or not.
  - `failRoutingType` -the type of fail routing,including `routeDepartmentOrAgent` and `routeCustomRules`.
  - `failRouteRule` - the rule of fail route ,including `department` and `agent`
  - `failRouteDepartmentId` - id of the department for fail routing
  - `failRouteDepartmentPriority` - the priority of the department for fail routing,including `lowest`、`low`、`normal`、`high` and `highest`.
  - `failRouteAgentId` - id of the agent for fail routing
  - `failRouteAgentPriority` - the priority of the agent for fail routing,including `lowest`、`low`、`normal`、`high` and `highest`.
  - `failToEmail` - redirect them to Offline Message Window and forward their messages to the email

### Parameters
  No parameters

### Response
  - `isEnable` -whether the routing rules is enable or not.
  - `routingType` -the type of routing,including `routeDepartmentOrAgent` and `routeCustomRules`.
  - `routeRule` - the rule of route ,including `department` and `agent`
  - `departmentId` - id of the department
  - `departmentPriority` - the priority of the department,including `lowest`、`low`、`normal`、`high` and `highest`.
  - `agentId` - id of the agent
  - `agentPriority` - the priority of the agent,including `lowest`、`low`、`normal`、`high` and `highest`.
  - `customRules` - custom rules list
    + `id` -id of the custom rule
    + `name` -name of the custom rule
    + `conditions` -conditions of the custom rule
    + `routeOjbect` - name of the route object
    + `priority` - the priority for the route
    + `isEnable` -whether the custom rule is enable or not.
  - `failRoutingType` -the type of fail routing,including `routeDepartmentOrAgent` and `routeCustomRules`.
  - `failRouteRule` - the rule of fail route ,including `department` and `agent`
  - `failRouteDepartmentId` - id of the department for fail routing
  - `failRouteDepartmentPriority` - the priority of the department for fail routing,including `lowest`、`low`、`normal`、`high` and `highest`.
  - `failRouteAgentId` - id of the agent for fail routing
  - `failRouteAgentPriority` - the priority of the agent for fail routing,including `lowest`、`low`、`normal`、`high` and `highest`.
  - `failToEmail` - redirect them to Offline Message Window and forward their messages to the email

## Get a custom rule for a campaign
### End Point
  `GET /api/v1/livechat/campaigns/{id}/RoutingRules/customRules/{customeRule_id}`

### Parameters
  No parameters

### Response
  - `id` -id of the custom rule.
  - `isEnable` -whether the custom rule is enable or not.
  - `triggeredWhen` - when the rule is triggered, including `all`、`any` and `logicalExpression` 
  - `logicalExpression` - the logical expression of the conditions
  - `conditions` -condition list
    + `variableName` - name of the variable,including comm100 system variable and custom variable
    + `expression` - expression of the condition
    + `value` - the value response to the variable
  - `routeRule` - the rule of route ,including `department` and `agent`
  - `departmentId` - id of the department
  - `departmentPriority` - the priority of the department,including `lowest`、`low`、`normal`、`high` and `highest`.
  - `agentId` - id of the agent
  - `agentPriority` - the priority of the agent,including `lowest`、`low`、`normal`、`high` and `highest`.

## Create a new custom rule for a campaign
### End Point
  `POST /api/v1/livechat/campaigns/{id}/RoutingRules/customRules`

### Parameters
  - `isEnable` -whether the custom rule is enable or not.
  - `triggeredWhen` - when the rule is triggered, including `all`、`any` and `logicalExpression` 
  - `logicalExpression` - the logical expression of the conditions
  - `conditions` -condition list
    + `variableName` - name of the variable,including comm100 system variable and custom variable
    + `expression` - expression of the condition
    + `value` - the value response to the variable
  - `routeRule` - the rule of route ,including `department` and `agent`
  - `departmentId` - id of the department
  - `departmentPriority` - the priority of the department,including `lowest`、`low`、`normal`、`high` and `highest`.
  - `agentId` - id of the agent
  - `agentPriority` - the priority of the agent,including `lowest`、`low`、`normal`、`high` and `highest`.  

### Response
  - `id` -id of the custom rule.
  - `isEnable` -whether the custom rule is enable or not.
  - `triggeredWhen` - when the rule is triggered, including `all`、`any` and `logicalExpression` 
  - `logicalExpression` - the logical expression of the conditions
  - `conditions` -condition list
    + `variableName` - name of the variable,including comm100 system variable and custom variable
    + `expression` - expression of the condition
    + `value` - the value response to the variable
  - `routeRule` - the rule of route ,including `department` and `agent`
  - `departmentId` - id of the department
  - `departmentPriority` - the priority of the department,including `lowest`、`low`、`normal`、`high` and `highest`.
  - `agentId` - id of the agent
  - `agentPriority` - the priority of the agent,including `lowest`、`low`、`normal`、`high` and `highest`.  

## Update a custom rule for a campaign
### End Point
  `PUT /api/v1/livechat/campaigns/{id}/RoutingRules/customRules/{customeRule_id}` 

### Parameters
  - `isEnable` -whether the custom rule is enable or not.
  - `triggeredWhen` - when the rule is triggered, including `all`、`any` and `logicalExpression` 
  - `logicalExpression` - the logical expression of the conditions
  - `conditions` -condition list
    + `variableName` - name of the variable,including comm100 system variable and custom variable
    + `expression` - expression of the condition
    + `value` - the value response to the variable
  - `routeRule` - the rule of route ,including `department` and `agent`
  - `departmentId` - id of the department
  - `departmentPriority` - the priority of the department,including `lowest`、`low`、`normal`、`high` and `highest`.
  - `agentId` - id of the agent
  - `agentPriority` - the priority of the agent,including `lowest`、`low`、`normal`、`high` and `highest`.  

### Response
  - `id` -id of the custom rule.
  - `isEnable` -whether the custom rule is enable or not.
  - `triggeredWhen` - when the rule is triggered, including `all`、`any` and `logicalExpression` 
  - `logicalExpression` - the logical expression of the conditions
  - `conditions` -condition list
    + `variableName` - name of the variable,including comm100 system variable and custom variable
    + `expression` - expression of the condition
    + `value` - the value response to the variable
  - `routeRule` - the rule of route ,including `department` and `agent`
  - `departmentId` - id of the department
  - `departmentPriority` - the priority of the department,including `lowest`、`low`、`normal`、`high` and `highest`.
  - `agentId` - id of the agent
  - `agentPriority` - the priority of the agent,including `lowest`、`low`、`normal`、`high` and `highest`.  

## Get settings of Language for a campaign
### End Point
  `GET /api/v1/livechat/campaigns/{id}/language`

### Parameters
  No parameters

### Response
  - `language ` -the main language.
  - `isCustomLanguage` - whether the custom language is used or not.
  - `isRTL` -whether the language is from right to left.
  - `languageSettings` - the language settings list
    + `module` - the module of language settings,including `Buttons`、`Fields`、`Prompts`、`SystemMessages`、`AudioChat`、`VideoChat`、`ScreenSharing`、`TranscriptEmail`、`TextOnMobile`、`EmbeddedWindow` and `Chatbot`. 
    + `name` -the name of field of the language settings
    + `defaultText` - the default text of field of the language settings
    + `currentText` - current text of field of the language settings
    + `macros` - macors which used in the field of the language settings

## Update settings of Language for a campaign
### End Point
  `PUT /api/v1/livechat/campaigns/{id}/language`

### Parameters
  - `language ` -the main language.
  - `isCustomLanguage` - whether the custom language is used or not.
  - `isRTL` -whether the language is from right to left.
  - `languageSettings` - the language settings list
    + `module` - the module of language settings,including `Buttons`、`Fields`、`Prompts`、`SystemMessages`、`AudioChat`、`VideoChat`、`ScreenSharing`、`TranscriptEmail`、`TextOnMobile`、`EmbeddedWindow` and `Chatbot`. 
    + `name` -the name of field of the language settings
    + `defaultText` - the default text of field of the language settings
    + `currentText` - current text of field of the language settings
    + `macros` - macors which used in the field of the language settings

### Response
  - `language ` -the main language.
  - `isCustomLanguage` - whether the custom language is used or not.
  - `isRTL` -whether the language is from right to left.
  - `languageSettings` - the language settings list
    + `module` - the module of language settings,including `Buttons`、`Fields`、`Prompts`、`SystemMessages`、`AudioChat`、`VideoChat`、`ScreenSharing`、`TranscriptEmail`、`TextOnMobile`、`EmbeddedWindow` and `Chatbot`. 
    + `name` -the name of field of the language settings
    + `defaultText` - the default text of field of the language settings
    + `currentText` - current text of field of the language settings
    + `macros` - macors which used in the field of the language settings

## Canned Message
  You need `Manage Pulbic Canned Messages` permission to manage canned message.
  + `GET /api/v1/livechat/cannedMessages` -get list of canned Message
  + `GET /api/v1/livechat/cannedMessages/{id}`  -get a single canned Message
  + `POST /api/v1/livechat/cannedMessages` -create a new canned Message
  + `PUT /api/v1/livechat/cannedMessages/{id}`  -update a canned Message
  + `DELETE /api/v1/livechat/cannedMessages/{id}`  -remove a canned Message

### Get list of canned messages 
#### End Point 
  `GET /api/v1/livechat/cannedMessages`

#### Parameters
  No parameters

#### Response
  canned messages list, including
  - `id ` -id of the canned message.
  - `name` -name of the canned message.
  - `message` -content of the canned message.
  - `shortcuts` - shortcuts of the canned message.
  - `categoryId` -id of the category of the canned message.
  - `isPrivate` - whether the canned message is private or not.

### Get a single canned message 
#### End Point 
  `GET /api/v1/livechat/cannedMessages/{id}`

#### Parameters
  No parameters

#### Response
  - `id ` -id of the canned message.
  - `name` -name of the canned message.
  - `message` -content of the canned message.
  - `shortcuts` - shortcuts of the canned message.
  - `categoryId` -id of the category of the canned message.
  - `isPrivate` - whether the canned message is private or not.

### Create a new canned message 
#### End Point 
  `POST /api/v1/livechat/cannedMessages`

#### Parameters
  - `name` -name of the canned message.
  - `message` -content of the canned message.
  - `categoryId` -id of the category of the canned message.
  - `isPrivate` - whether the canned message is private or not.
optional:
  - `shortcuts` - shortcuts of the canned message.

#### Response
  - `id ` -id of the canned message.
  - `name` -name of the canned message.
  - `message` -content of the canned message.
  - `shortcuts` - shortcuts of the canned message.
  - `categoryId` -id of the category of the canned message.
  - `isPrivate` - whether the canned message is private or not.

### Update a canned message 
#### End Point 
  `PUT /api/v1/livechat/cannedMessages/{id}`

#### Parameters
  - `name` -name of the canned message.
  - `message` -content of the canned message.
  - `categoryId` -id of the category of the canned message.
optional:
  - `shortcuts` - shortcuts of the canned message.

#### Response
  - `id ` -id of the canned message.
  - `name` -name of the canned message.
  - `message` -content of the canned message.
  - `shortcuts` - shortcuts of the canned message.
  - `categoryId` -id of the category of the canned message.
  - `isPrivate` - whether the canned message is private or not.

### Remove a canned message 
#### End Point 
  `DELETE /api/v1/livechat/cannedMessages/{id}`

#### Parameters
  No parameters

#### Response
  - `result ` -the result of operating

## Canned Message Category
  You need `Manage Pulbic Canned Messages` permission to manage canned message category.
  + `GET /api/v1/livechat/cannedMessageCategories` -get list of canned Messages Categories
  + `GET /api/v1/livechat/cannedMessageCategories/{id}`  -get a single canned Messages Category
  + `POST /api/v1/livechat/cannedMessageCategories` -create a new canned Messages Category
  + `PUT /api/v1/livechat/cannedMessageCategories/{id}`  -update a canned Messages Category
  + `DELETE /api/v1/livechat/cannedMessageCategories/{id}`  -remove a canned Messages Category

### Get list of canned message categories
#### End Point 
  `GET /api/v1/livechat/cannedMessageCategories`

#### Parameters
  No parameters

#### Response
  canned message categories list, including
  - `id ` -id of the canned message category.
  - `name` -name of the canned message category.
  - `parentCategoryId` - id of the parent of the canned message category
  - `parentCategoryName` -name of the parent of the canned message category
  - `isPrivate` - whether the canned message category is private or not.

### Get a single canned message category
#### End Point 
  `GET /api/v1/livechat/cannedMessageCategories/{id}`

#### Parameters
  No parameters

#### Response
  - `id ` -id of the canned message category.
  - `name` -name of the canned message category.
  - `parentCategoryId` - id of the parent of the canned message category
  - `parentCategoryName` -name of the parent of the canned message category
  - `isPrivate` - whether the canned message category is private or not.

### Create a new canned message category
#### End Point 
  `POST /api/v1/livechat/cannedMessageCategories`

#### Parameters
  - `name` -name of the canned message category.
  - `parentCategoryId` - id of the parent of the canned message category

#### Response
  - `id ` -id of the canned message category.
  - `name` -name of the canned message category.
  - `parentCategoryId` - id of the parent of the canned message category
  - `parentCategoryName` -name of the parent of the canned message category
  - `isPrivate` - whether the canned message category is private or not.

### Update a canned message category
#### End Point 
  `PUT /api/v1/livechat/cannedMessageCategories/{id}`

#### Parameters
  - `name` -name of the canned message category.
  - `parentCategoryId` - id of the parent of the canned message category

#### Response
  - `id ` -id of the canned message category.
  - `name` -name of the canned message category.
  - `parentCategoryId` - id of the parent of the canned message category
  - `parentCategoryName` -name of the parent of the canned message category
  - `isPrivate` - whether the canned message category is private or not.

### Remove a canned message category
#### End Point 
  `DELETE /api/v1/livechat/cannedMessageCategories/{id}`

#### Parameters
  No parameters

#### Response
  - `result ` -the result of operating

## Department
  You need `Manage Settings` permission to manage department.
  + `GET /api/v1/livechat/departments` -get list of departments
  + `GET /api/v1/livechat/departments/{id}`  -get a single department
  + `POST /api/v1/livechat/departments` -create a new department
  + `PUT /api/v1/livechat/departments/{id}`  -update a department
  + `DELETE /api/v1/livechat/departments/{id}`  -remove a department

### Get list of departments 
#### End Point 
  `GET /api/v1/livechat/departments`

#### Parameters
  No parameters

#### Response
  departments list, including
  - `id ` -id of the department.
  - `name` -name of the department.
  - `description` -description of the department.
  - `members` - the string of the members list in the department.
  - `allocationStratege` - stratege of chat allocation,including `load banlancing` 、`round robin` and `capability weighted`.
  - `isLastChattedPreferred` -whether last-chatted agent is prefer or not.
  - `backupDepartmentId` - id of back up department

### Get a single department 
#### End Point 
  `GET /api/v1/livechat/departments/{id}`

#### Parameters
  No parameters

#### Response
  - `id ` -id of the department.
  - `name` -name of the department.
  - `description` -description of the department.
  - `agentIds` - the id of the agent list in the department.
  - `groupIds` - the id of the groups list in the department.
  - `offlineMessageTo` - object which mail offline messages of the department to,including `allAgents` and `emailAddresses`
  - `emaileAddresses` - the email addresses which mail offline messages of the department to
  - `allocationStratege` - stratege of chat allocation,including `load banlancing` 、`round robin` and `capability weighted`.
  - `isLastChattedPreferred` -whether last-chatted agent is prefer or not.
  - `backupDepartmentId` - id of back up department

### Create a new department 
#### End Point 
  `POST /api/v1/livechat/departments`

#### Parameters
  - `name` -name of the department.
  optional:
  - `description` -description of the department.
  - `agentIds` - the id of the agent list in the department.
    + `agentId` - id of agent
  - `groupIds` - the id of the groups list in the department.
    + `groupId` -id of group
  - `offlineMessageTo` - object which mail offline messages of the department to,including `allAgents` and `emailAddresses`
  - `emaileAddresses` - the email addresses which mail offline messages of the department to

#### Response
  - `id ` -id of the department.
  - `name` -name of the department.
  - `description` -description of the department.
  - `agentIds` - the id of the agent list in the department.
    + `agentId` - id of agent
  - `groupIds` - the id of the groups list in the department.
    + `groupId` -id of group
  - `offlineMessageTo` - object which mail offline messages of the department to,including `allAgents` and `emailAddresses`
  - `emaileAddresses` - the email addresses which mail offline messages of the department to
  - `allocationStratege` - stratege of chat allocation,including `load banlancing` 、`round robin` and `capability weighted`.
  - `isLastChattedPreferred` -whether last-chatted agent is prefer or not.
  - `backupDepartmentId` - id of back up department

### Update a department 
#### End Point 
  `PUT /api/v1/livechat/departments/{id}`

#### Parameters
  - `name` -name of the department.
  optional:
  - `description` -description of the department.
  - `agentIds` - the id of the agent list in the department.
    + `agentId` - id of agent
  - `groupIds` - the id of the groups list in the department.
    + `groupId` -id of group
  - `offlineMessageTo` - object which mail offline messages of the department to,including `allAgents` and `emailAddresses`
  - `emaileAddresses` - the email addresses which mail offline messages of the department to
  - `allocationStratege` - stratege of chat allocation,including `load banlancing` 、`round robin` and `capability weighted`.
  - `isLastChattedPreferred` -whether last-chatted agent is prefer or not.
  - `backupDepartmentId` - id of back up department

#### Response
  - `id ` -id of the department.
  - `name` -name of the department.
  - `description` -description of the department.
  - `agentIds` - the id of the agent list in the department.
    + `agentId` - id of agent
  - `groupIds` - the id of the groups list in the department.
    + `groupId` -id of group
  - `offlineMessageTo` - object which mail offline messages of the department to,including `allAgents` and `emailAddresses`
  - `emaileAddresses` - the email addresses which mail offline messages of the department to
  - `allocationStratege` - stratege of chat allocation,including `load banlancing` 、`round robin` and `capability weighted`.
  - `isLastChattedPreferred` -whether last-chatted agent is prefer or not.
  - `backupDepartmentId` - id of back up department

### Remove a department
#### End Point 
  `DELETE /api/v1/livechat/departments/{id}`

#### Parameters
  No parameters

#### Response
  - `result ` -the result of operating

## Auto Allocation
You need `Manage Settings` permission to config auto allocation.
  + `GET /api/v1/livechat/autoAllocation` -Get settings of auto allocation.
  + `PUT /api/v1/livechat/autoAllocation`  -Update settings of auto allocation.

### Get settings of auto allocation.
#### End Point 
  `GET /api/v1/livechat/autoAllocation`

#### Parameters
  No parameters

#### Response
  - `id ` -id of the auto allocation.
  - `isEnable` -whether the auto allocation is enable or not.
  - `isEnableDepartment` - whether department is enable or not.
  - `allocationStratege` - stratege of chat allocation,including `load banlancing` 、`round robin` and `capability weighted`, available when the `isEnableDepartment` is `false`.
  - `isLastChattedPreferred` -whether last-chatted agent is prefer or not, available when the `isEnableDepartment` is `false`.
  - `isEnableAllocateWhenAudioVideo` -whether auto allocate chats to agents who are having audio or video chats is enable or not.

### Update settings of auto allocation.
#### End Point 
  `PUT /api/v1/livechat/autoAllocation`

#### Parameters
optional:  
  - `allocationStratege` - stratege of chat allocation,including `load banlancing` 、`round robin` and `capability weighted`, available when the `isEnableDepartment` is `false`.
  - `isLastChattedPreferred` -whether last-chatted agent is prefer or not, available when the `isEnableDepartment` is `false`.
  - `isEnableAllocateWhenAudioVideo` -whether auto allocate chats to agents who are having audio or video chats is enable or not.

#### Response
  - `id ` -id of the auto allocation.
  - `isEnable` -whether the auto allocation is enable or not.
  - `isEnableDepartment` - whether department is enable or not.
  - `allocationStratege` - stratege of chat allocation,including `load banlancing` 、`round robin` and `capability weighted`, available when the `isEnableDepartment` is `false`.
  - `isLastChattedPreferred` -whether last-chatted agent is prefer or not, available when the `isEnableDepartment` is `false`.
  - `isEnableAllocateWhenAudioVideo` -whether auto allocate chats to agents who are having audio or video chats is enable or not.

## Custom Away Status
  You need `Manage Settings` permission to manage custom away status.
  + `GET /api/v1/livechat/customAwayStatus` -get list of custom away status
  + `GET /api/v1/livechat/customAwayStatus/{id}`  -get a single custom away status
  + `POST /api/v1/livechat/customAwayStatus` -create a new custom away status
  + `PUT /api/v1/livechat/customAwayStatus/{id}`  -update a custom away status
  + `DELETE /api/v1/livechat/customAwayStatus/{id}`  -remove a custom away status

### Get list of custom away status 
#### End Point 
  `GET /api/v1/livechat/customAwayStatus`

#### Parameters
  No parameters

#### Response
  custom away status list, including
  - `id ` -id of the custom away status.
  - `name` -name of the custom away status.
  - `isVisible` -whether the custom away status is visible or not.
  - `isSystem` - whether the custom away status is system status or not.

### Get a single custom away status 
#### End Point 
  `GET /api/v1/livechat/customAwayStatus/{id}`

#### Parameters
  No parameters

#### Response
  - `id ` -id of the custom away status.
  - `name` -name of the custom away status.
  - `isVisible` -whether the custom away status is visible or not.
  - `isSystem` - whether the custom away status is system status or not.

### Create a new custom away status 
#### End Point 
  `POST /api/v1/livechat/customAwayStatus`

#### Parameters
  - `name` -name of the custom away status.
  - `isVisible` -whether the custom away status is visible or not.

#### Response
  - `id ` -id of the custom away status.
  - `name` -name of the custom away status.
  - `isVisible` -whether the custom away status is visible or not.
  - `isSystem` - whether the custom away status is system status or not.

### Update a custom away status 
#### End Point 
  `PUT /api/v1/livechat/customAwayStatus/{id}`

#### Parameters
  - `name` -name of the custom away status.
  - `isVisible` -whether the custom away status is visible or not.

#### Response
  - `id ` -id of the custom away status.
  - `name` -name of the custom away status.
  - `isVisible` -whether the custom away status is visible or not.
  - `isSystem` - whether the custom away status is system status or not.

### Remove a custom away status 
#### End Point 
  `DELETE /api/v1/livechat/customAwayStatus/{id}`

#### Parameters
  No parameters

#### Response
  - `result ` -the result of operating

## Ban
  You need `Manage Ban List` permission to manage ban list.
  + `GET /api/v1/livechat/bans` -get list of bans
  + `GET /api/v1/livechat/bans/{id}`  -get a single ban
  + `POST /api/v1/livechat/bans` -create a new ban
  + `PUT /api/v1/livechat/bans/{id}`  -update a ban
  + `DELETE /api/v1/livechat/bans/{id}`  -remove a ban

### Get list of bans
#### End Point 
  `GET /api/v1/livechat/bans`

#### Parameters
  No parameters

#### Response
  ban list, including
  - `id ` -id of the ban.
  - `banType` -type of ban,including `visitorId`、`ip` and `ipArrange`.
  - `banValue1` - value of ban,it means `ip from` while `banType` is `ipArrange` 
  - `banValue2` -ban to the ip ,available when the `banType` is `ipArrange`.
  - `comment` - comment of the ban.

### Get a single ban
#### End Point 
  `GET /api/v1/livechat/bans/{id}`

#### Parameters
  No parameters

#### Response
  - `id ` -id of the ban.
  - `banType` -type of ban,including `visitorId`、`ip` and `ipArrange`.
  - `banValue1` - value of ban,it means `ip from` while `banType` is `ipArrange` 
  - `banValue2` -ban to the ip ,available when the `banType` is `ipArrange`.
  - `comment` - comment of the ban.

### Create a new ban 
#### End Point 
  `POST /api/v1/livechat/bans`

#### Parameters
  - `banType` -type of ban,including `visitorId`、`ip` and `ipArrange`.
  - `banValue1` - value of ban,it means `ip from` while `banType` is `ipArrange` 
  - `banValue2` -ban to the ip ,available when the `banType` is `ipArrange`.
  - `comment` - comment of the ban.

#### Response
  - `id ` -id of the ban.
  - `banType` -type of ban,including `visitorId`、`ip` and `ipArrange`.
  - `banValue1` - value of ban,it means `ip from` while `banType` is `ipArrange` 
  - `banValue2` -ban to the ip ,available when the `banType` is `ipArrange`.
  - `comment` - comment of the ban.

### Update a ban
#### End Point 
  `PUT /api/v1/livechat/bans/{id}`

#### Parameters
  - `banType` -type of ban,including `visitorId`、`ip` and `ipArrange`.
  - `banValue1` - value of ban,it means `ip from` while `banType` is `ipArrange` 
  - `banValue2` -ban to the ip ,available when the `banType` is `ipArrange`.
  - `comment` - comment of the ban.

#### Response
  - `id ` -id of the ban.
  - `banType` -type of ban,including `visitorId`、`ip` and `ipArrange`.
  - `banValue1` - value of ban,it means `ip from` while `banType` is `ipArrange` 
  - `banValue2` -ban to the ip ,available when the `banType` is `ipArrange`.
  - `comment` - comment of the ban.

### Remove a ban
#### End Point 
  `DELETE /api/v1/livechat/bans/{id}`

#### Parameters
  No parameters

#### Response
  - `result ` -the result of operating

## Conversion Action
  You need `Manage Settings` permission to manage conversion action.
  + `GET /api/v1/livechat/conversionsActions` -get list of visitor segments
  + `GET /api/v1/livechat/conversionsActions/{id}`  -get a visitor segment
  + `POST /api/v1/livechat/conversionsActions` -create a new visitor segment

### Get list of conversion actions
#### End Point 
  `GET /api/v1/livechat/conversionsActions`

#### Parameters
  No parameters

#### Response
  conversion actions list, including
  - `id ` -id of the conversion action.
  - `name` - name of the conversion action.
  - `isEnable` -whether the conversion action is enable or not.
  - `typeContent` -content of type of the conversion action.

### Get a single conversion action
#### End Point 
  `GET /api/v1/livechat/conversionsActions/{id}`

#### Parameters
  No parameters

#### Response
  - `id ` -id of the conversion action.
  - `name` - name of the conversion action.
  - `isEnable` -whether the conversion action is enable or not.
  - `type` -type of the conversion action,including `url`、`customVariable` and `setByApi`.
  - `matchType` - match type of the conversion action.
  - `matchValue` - match value of the conversion action.
  - `isCaseSensitive` - whether the conversion action is case sensitive or not,available when `type` is `url`
  - `isAssignValue` - whether a value is assigned for the conversion action or not
  - `value` - the value assigned for the conversion action,available when `isAssignValue` is `true`
  - `customVariable` - the value come from the custom variable,available when `isAssignValue` is `true`
  - `customVariableField` - the name of the custom variable,available when `type` is `customVariable`.

### Create a new conversion action
#### End Point 
  `POST /api/v1/livechat/conversionsActions`

#### Parameters
  - `name` - name of the conversion action.
  - `isEnable` -whether the conversion action is enable or not.
  - `type` -type of the conversion action,including `url`、`customVariable` and `setByApi`.
  - `matchType` - match type of the conversion action.
  - `matchValue` - match value of the conversion action.
  - `isCaseSensitive` - whether the conversion action is case sensitive or not,available when `type` is `url`
  - `isAssignValue` - whether a value is assigned for the conversion action or not
  - `value` - the value assigned for the conversion action,available when `isAssignValue` is `true`
  - `customVariable` - the value come from the custom variable,available when `isAssignValue` is `true`
  - `customVariableField` - the name of the custom variable,available when `type` is `customVariable`.

#### Response
  - `id ` -id of the conversion action.
  - `name` - name of the conversion action.
  - `isEnable` -whether the conversion action is enable or not.
  - `type` -type of the conversion action,including `url`、`customVariable` and `setByApi`.
  - `matchType` - match type of the conversion action.
  - `matchValue` - match value of the conversion action.
  - `isCaseSensitive` - whether the conversion action is case sensitive or not,available when `type` is `url`
  - `isAssignValue` - whether a value is assigned for the conversion action or not
  - `value` - the value assigned for the conversion action,available when `isAssignValue` is `true`
  - `customVariable` - the value come from the custom variable,available when `isAssignValue` is `true`
  - `customVariableField` - the name of the custom variable,available when `type` is `customVariable`.

### Update a conversion action
#### End Point 
  `PUT /api/v1/livechat/conversionsActions/{id}`

#### Parameters
  - `name` - name of the conversion action.
  - `isEnable` -whether the conversion action is enable or not.
  - `type` -type of the conversion action,including `url`、`customVariable` and `setByApi`.
  - `matchType` - match type of the conversion action.
  - `matchValue` - match value of the conversion action.
  - `isCaseSensitive` - whether the conversion action is case sensitive or not,available when `type` is `url`
  - `isAssignValue` - whether a value is assigned for the conversion action or not
  - `value` - the value assigned for the conversion action,available when `isAssignValue` is `true`
  - `customVariable` - the value come from the custom variable,available when `isAssignValue` is `true`
  - `customVariableField` - the name of the custom variable,available when `type` is `customVariable`.

#### Response
  - `id ` -id of the conversion action.
  - `name` - name of the conversion action.
  - `isEnable` -whether the conversion action is enable or not.
  - `type` -type of the conversion action,including `url`、`customVariable` and `setByApi`.
  - `matchType` - match type of the conversion action.
  - `matchValue` - match value of the conversion action.
  - `isCaseSensitive` - whether the conversion action is case sensitive or not,available when `type` is `url`
  - `isAssignValue` - whether a value is assigned for the conversion action or not
  - `value` - the value assigned for the conversion action,available when `isAssignValue` is `true`
  - `customVariable` - the value come from the custom variable,available when `isAssignValue` is `true`
  - `customVariableField` - the name of the custom variable,available when `type` is `customVariable`.

## Visitor Segmentation
  You need `Manage Settings` permission to manage visitor segmentation.
  + `GET /api/v1/livechat/visitorSegments` -get list of visitor segments
  + `GET /api/v1/livechat/visitorSegments/{id}`  -get a visitor segment
  + `POST /api/v1/livechat/visitorSegments` -create a new visitor segment
  + `PUT /api/v1/livechat/visitorSegments/{id}`  -update a visitor segment
  + `DELETE /api/v1/livechat/visitorSegments/{id}`  -remove a visitor segment

### Get list of visitor segments
#### End Point 
  `GET /api/v1/livechat/visitorSegments`

#### Parameters
  No parameters

#### Response
  visitor segments list, including
  - `id ` -id of the visitor segment.
  - `name` - name of the visitor segment.
  - `color` -color of the visitor segment
  - `isEnable` -whether the visitor segment is enable or not.
  - `priority` -priority of the visitor segment.
  - `description` - description of the visitor segment.
  - `displayConditions` - conditions which display in the list.
  - `displayNotifications` - objects of notification which display in the list.

### Get a single visitor segment
#### End Point 
  `GET /api/v1/livechat/visitorSegments/{id}`

#### Parameters
  No parameters

#### Response
  - `id ` -id of the visitor segment.
  - `name` - name of the visitor segment.
  - `color` -color of the visitor segment
  - `isEnable` -whether the visitor segment is enable or not.
  - `priority` -priority of the visitor segment.
  - `description` - description of the visitor segment.
  - `displayConditions` - conditions which display in the list.
  - `triggeredWhen` - when the rule is triggered, including `all`、`any` and `logicalExpression` 
  - `logicalExpression` - the logical expression of the conditions
  - `conditions` -condition list
    + `variableName` - name of the variable,including comm100 system variable and custom variable
    + `expression` - expression of the condition
    + `value` - the value response to the variable
  - `displayNotifications` - objects of notification which display in the list.
  - `notificationType` - type of notification, including `departments`、`agents` and `none`. 
  - `notifyObject` - object of notification
    + `id` -id of object of notification
    + `name` - name of object of notification

### Create a new visitor segment 
#### End Point 
  `POST /api/v1/livechat/visitorSegments`

#### Parameters
  - `name` - name of the visitor segment.
  - `color` -color of the visitor segment
  - `isEnable` -whether the visitor segment is enable or not.
  - `priority` -priority of the visitor segment.
  - `description` - description of the visitor segment.
  - `triggeredWhen` - when the rule is triggered, including `all`、`any` and `logicalExpression` 
  - `logicalExpression` - the logical expression of the conditions
  - `conditions` -condition list
    + `variableName` - name of the variable,including comm100 system variable and custom variable
    + `expression` - expression of the condition
    + `value` - the value response to the variable
  - `notificationType` - type of notification, including `departments`、`agents` and `none`. 
  - `notifyObject` - object of notification
    + `id` -id of object of notification
    + `name` - name of object of notification

#### Response
  - `id ` -id of the visitor segment.
  - `name` - name of the visitor segment.
  - `color` -color of the visitor segment
  - `isEnable` -whether the visitor segment is enable or not.
  - `priority` -priority of the visitor segment.
  - `description` - description of the visitor segment.
  - `displayConditions` - conditions which display in the list.
  - `triggeredWhen` - when the rule is triggered, including `all`、`any` and `logicalExpression` 
  - `logicalExpression` - the logical expression of the conditions
  - `conditions` -condition list
    + `variableName` - name of the variable,including comm100 system variable and custom variable
    + `expression` - expression of the condition
    + `value` - the value response to the variable
  - `displayNotifications` - objects of notification which display in the list.
  - `notificationType` - type of notification, including `departments`、`agents` and `none`. 
  - `notifyObject` - object of notification
    + `id` -id of object of notification
    + `name` - name of object of notification

### Update a visitor segment
#### End Point 
  `PUT /api/v1/livechat/visitorSegmentsbans/{id}`

#### Parameters
  - `name` - name of the visitor segment.
  - `color` -color of the visitor segment
  - `isEnable` -whether the visitor segment is enable or not.
  - `priority` -priority of the visitor segment.
  - `description` - description of the visitor segment.
  - `triggeredWhen` - when the rule is triggered, including `all`、`any` and `logicalExpression` 
  - `logicalExpression` - the logical expression of the conditions
  - `conditions` -condition list
    + `variableName` - name of the variable,including comm100 system variable and custom variable
    + `expression` - expression of the condition
    + `value` - the value response to the variable
  - `notificationType` - type of notification, including `departments`、`agents` and `none`. 
  - `notifyObject` - object of notification
    + `id` -id of object of notification
    + `name` - name of object of notification

#### Response
  - `id ` -id of the visitor segment.
  - `name` - name of the visitor segment.
  - `color` -color of the visitor segment
  - `isEnable` -whether the visitor segment is enable or not.
  - `priority` -priority of the visitor segment.
  - `description` - description of the visitor segment.
  - `displayConditions` - conditions which display in the list.
  - `triggeredWhen` - when the rule is triggered, including `all`、`any` and `logicalExpression` 
  - `logicalExpression` - the logical expression of the conditions
  - `conditions` -condition list
    + `variableName` - name of the variable,including comm100 system variable and custom variable
    + `expression` - expression of the condition
    + `value` - the value response to the variable
  - `displayNotifications` - objects of notification which display in the list.
  - `notificationType` - type of notification, including `departments`、`agents` and `none`. 
  - `notifyObject` - object of notification
    + `id` -id of object of notification
    + `name` - name of object of notification

### Remove a visitor segment
#### End Point 
  `DELETE /api/v1/livechat/visitorSegments/{id}`

#### Parameters
  No parameters

#### Response
  - `result ` -the result of operating

## Visitor SSO Settings
  You need `Manage Settings` permission to setting sso for a site.
  + `GET /api/v1/livechat/visitorSSO` -Get sso settings of visitor
  + `PUT /api/v1/livechat/visitorSSO`  -Update configuration of visitor

### Get sso settings of visitor
#### End Point 
  `GET /api/v1/livechat/visitorSSO`

#### Parameters
  No parameters

#### Response
  - `id` -id of the sso settings.
  - `siteId` -id of the site which the visitor sso belongs to.
  - `isEnable` - whether visitor sso is enable or not.
  - `signInUrl` -url which visitor sign in
  - `vertificationCertificate` -infomation of the Identity Provider Verification Certificate.
  - `certificateFileName` - file name of the certificate.
  - `dataMappings` - data mapping list of the sso.
    + `id` - id of the data mapping
    + `userAttribute` - user attribute of the mapping
    + `macro` - common 100 field correspond with the user attribute.
  - `signInOptions` - sign in options list.
    + `id` -id of the options
    + `campaignId` -id of the campaign
    + `signInType` -type of the sign in,including `no`、`optional` and `required`.
    + `isSkipPrechat` - whether the pre-chat form is skipped when visitors sign in, available when the `signInType` is not `no`.

### Update sso settings of visitor
#### End Point 
  `PUT /api/v1/livechat/visitorSSO`

#### Parameters
  - `isEnable` - whether visitor sso is enable or not.
  - `signInUrl` -url which visitor sign in
  - `vertificationCertificate` -infomation of the Identity Provider Verification Certificate.
  - `certificateFileName` - file name of the certificate.
  - `dataMappings` - data mapping list of the sso.
    + `userAttribute` - user attribute of the mapping
    + `macro` - common 100 field correspond with the user attribute.
  - `signInOptions` - sign in options list.
    + `campaignId` -id of the campaign
    + `signInType` -type of the sign in,including `no`、`optional` and `required`.
    + `isSkipPrechat` - whether the pre-chat form is skipped when visitors sign in, available when the `signInType` is not `no`.

#### Response
  - `id` -id of the sso settings.
  - `siteId` -id of the site which the visitor sso belongs to.
  - `isEnable` - whether visitor sso is enable or not.
  - `signInUrl` -url which visitor sign in
  - `vertificationCertificate` -infomation of the Identity Provider Verification Certificate.
  - `certificateFileName` - file name of the certificate.
  - `dataMappings` - data mapping list of the sso.
    + `id` - id of the data mapping
    + `userAttribute` - user attribute of the mapping
    + `macro` - common 100 field correspond with the user attribute.
  - `signInOptions` - sign in options list.
    + `id` -id of the options
    + `campaignId` -id of the campaign
    + `signInType` -type of the sign in,including `no`、`optional` and `required`.
    + `isSkipPrechat` - whether the pre-chat form is skipped when visitors sign in, available when the `signInType` is not `no`.

## Site Config
  You need `Manage Settings` permission to config for a site.
  + `GET /api/v1/livechat/configs` -get config for a site
  + `PUT /api/v1/livechat/configs`  -update configuration of a site

### Get config for a site
#### End Point 
  `GET /api/v1/livechat/configs`

#### Parameters
  No parameters

#### Response
  - `siteId` -id of the site which the configuration belongs to.
  - `isEnableMultipleCampaigns` - whether multiple campaigns are enable or not in the site.
  - `isEnableAutoAllocation` -whether auto allocation is enable or not in the site.
  - `isEnableCustomAwayStatus` -whether custom away status is enable or not in the site.
  - `isEnableDepartment` -whether department is enable or not in the site.
  - `isEnableAutoTranslation` - whether auto translation is enable or not in the site.
  - `isEnableAudioAndVideoChat` - whether audio&video chat is enable or not in the site.
  - `isEnableVisitorSegmentation` - whether visitor segmentation is enable or not in the site.
  - `isEnableVisitorSSO` - whether visitor SSO is enable or not in the site.
  - `isEnableCreditCardMasking` - whether Credit card masking is enable or not in the site.
  - `isEnableCustomVariables` - whether custom variables are enable or not in the site.
  - `isEnableSalesforce` - whether Salesforce integration is enable or not in the site.
  - `isEnableZendesk` - whether Zendesk integration is enable or not in the site.
  - `isEnableGoogleAnalytics` - whether Google Analytics integration is enable or not in the site.
  - `isEnableGotoMeeting` - whether GotoMeeting integration is enable or not in the site.
  - `isEnableJoinme` - whether Joinme integration is enable or not in the site.

### Update configuration of a site
#### End Point 
  `PUT /api/v1/livechat/configs`

#### Parameters
  optional:
  - `isEnableMultipleCampaigns` - whether multiple campaigns are enable or not in the site.
  - `isEnableAutoAllocation` -whether auto allocation is enable or not in the site.
  - `isEnableCustomAwayStatus` -whether custom away status is enable or not in the site.
  - `isEnableDepartment` -whether department is enable or not in the site.
  - `isEnableAutoTranslation` - whether auto translation is enable or not in the site.
  - `isEnableAudioAndVideoChat` - whether audio&video chat is enable or not in the site.
  - `isEnableVisitorSegmentation` - whether visitor segmentation is enable or not in the site.
  - `isEnableVisitorSSO` - whether visitor SSO is enable or not in the site.
  - `isEnableCreditCardMasking` - whether Credit card masking is enable or not in the site.
  - `isEnableCustomVariables` - whether custom variables are enable or not in the site.
  - `isEnableSalesforce` - whether Salesforce integration is enable or not in the site.
  - `isEnableZendesk` - whether Zendesk integration is enable or not in the site.
  - `isEnableGoogleAnalytics` - whether Google Analytics integration is enable or not in the site.
  - `isEnableGotoMeeting` - whether GotoMeeting integration is enable or not in the site.
  - `isEnableJoinme` - whether Joinme integration is enable or not in the site.

#### Response
  - `siteId` -id of the site which the configuration belongs to.
  - `isEnableMultipleCampaigns` - whether multiple campaigns are enable or not in the site.
  - `isEnableAutoAllocation` -whether auto allocation is enable or not in the site.
  - `isEnableCustomAwayStatus` -whether custom away status is enable or not in the site.
  - `isEnableDepartment` -whether department is enable or not in the site.
  - `isEnableAutoTranslation` - whether auto translation is enable or not in the site.
  - `isEnableAudioAndVideoChat` - whether audio&video chat is enable or not in the site.
  - `isEnableVisitorSegmentation` - whether visitor segmentation is enable or not in the site.
  - `isEnableVisitorSSO` - whether visitor SSO is enable or not in the site.
  - `isEnableCreditCardMasking` - whether Credit card masking is enable or not in the site.
  - `isEnableCustomVariables` - whether custom variables are enable or not in the site.
  - `isEnableSalesforce` - whether Salesforce integration is enable or not in the site.
  - `isEnableZendesk` - whether Zendesk integration is enable or not in the site.
  - `isEnableGoogleAnalytics` - whether Google Analytics integration is enable or not in the site.
  - `isEnableGotoMeeting` - whether GotoMeeting integration is enable or not in the site.
  - `isEnableJoinme` - whether Joinme integration is enable or not in the site.
