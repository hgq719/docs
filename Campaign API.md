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
    + `GET /api/v1/livechat/campaigns/{id}/preChat`  -Get settings of PreChat for a campaign
    + `PUT /api/v1/livechat/campaigns/{id}/preChat`  -Update settings of PreChat for a campaign
    + `GET /api/v1/livechat/campaigns/{id}/postChat` -Get settings of PostChat for a campaign
    + `PUT /api/v1/livechat/campaigns/{id}/postChat` -Update settings of PostChat for a campaign
    + `GET /api/v1/livechat/campaigns/{id}/offlineMessage`  -Get settings of OfflineMessage for a campaign
    + `PUT /api/v1/livechat/campaigns/{id}/offlineMessage`  -Update settings of OfflineMessage for a campaign
    + `GET /api/v1/livechat/campaigns/{id}/autoInvitation`  -Get settings of AutoInvitation for a campaign
    + `PUT /api/v1/livechat/campaigns/{id}/autoInvitation`  -Update settings of AutoInvitation for a campaign
    + `GET /api/v1/livechat/campaigns/{id}/manualInvitation`  -Get settings of ManualInvitation for a campaign
    + `PUT /api/v1/livechat/campaigns/{id}/manualInvitation`  -Update settings of ManualInvitation for a campaign
    + `GET /api/v1/livechat/campaigns/{id}/agentWrapup`  -Get settings of Agent Wrap Up for a campaign
    + `PUT /api/v1/livechat/campaigns/{id}/agentWrapup`  -Update settings of Agent Wrap Up for a campaign
    + `GET /api/v1/livechat/campaigns/{id}/RoutingRules` -Get settings of Routing Rules for a campaign
    + `PUT /api/v1/livechat/campaigns/{id}/RoutingRules` -Update settings of Routing Rules for a campaign
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

### Example
Sample request:

  `curl -u tester@comm100.com:ef43f9362aac4f60ad428cb4d072f2c8 -X GET \`   
  `"https://hosted.comm100.com/api/v1/livechat/campaigns"`

Sample Response:
```javascript
  [ 
    {
      "id":"1590", 
      "name":"joe Campaign",
      "description" : ""
    },
    {
      "id":"2311", 
      "name":"sundy",
      "description" : "test for sundy"
    },
    ...
  ]   
```

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

### Example
Sample request:

  `curl –u allon@comm100.com:ef43f9362aac4f60ad428cb4d072f2c8 -X POST -d \`
  `name=kim%20campaign&description=this%20is%20my%20campaign%20for%20test \`   
  `"https://hosted.comm100.com/api/v1/livechat/campaigns"`

Sample Response:
```javascript
{ 
  "id":"2288", 
  "name":"kim campaign",
  "description" : "this is my campaign for test"
}	     
```

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

### Example
Sample request:

  `curl –u allon@comm100.com:ef43f9362aac4f60ad428cb4d072f2c8 -X PUT -d name=kim%20campaign&description=campaign%20description \`   
  `"https://hosted.comm100.com/api/v1/livechat/campaigns/2288"`

Sample Response:
```javascript
{ 
  "id":"2288", 
  "name":"kim campaign",
  "description" : "campaign description"
}	       
```

## Remove a campaign 
### End Point
  `DELETE /api/v1/livechat/campaigns/{id}`

### Parameters
  No parameters.

### Response
  - `result ` -the result of operating

### Example
Sample request:

  `curl –u allon@comm100.com:ef43f9362aac4f60ad428cb4d072f2c8 -X DELETE \`   
  `"https://hosted.comm100.com/api/v1/livechat/campaigns/2288"`

Sample Response:
```javascript
{
    "result":"Campaign '2288' has been removed."
}
```

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

### Example
Sample request:

  `curl -u tester@comm100.com:ef43f9362aac4f60ad428cb4d072f2c8 -X GET \`   
  `"https://hosted.comm100.com/api/v1/livechat/campaigns/2288/chatButton"`

Sample Response:
```javascript
  {
    "buttonType":"adaptive", 
    "themeColor": "#3AA682",
    "onlineImageId":"111",
    "offlineImageId" :"211",
    "onlineImageUrl":"https://hosted.comm100.com/resources/img/111.ico",
    "offlineImageUrl":"https://hosted.comm100.com/resources/img/222.ico"
    "isHideOffline":true,
    "isEnableDomainRestriction":true,
    "descripallowedDomainstion" : [
        "google.com",
        "facebook.com"
    ]    
  }     
```

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

### Example
Sample request:

  `curl –u allon@comm100.com:ef43f9362aac4f60ad428cb4d072f2c8 -X PUT -d buttonType=textLink&isHideOffline=false&isEnableDomainRestriction=false&buttonText=Chat%20Now \` 
  `"https://hosted.comm100.com/api/v1/livechat/campaigns/2288/chatButton"`

Sample Response:
```javascript
  {
    "buttonType":"textLink", 
    "buttonText": "Chat Now",
    "isHideOffline":false,
    "isEnableDomainRestriction":false
  }     
