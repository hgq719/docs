# General
|Object     | Path               | Support                                                                                                   
| ------------- |------------------------------- | -------------------------------------- 
| [Site Profile](#site-profile)   |/account/sites/{site_id}/profile                    | 1       
| [Agent](#agent)       |/account/agents                    | 1       
| [Group](#group)        |/account/groups                    | 1       
| [Permission](#permission)        |/account/permissions                    | 1       
| [Agent Permission](#agent-permission)  |/account/agents/{id}/permissions                    | 1       
| [Group Permission](#group-permission)  |/account/groups/{id}/permissions                    | 1              
| [Ip Restriction](#ip-restriction)   |/account/ipRestrictions                    | 1      
| [Audit Log](#audit-log) |/livechat/auditLogs                    | 1                

## Site Profile
  You need `Manage Site Profile` permission to manage site.
  - `GET /api/v1/account/sites/{id}/profile` -Get profile of a single site
  - `PUT /api/v1/account/sites/{id}/profile` -Update profile of a site
  - `PUT /api/v1/account/sites/{id}/cancel` -Cancel the site

### Site Profile Json Format
 Site profile is represented as simple flat JSON objects with the following keys:  

|name     | Type               | Read-only    | Mandatory      |  Description                                                                                                   
| ------------- |--------------------- | ---------- | -------------------- | ------------------ 
| id | integer  | yes  | no| id of the site
| siteName| string  | no  | yes|name of the site
| contact.firstName| string  | no  | yes|first name of the contact
| contact.lastName| string  | no  | yes|last name of the contact
| contact.email| string  | no  | yes|email of the contact
| contact.mobileNumber| string  | no  | yes|mobile number of the contact
| company| string  | no  | yes| company the site belongs to
| website| string  | no  | yes| website of the site
| phoneNumber| string  | no  | no| phone number of the site
| title| string  | no | no | title of the site
| faxNumber| string  | no | no | fax number of the site
| mailAddress| string  | no | no | mail address of the site
| city| string  | no | no | city which the site is in
| stateOrProvince| string  | no | no | state or provice which the site is in
| postalOrZipCode| string  | no | no | postal or zip code of the site
| country| string  | no | no | country which the site's company belongs to 
| companySize| string  | no | no | staff number of the site's company
| timeZone| string  | no | no | time zone which the site's company belongs to 
| datetimeFormat| string  | no | no | datatime format which the site will display

### Get profile of a single site
- End Point   
  `GET /api/v1/account/sites/{site_id}/profile`
    
- Parameters    
  No parameters    
    
- Response   
 Site Profile Json Object
    
### Update profile of a site  
- End Point    
  `PUT /api/v1/account/site/{site_id}/profile`
    
- Parameters    
 Site Profile Json Object    
    
- Response    
 Site Profile Json Object
    
### Cancel the site
- End Point    
  `PUT /api/v1/account/sites/{site_id}/cancel`
    
- Parameters    
  + `reason` -the reason of canceling the site.
    
- Response    
  Status: 200 OK
    
## Agent 
  You need `Manage Agent & Agent Groups` permission to manage agent.
  - `GET /api/v1/account/agents` -Get list of agent   
  - `GET /api/v1/account/agents/{id}` -Get a single agent
  - `POST /api/v1/account/agents` -Create a new agent
  - `PUT /api/v1/account/agents/{id}` -Update an agent  
  - `PUT /api/v1/account/agents/{id}/reset_api_key` -Reset an API key   
  - `PUT /api/v1/account/agents/{id}/changePassword` -Change password   
  - `PUT /api/v1/account/agents/{id}/unlock` -unlock the agent   
  - `DELETE /api/v1/account/agents/{id}` -Remove an agent

### Agent Json Format
 Agent is represented as simple flat JSON objects with the following keys:  

|name     | Type               | Read-only    | Mandatory      |  Description                                                                                                   
| ------------- |--------------------- | ---------- | -------------------- | ------------------ 
|id | integer  | yes  | no|id of the agent.
|displayName| string  | no  | yes|display name of the agent.
|email| string  | no  | yes|email of the agent.
|firstName| string  | no  | yes| first name of the agent
|lastName| string  | no  | yes| last name of the agent
|title| string  | no  | no| title of the agent
|bio| string  | no  | no| bio of the agent
|mobilePhone| string  | no  | no| mobile phone number of the agent
|timeZone| string  | no  | no| time zone of the agent 
|dateTimeFormat| string  | no  | no| datetime format which the agent want to display in the site.
|groups| Array  | no  | no| an array of group which the agent belongs to.
|isAdmin| boolean  | yes  | no| whether the agent is an administrator or not.
|isActive| boolean  | yes  | no| whether the agent is active or not.
|isLocked| boolean  | yes  | no| whether the agent is locked or not.
|apikey| string  | yes  | no| the key by which you can exchange the token when calling restful api

### Get list of agents
- End Point    
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
- End Point     
  `GET /api/v1/account/agents/{id}`
    
- Parameters     
  No parameters
    
- Response     
Agent Json Object
    
### Create a new agent
- End Point     
  `POST /api/v1/account/agents`
    
- Parameters     
  Agent Json Object
    
- Response     
  Agent Json Object
    
### Update an agent
- End Point     
  `PUT /api/v1/account/agents/{id}`
    
- Parameters     
  Agent Json Object
    
- Response     
  Agent Json Object
    
### Reset API Key 
- End Point     
  `PUT /api/v1/account/agents/{id}/reset_api_key`
    
- Parameters     
  No parameters.
    
- Response     
  Agent Json Object

### Change Password 
- End Point     
  `PUT /api/v1/account/agents/{id}/changePassword`
    
- Parameters     
  - `oldPassword` - the old password of the agent.
  - `newPassword` - the new password of the agent.   
    
- Response     
  Status: 200 OK  

### Unlock The Agent 
- End Point     
  `PUT /api/v1/account/agents/{id}/unlock`
    
- Parameters     
  No parameters.
    
- Response     
  Status: 200 OK  

### Remove an agent 
- End Point     
  `DELETE /api/v1/account/agents/{id}`
    
- Parameters     
  No parameters.
    
- Response     
  Status: 200 OK    
    
## Group 
  You need `Manage Agent & Agent Groups` permission to manage group.
  - `GET /api/v1/account/groups` -Get list of groups
  - `GET /api/v1/account/groups/{id}` -Get a single group
  - `POST /api/v1/account/groups` -Create a new group
  - `PUT /api/v1/account/groups/{id}` -Update a group  
  - `DELETE /api/v1/account/groups/{id}` -Remove a group

### Group Json Format
 Group is represented as simple flat JSON objects with the following keys:  

|name     | Type               | Read-only    | Mandatory      |  Description                                                                                                   
| ------------- |--------------------- | ---------- | -------------------- | ------------------ 
|id | integer  | yes  | no|id of the group.
|name | string  | no  | yes|name of the group.
|description | string  | no  | no|the description of the group.
|agents | array  | no  | no|an array of agents in current group
    
### Get list of Groups
- End Point     
  `GET /api/v1/account/groups`
    
- Parameters     
  No parameters
    
- Response     
 An array of Group Json Object.
    
### Get a single group
- End Point     
  `GET /api/v1/account/groups/{id}`
    
- Parameters     
  No parameters
    
- Response     
 Group Json Object
    
### Create a new group
- End Point     
  `POST /api/v1/account/groups`
    
- Parameters     
 Group Json Object
    
- Response     
 Group Json Object
    
### Update a group
- End Point     
  `PUT /api/v1/account/groups/{id}`
    
- Parameters     
 Group Json Object
        
- Response     
 Group Json Object
    
### Remove a group 
- End Point     
  `DELETE /api/v1/account/groups/{id}`
    
- Parameters     
  No parameters.
    
- Response     
  Status: 200 OK    
    
## Permission 
  You need `Manage Agent & Agent Groups` permission to manage permission.
  - `GET /api/v1/account/permissions` -Get list of permissions  
    
### Permission Json Format
 Permission is represented as simple flat JSON objects with the following keys:  

|name     | Type               | Read-only    | Mandatory      |  Description                                                                                                   
| ------------- |--------------------- | ---------- | -------------------- | ------------------ 
|name | string  | no  | yes|name of the permission.
|description | string  | no  | no|the description of the permission.
|module | string  | no  | yes|module which the permission belongs to,including `LiveChat`、`UserAndContact` and `Account`.
    
### Get list of permissions
- End Point     
  `GET /api/v1/account/permissions`
    
- Parameters     
  No parameters
    
- Response     
  An array of Permission Json Object.
    
## Agent Permission 
  You need `Manage Agent & Agent Groups` permission to manage permission of agent.
  - `GET /api/v1/account/agents/{id}/permissions` -Get list of agent's permissions. 
  - `GET /api/v1/account/agents/{id}/effectivePermissions` -Get list of agent's effective permissions,including the permissions of the agent and the permissions of the groups which the agent belongs to. 
  - `PUT /api/v1/account/agents/{id}/permissions` -Update permissions for a agent.
    
### Agent Permission Json Format
 Agent Permission is represented as simple flat JSON objects with the following keys:  

|name     | Type               | Read-only    | Mandatory      |  Description                                                                                                   
| ------------- |--------------------- | ---------- | -------------------- | ------------------ 
|name | string  | no  | yes|name of the permission.
|module | string  | no  | yes|module which the permission belongs to,including `LiveChat`、`UserAndContact` and `Account`.
    
### Get list of a agent's permissions
- End Point     
  `GET /api/v1/account/agents/{id}/permissions`
    
- Parameters     
  No parameters
    
- Response     
  An array of Agent Permission Json Object.

### Get list of a agent's effective permissions
- End Point     
  `GET /api/v1/account/agents/{id}/effectivePermissions`
    
- Parameters     
  No parameters
    
- Response     
  An array of Agent Permission Json Object.
    
### Update permissions for a agent
- End Point     
  `PUT /api/v1/account/agents/{id/}/permissions`
    
- Parameters     
Agent Permission Json Object
    
- Response     
Agent Permission Json Object
    
## Group Permission 
  You need `Manage Agent & Agent Groups` permission to manage permission of group.
  - `GET /api/v1/account/groups/{id}/permissions` -Get list of group's permissions.
  - `PUT /api/v1/account/groups/{id}/permissions` -Update permissions for a group.
    
### Group Permission Json Format
 Group Permission is represented as simple flat JSON objects with the following keys:  

|name     | Type               | Read-only    | Mandatory      |  Description                                                                                                   
| ------------- |--------------------- | ---------- | -------------------- | ------------------ 
|name | string  | no  | yes|name of the permission.
|module | string  | no  | yes|module of the permission belong to,including `LiveChat`、`UserAndContact` and `Account`.
    
### Get list of a group's permissions
- End Point     
  `GET /api/v1/account/groups/{id}/permissions`
    
- Parameters     
  No parameters
    
- Response     
  An array of Group Permission Json Object.
    
### Update permissions for a group
- End Point     
  `PUT /api/v1/account/groups/{id/}/permissions`
    
- Parameters     
  Group Permission Json Object.
    
- Response     
  Group Permission Json Object . 
    
## Ip Restriction
  You need `Manage Security` permission to manage ip restrictions.
  - `Get /api/v1/account/ipRestrictions/ipRanges` -Get ip range list of ip restrictions 
  - `POST /api/v1/account/ipRestrictions/ipRanges/{id} ` -Create a new ip range of ip restrictions 
  - `DELETE /api/v1/account/ipRestrictions/ipRanges/{id} ` -Remove a ip range of ip restrictions 
  - `Get /api/v1/account/ipRestrictions/config` -Get configuration of ip restrictions 
  - `PUT /api/v1/account/ipRestrictions/config` -Update configuration of ip restrictions 
    
### Ip Range Json Format
 Ip Range is represented as simple flat JSON objects with the following keys:  

|name     | Type               | Read-only    | Mandatory      |  Description                                                                                                   
| ------------- |--------------------- | ---------- | -------------------- | ------------------ 
|id | integer  | yes  | no|id of ip range.
|ipFrom | string  | no  | yes|ip which ip range start from.
|ipTo | string  | no  | yes|ip which ip range end to.
    
### Get ip range list of ip restrictions
- End Point     
  `Get /api/v1/account/ipRestrictions/ipRanges`
    
- Parameters     
  No parameters
    
- Response     
  An array of Ip Range Json Object.
    
### Create a new ip range of ip restrictions 
- End Point     
  `POST /api/v1/account/ipRestrictions/ipRanges/{id} `
    
- Parameters     
    Ip Range Json Object.
    
- Response     
    Ip Range Json Object.
    
### Remove a ip range of ip restrictions
- End Point     
  `DELETE /api/v1/account/ipRestrictions/ipRanges/{id} `
    
- Parameters     
  No parameters.
    
- Response     
  Status: 200 OK    
    
### Ip Restrictions Json Format
 Ip Restrictions is represented as simple flat JSON objects with the following keys:  

|name     | Type               | Read-only    | Mandatory      |  Description                                                                                                   
| ------------- |--------------------- | ---------- | -------------------- | ------------------ 
|isEnable | boolean  | no  | no|whether IP Restrictions is enable or not.
|isEnableForMobile | boolean  | no  | no|whether IP Restrictions is enable or not for mobile access.
    
### Get configuration of ip restrictions 
- End Point     
  `Get /api/v1/account/ipRestrictions/config`
    
- Parameters     
  No parameters.
    
- Response     
  Ip Restrictions Json Object.
    
### Update configuration of ip restrictions 
- End Point     
  `PUT /api/v1/account/ipRestrictions/config`
    
- Parameters     
  Ip Restrictions Json Object.
    
- Response     
  Ip Restrictions Json Object.
    
## Audit Log
  You need `View Audit Log` permission to view audit logs.
  + `Get /api/v1/account/auditLogs` -Get audit Logs list.
    
### Get audit Logs list 
- End Point     
  `Get /api/v1/account/auditLogs`
    
- Parameters     
  - `dateFrom` - the date from which agent do the action.
  - `dateTo` - the date end which agent do the action.   
  optional：
  - `product` - the product which the action belongs to, including `liveChat`、`userContact` and `account`.
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
    + `application` - the module which the action belongs to.
    + `actionType` - the type of the action.
    + `actionSummary` - the summary of the action.

