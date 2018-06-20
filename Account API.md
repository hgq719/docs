# General

| Object | Path |
| - | - |
| [Site](#site) | `/account/site` |
| [Agent](#agent) | `/account/agents` | 
| [Group](#group) | `/account/groups` |
| [Permission](#permission) | `/account/permissions` |
| [Agent Permission](#agent-permission) | `/account/agents/{id}/permissions` |
| [Group Permission](#group-permission) | `/account/groups/{id}/permissions` |
| [Ip Restriction](#ip-restriction) | `/account/ipRestrictions` |
| [Audit Log](#audit-log) | `/livechat/auditLogs` |              

## Site
  You need `Manage Site` permission to manage site.
  - `GET /api/v1/account/site/profile` -Get profile of a single site
  - `PUT /api/v1/account/site/profile` -Update profile of a site
  - `PUT /api/v1/account/site/cancel` -Cancel the site    

### Site Profile Json Format
  Site profile is represented as simple flat JSON objects with the following keys:  

  | Name | Type | Read-only | Mandatory | Description |
  | - | - | :-: | :-: | - | 
  | id | integer | yes | no | id of the site
  | siteName | string | no | yes | name of the site
  | contact.firstName | string | no | yes |first name of the contact
  | contact.lastName | string | no | yes |last name of the contact
  | contact.mobileNumber | string | no | yes |mobile number of the contact
  | company | string | no | yes | company the site belongs to
  | website | string | no | yes | website of the site
  | phoneNumber | string | no | no | phone number of the site
  | title | string | no | no | title of the site
  | faxNumber | string | no | no | fax number of the site
  | email | string | no | no | mail address of the site
  | city | string | no | no | city which the site is in
  | stateOrProvince | string | no | no | state or provice which the site is in
  | postalOrZipCode | string | no | no | postal or zip code of the site
  | country | string | no | no | country which the site's company belongs to 
  | companySize | string | no | no | staff number of the site's company
  | timeZone | string | no | no | time zone which the site's company belongs to 
  | datetimeFormat | string | no | no | datatime format which the site will display

### Get profile of a single site

  `GET /api/v1/account/site/profile`
    
  - Parameters    
    No parameters    
      
  - Response   
    Site Profile Object
    
### Update profile of a site  

  `PUT /api/v1/account/site/profile`
    
  - Parameters    
    Site Profile Object    
      
  - Response    
    Site Profile Object
    
### Cancel the site
 
  `PUT /api/v1/account/site/cancel`
    
  + Parameters    
    - `reason` -the reason of canceling the site.
      
  - Response    
    Status: 200 OK
    
## Agent 

  + You need `Manage Agent & Agent Groups` permission to manage agent.
    - `GET /api/v1/account/agents` - Get list of agent   
    - `GET /api/v1/account/agents/{id}` - Get a single agent
    - `POST /api/v1/account/agents` - Create a new agent
    - `PUT /api/v1/account/agents/{id}` - Update an agent  
    - `DELETE /api/v1/account/agents/{id}` - Remove an agent
    - `POST /api/v1/account/agents/{id}/password` - Admin set an agent's password
    - `PUT /api/v1/account/agents/{id}/unlock` - unlock the agent
    - `GET /api/v1/account/agents/{id}/permissions` - Get list of agent's permissions. 
    - `PUT /api/v1/account/agents/{id}/permissions` - Update permissions for a agent.
    - `GET /api/v1/account/agents/{id}/effectivePermissions` -Get list of agent's effective permissions,including the permissions of the agent and the permissions of the groups which the agent belongs to. 
    
  + You can manage your own profile
    - `GET /api/v1/account/agents/me` - Get current agent
    - `PUT /api/v1/account/agents/me` - Update own profile
    - `POST /api/v1/account/agents/me/password` - Change own password

### Agent Json Format
  Agent is represented as simple flat JSON objects with the following keys:  

  | Name | Type | Read-only | Mandatory | Description |
  | - | - | :-: | :-: | - | 
  | id | integer | yes | no |id of the agent.
  | email | string | no | yes |email of the agent.
  | displayName | string | no | yes |display name of the agent.
  | firstName | string | no | yes | first name of the agent
  | lastName | string | no | yes | last name of the agent
  | title | string | no | no | title of the agent
  | bio | string | no | no | bio of the agent
  | mobilePhone | string | no | no | mobile phone number of the agent
  | timeZone | string | no | no | time zone of the agent 
  | dateTimeFormat | string | no | no| datetime format which the agent want to display in the site.
  | groups | array  | no | no | an array of group which the agent belongs to.
  | isAdmin | boolean | yes | no | whether the agent is an administrator or not.
  | isActive | boolean | yes | no | whether the agent is active or not.
  | isLocked | boolean | yes | no | whether the agent is locked or not.

### Get list of agents
 
  `GET /api/v1/account/agents`
    
  - Parameters    
    Optional:   
    - `pageIndex` -the page index of query.
      
  - Response 
    - `total` -total count of the list.
    - `previousPage` -url of the previous page.
    - `nextPage` -url of the next page.
    - `agents` -An array of Agent Json Object.
    
### Get a single agent

  `GET /api/v1/account/agents/{id}`
    
  - Parameters     
    No parameters
      
  - Response     
    Agent Object
    
### Create a new agent
  
  `POST /api/v1/account/agents`

  - Parameters     
    Agent Object
      
  - Response     
    Agent Object
    
### Update an agent

  `PUT /api/v1/account/agents/{id}`
    
  - Parameters     
    Agent Object
      
  - Response     
    Agent Object

### Remove an agent 
 
  `DELETE /api/v1/account/agents/{id}`
    
  - Parameters     
    No parameters.
      
  - Response     
    Status: 200 OK
    
### Admin set an agent's password

  `POST /api/v1/account/agents/{id}/password`
    
  - Parameters     
    - `password` - the new password of the agent.   

  - Response
    Status: 200 OK

### Unlock The Agent 

  `PUT /api/v1/account/agents/{id}/unlock`

  - Parameters     
    No parameters.
      
  - Response     
    Status: 200 OK  

### Get an agent's permissions
     
  `GET /api/v1/account/agents/{id}/permissions`
    
  - Parameters     
    No parameters
      
  - Response     

    An map of permissions group by Products
  
  ```json
  {
    "liveChat": {
      "manageCampaigns" : false,
      "managePublicCannedMessages" : false,
      "manageSettings": false,
      "manageChatbot": false,
      "manageSecurity" : false,
      "manageIntegration": false,
      "manageBan" : false,
      "manageCustomMetrics" : false,
      "viewAllHistory" : true,
      "viewHistoryInMyDepartment" : false,
      "chatWithAgents" : false,
      "viewAllAgentChats": false,
      "viewAgentChatsInMyDepartment" : false,
      "deleteHistory" : false,
      "viewReports" : false,
      "acceptChats" : true,
      "refuseChats" : false,
      "inviteVisitor" : false,
      "joinChats" : true,
      "transferChats": true,
      "monitorAllChats" : false,
      "monitorChatsInMyDepartment": false,
      "captureVisitor" : false,
      "setOtherAgentToAway" : false,
      "logOtherAgentOff" : false,
      "promoteVisitor" : false,
    },
    "account": {
      "manageAgentAndGroups": true,
      "manageBillingInfo" : false,
      "managePlan": false,
      "buyEmailMarketingCredits": false,
      "viewBalanceHistory": false,
      "manageSite": false,
      "manageHeaderAndFooterSettings": false,
      "viewAuditLog": false,
      "viewReports": false,
      "manageSecurity" : false,  
    }
  }
  ```

### Update permissions for a agent
 
  `PUT /api/v1/account/agents/{id/}/permissions`
    
- Parameters     
  An map of permissions group by Products
    
- Response     
  An map of permissions group by Products

### Get list of a agent's effective permissions

  `GET /api/v1/account/agents/{id}/effectivePermissions`

  - Parameters     
    No parameters
      
  - Response     
    An array of Agent Permission Object.

### Get current agent

  `GET /api/v1/account/agents/me`

  - Parameters
    No parameters.
  
  - Response 
    Agent Object

### Update own profile

  `PUT /api/v1/account/agents/me` 

  - Parameters 
    Agent Object

  - Response
    Agent Object

### Change own password

  `POST /api/v1/account/agents/me/password` 

  - Parameters
    - `currentPassword` - current password of curreng agent
    - `newPassword` - new password of current agent

  - Response
   Status: 200 OK
    
## Group 
  You need `Manage Agent & Agent Groups` permission to manage group.
  - `GET /api/v1/account/groups` - Get list of groups
  - `GET /api/v1/account/groups/{id}` - Get a single group
  - `POST /api/v1/account/groups` - Create a new group
  - `PUT /api/v1/account/groups/{id}` - Update a group
  - `DELETE /api/v1/account/groups/{id}` - Remove a group
  - `GET /api/v1/account/groups/{id}/permissions` - Get a group's permissions.
  - `PUT /api/v1/account/groups/{id}/permissions` - Update permissions for a group.

### Group Json Format
 Group is represented as simple flat JSON objects with the following keys:  

| Name | Type | Read-only | Mandatory | Description |
| - | - | :-: | :-: | - |
| id | integer | yes | no | id of the group. |
| isSystem | bool | yes | no | indicated that the group is maintained by the system |
| name | string | no | yes | name of the group. |
| description | string | no | no | the description of the group. |
| agents | array | no | no | an array of agents in current group. |

    
### Get list of Groups

  `GET /api/v1/account/groups`
    
  - Parameters     
    No parameters
      
  - Response     
    An array of Group Object.
    
### Get a single group

  `GET /api/v1/account/groups/{id}`
    
  - Parameters     
    No parameters
      
  - Response     
    Group Object
    
### Create a new group
  
  `POST /api/v1/account/groups`
    
  - Parameters     
    Group Object
    
  - Response     
    Group Object
    
### Update a group

  `PUT /api/v1/account/groups/{id}`
    
  - Parameters     
    Group Object
          
  - Response     
    Group Object
      
### Remove a group 
 
  `DELETE /api/v1/account/groups/{id}`
    
  - Parameters     
    No parameters.
      
  - Response     
    Status: 200 OK    
    
### Get a group's permissions
- End Point     
  `GET /api/v1/account/groups/{id}/permissions`
    
- Parameters     
  No parameters
    
- Response     
  An map of permissions group by Products
    
### Update permissions for a group
- End Point     
  `PUT /api/v1/account/groups/{id/}/permissions`
    
- Parameters     
  An map of permissions group by Products
    
- Response     
  An map of permissions group by Products
    
## IP Restriction
  You need `Manage Security` permission to manage ip restrictions.
  - `GET /api/v1/account/ipRestriction` - Get configuration of ip restrictions 
  - `PUT /api/v1/account/ipRestriction` - Update configuration of ip restrictions 
  - `GET /api/v1/account/ipRestriction/ipRanges` - Get authorized ip range list of ip restriction
  - `PUT /api/v1/account/ipRestriction/ipRanges` - Update an authorized ip range
  - `POST /api/v1/account/ipRestriction/ipRanges/{id} ` - Create a new ip range of ip restriction
  - `DELETE /api/v1/account/ipRestriction/ipRanges/{id} ` - Remove a ip range of ip restriction

### IP Restriction Config Json Format
 Ip Restrictions is represented as simple flat JSON objects with the following keys:  

| Name | Type | Read-only | Mandatory |  Description |         
| - | - | - | - | - | 
| isEnable | boolean | no | no | whether IP Restrictions is enable or not. |
| isEnableForMobile | boolean | no | no | whether IP Restrictions is enable or not for mobile app access. |
    
### Get configuration of ip restriction

  `Get /api/v1/account/ipRestriction`

  - Parameters     
    No parameters.

  - Response     
    IP Restriction Config Object.

### Update configuration of ip restriction

  `PUT /api/v1/account/ipRestriction`

  - Parameters     
    IP Restriction Config Object.

  - Response     
    IP Restriction Config Object.

### Ip Range Json Format
  Ip Range is represented as simple flat JSON objects with the following keys:  

  | Name | Type | Read-only | Mandatory | Description |                    
  | - | - | :-: | :-: | - | 
  | id | integer  | yes | no | id of ip range. |
  | from | string  | no | yes | ip which ip range start from. |
  | to | string  | no | yes | ip which ip range end to. |
    
### Get ip range list of ip restriction
  
  `Get /api/v1/account/ipRestriction/ipRanges`

  - Parameters
    No parameters

  - Response
    An array of Ip Range Json Object.

### Create a new ip range of ip restrictions

  `POST /api/v1/account/ipRestriction/ipRanges/{id} `

  - Parameters
      Ip Range Json Object.

  - Response
      Ip Range Json Object.

### Remove a ip range of ip restriction

  `DELETE /api/v1/account/ipRestriction/ipRanges/{id} `

  - Parameters
    No parameters.

  - Response
    Status: 200 OK

## Audit Log
  You need `View Audit Log` permission to view audit logs.
  + `Get /api/v1/account/auditLogs` - Get audit Logs list.
    
### Get audit Logs list 

  `Get /api/v1/account/auditLogs`

  - Parameters
    - `dateFrom` - the date from which agent do the action.
    - `dateTo` - the date end which agent do the action.   
    optional：
    - `product` - the product which the action belongs to, including `liveChat` and `account`.
    - `type` - the type of the action.
    - `agentId` - id of the agent who do the action.
    - `keywords` - the key words of inquiring the action
    - `pageIndex` -the page index of query.
      
  - Response
    - `total` -total count of the list.
    - `previousPage` -url of the previous page.
    - `nextPage` -url of the next page.
    - `logs` -audit log list
      + `id` -id of the config.
      + `actionTime` -the time of the action.
      + `agentName` - the agent which do the action.
      + `product` - the module which the action belongs to.
      + `actionType` - the type of the action.
      + `actionSummary` - the summary of the action.
