# General

## Campaign API
  You need `Manage Campaigns` permission to manage campaigns and customize the settings for a campaigns.
  - `Campaigns` -Campaigns Manage
    + `GET /api/v1/livechat/campaigns` -Get list of campaigns
    + `POST /api/v1/livechat/campaigns` -Create a new campaign
    + `PUT /api/v1/livechat/campaigns/{id}` -Update a campaign
    + `DELETE /api/v1/livechat/campaigns/{id}` -Remove a campaign
  - `Campaign Settings` --setting of campaign
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

## Get settings of ChatButton for a campaign
### End Point
  `GET /api/v1/livechat/campaigns/{id}/chatButton`

### Parameters
  No parameters

### Response
  - `buttonType ` -type of the permission,including `adaptive`、`image` and `textLink`.
  - `isHideOffline` -whether the chatButton is visible when no agent is online.`true` means that button is invisible.
  - `isEnableDomainRestriction` -whether the domain restriction is enable
  - `allowedDomains` -display the chat button on specified domains/URLs only.
  Optional:  
  - `adaptiveSettings` - settings when `buttonType` is `adaptive`
    + `themeColor` - the theme color of chatbutton
    + `onlineImageId` - id of the image when any agents are on line
    + `offlineImageId` - id of the image when no agent is on line
    + `onlineImageUrl` - url of the image when any agents is on line
    + `offlineImageUrl` - url of the image when no agent is on line
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
    + `mobileOnlineText` -the content of text on mobile device when any agents are on line
    + `mobileOfflineText` -the content of text on mobile device when no agent is on line
    + `mobileThemeColor` - the theme color of chatbutton on mobile device
    + `mobileOnlineImageUrl` -the url of image on mobile device when any agents are on line
    + `mobileOfflineImageUrl` -the url of image on mobile device when no agent is on line
    + `mobileImagePosition` - position of the chat button on mobile device， including `bottomLeft`、`bottomMiddle`、`bottomRight`、`leftMiddle`、`RightMiddle`、`leftBottom` and `rightBottom`.
  - `textLinkSettings` -settings when `buttonType` is `textLink`
    + `buttonText` -the content of the text link


## Update settings of ChatButton for a campaign
### End Point
  `PUT /api/v1/livechat/campaigns/{id}/chatButton`

### Parameters
  Required parameters: 
  - `buttonType ` -type of the permission,including `adaptive`、`image` and `textLink`.
  Optional parameters:    
  + `isHideOffline` -whether the chatButton is visible when no agent is online.`true` means that button is invisible.
  + `isEnableDomainRestriction` -whether the domain restriction is enable
  + `allowedDomains` -display the chat button on specified domains/URLs only.  
  + `themeColor` - the theme color of chatbutton
  + `onlineImageId` - id of the image when any agents are on line
  + `offlineImageId` - id of the image when no agent is on line
  + `onlineImageUrl` - url of the image when any agents is on line
  + `offlineImageUrl` - url of the image when no agent is on line
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
  + `mobileOnlineText` -the content of text on mobile device when any agents are on line
  + `mobileOfflineText` -the content of text on mobile device when no agent is on line
  + `mobileThemeColor` - the theme color of chatbutton on mobile device
  + `mobileOnlineImageUrl` -the url of image on mobile device when any agents are on line
  + `mobileOfflineImageUrl` -the url of image on mobile device when no agent is on line
  + `mobileImagePosition` - position of the chat button on mobile device， including `bottomLeft`、`bottomMiddle`、`bottomRight`、`leftMiddle`、`RightMiddle`  `leftBottom` and `rightBottom`.
  + `buttonText` -the content of the text link

### Response
  - `buttonType ` -type of the permission,including `adaptive`、`image` and `textLink`.
  - `isHideOffline` -whether the chatButton is visible when no agent is online.`true` means that button is invisible.
  - `isEnableDomainRestriction` -whether the domain restriction is enable
  - `allowedDomains` -display the chat button on specified domains/URLs only.
  Optional:  
  - `adaptiveSettings` - settings when `buttonType` is `adaptive`
    + `themeColor` - the theme color of chatbutton
    + `onlineImageId` - id of the image when any agents are on line
    + `offlineImageId` - id of the image when no agent is on line
    + `onlineImageUrl` - url of the image when any agents is on line
    + `offlineImageUrl` - url of the image when no agent is on line
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
    + `mobileOnlineText` -the content of text on mobile device when any agents are on line
    + `mobileOfflineText` -the content of text on mobile device when no agent is on line
    + `mobileThemeColor` - the theme color of chatbutton on mobile device
    + `mobileOnlineImageUrl` -the url of image on mobile device when any agents are on line
    + `mobileOfflineImageUrl` -the url of image on mobile device when no agent is on line
    + `mobileImagePosition` - position of the chat button on mobile device， including `bottomLeft`、`bottomMiddle`、`bottomRight`、`leftMiddle`、`RightMiddle`、`leftBottom` and `rightBottom`.
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