```


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
  - `isCanPrintChatDetail` -whether the chatButton is visible when no agent is online.`true` means that button is invisible.
  - `isShowEmail` -whether the domain restriction is enable
  - `isUseOperatorEmailOrFromEmail` -whether the domain restriction is enable
  - `fromEmail_email` -whether the domain restriction is enable
  - `fromEmail_name` -whether the domain restriction is enable
  - `isCanSwitchToOffline` -display the chat button on specified domains/URLs only.
  - `isCanSendFile` -display the chat button on specified domains/URLs only.
  - `isCanHaveAudioChat` -display the chat button on specified domains/URLs only.
  - `isCanHaveVideoChat` -display the chat button on specified domains/URLs only.
  - `isEndChatWhenVisitorInactivity` -display the chat button on specified domains/URLs only.
  - `timeEndChatDelayWhenVisitorInactivity` -display the chat button on specified domains/URLs only.
  - `isEnableSendTranscriptEmail` -display the chat button on specified domains/URLs only.
  - `sendTranscriptEmailAddress` -display the chat button on specified domains/URLs only.
  - `sendTranscriptEmailSubject` -display the chat button on specified domains/URLs only.
  - `greetingMessage` -display the chat button on specified domains/URLs only.
  - `isEnableCustomJS` -display the chat button on specified domains/URLs only.
  - `customJS` -display the chat button on specified domains/URLs only.
  Optional:  
  - `classic` - settings when `whindowThemeType` is `classic`
    + `headerType` - type of the header,including `agentInfo`、`bannerImage` and `avatarAndCompanyLogo`.
    + `agentInfo` - id of the image when any agents are on line
      * `isShowDisplayName` - id of the image when any agents are on line 
      * `isShowAvatar` - id of the image when any agents are on line 
      * `isShowTitle` - id of the image when any agents are on line 
      * `isShowBio` - id of the image when any agents are on line 
    + `bannerImage` - id of the image when any agents are on line
      * `imageType` - the type of the image ,including `gallery` and `upload`
      * `imageId` - id of the image when any agents are on line
      * `imageUrl` - url of the image when any agents are on line
    + `avatarAndCompanyLogo` - id of the image when any agents are on line
      * `isShowAvatar` - id of the image when any agents are on line
      * `isShowLogo` - url of the image when any agents are on line
      * `companyImageId` - id of the image when any agents are on line
      * `companyImageUrl` - url of the image when any agents are on line
    + `body` - id of the image when any agents are on line
      * `isShowAvatarWithMessage` - id of the image when any agents are on line
      * `isShowTextureWithMessage` - url of the image when any agents are on line
      * `backgroudImageId` - url of the image when any agents are on line
      * `backgroudImageUrl` - url of the image when any agents are on line
      * `customCSS` - url of the image when any agents are on line
  - `simple` -settings when `buttonType` is `image`
    + `headerType` - type of the header,including `agentInfo`、`bannerImage` and `avatarAndCompanyLogo`.
    + `agentInfo` - id of the image when any agents are on line
      * `isShowDisplayName` - id of the image when any agents are on line 
      * `isShowAvatar` - id of the image when any agents are on line 
      * `isShowTitle` - id of the image when any agents are on line 
      * `isShowBio` - id of the image when any agents are on line 
    + `bannerImage` - id of the image when any agents are on line
      * `imageType` - the type of the image ,including `gallery` and `upload`
      * `imageId` - id of the image when any agents are on line
      * `imageUrl` - url of the image when any agents are on line
    + `body` - id of the image when any agents are on line
      * `isShowAvatar` - id of the image when any agents are on line
      * `isShowTexture` - url of the image when any agents are on line
      * `backgroudImageId` - url of the image when any agents are on line
      * `backgroudImageUrl` - url of the image when any agents are on line
      * `customCSS` - url of the image when any agents are on line

### Example
Sample request:

  `curl -u tester@comm100.com:ef43f9362aac4f60ad428cb4d072f2c8 -X GET \`   
  `"https://hosted.comm100.com/api/v1/livechat/campaigns/2288/chatWindow"`

Sample Response:
```javascript
  {
    "themeType":"classic", 
    "themeColor": "#3AA682",
    "windowType":"popup",
    "windowTitle" :"Comm100 Live Chat - Chat Window",
    "isCanPrintChatDetail":true,
    "isShowEmail":true,
    "isUseOperatorEmailOrFromEmail":true,
    "fromEmail_email":"",
    "fromEmail_name":"",
    "isCanSwitchToOffline":false,
    "isCanSendFile":true,
    "isCanHaveAudioChat":false,
    "isCanHaveVideoChat":false,
    "isEndChatWhenVisitorInactivity":true,
    "timeEndChatDelayWhenVisitorInactivity":180,
    "isEnableSendTranscriptEmail":true,
    "sendTranscriptEmailAddress":"agentKim@gmail.com",
    "sendTranscriptEmailSubject":"Chat transcript: {!Agent.Name} with {!Visitor.Name}",
    "greetingMessage":"We are excited to chat with you!Now you can visit our forum or help desk.",
    "isEnableCustomJS":false,
    "customJS":"",
    "headerType":"avatarAndCompanyLogo",
    "isShowAvatar":true,
    "isShowLogo":false,
    "companyImageId":"",
    "companyImageUrl":"",
    "isShowAvatarWithMessage": true,
    "isShowTextureWithMessage": true,
    "backgroundImageId":"123",
    "backgroundImageUrl":"https://hosted.comm100.com/resources/img/111.ico",
    "customCSS":"",
  }     
```

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

### Example
Sample request:

  `curl –u allon@comm100.com:ef43f9362aac4f60ad428cb4d072f2c8 -X PUT -d buttonType=textLink&isHideOffline=false&isEnableDomainRestriction=false&buttonText=Chat%20Now \` 
  `"https://hosted.comm100.com/api/v1/livechat/campaigns/2288/chatButton"`

Sample Response:
```javascript
  {
    "buttonType":"textLink", 
    "textLinkSettings": {
       "buttonText": "Chat Now"
    }
    "isHideOffline":false,
    "isEnableDomainRestriction":false
  }     
```