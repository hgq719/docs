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
| firstName| string  | no  | yes|first name of the site
| lastName| string  | no  | yes|last name of the site
| company| string  | no  | yes| company the site belongs to
| website| string  | no  | yes| website of the site
| phoneNumber| string  | no  | no| phone number of the site
| mobileNumber| string  | no  | no| mobile number of the site
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
  - `GET /api/v1/account/agents/{agent_email}` -Get a single agent
  - `POST /api/v1/account/agents` -Create a new agent
  - `PUT /api/v1/account/agents/{id}` -Update an agent  
  - `PUT /api/v1/account/agents/{id}/reset_api_key` -Reset an API key   
  - `DELETE /api/v1/account/agents/{id}` -Remove an agent

### Agent Json Format
 Agent is represented as simple flat JSON objects with the following keys:  

|name     | Type               | Read-only    | Mandatory      |  Description                                                                                                   
| ------------- |--------------------- | ---------- | -------------------- | ------------------ 
|id | integer  | yes  | no|id of the agent.
|displayName| string  | no  | yes|display name of the agent.
|email| string  | no  | yes|email of the agent.
|status| string  | yes  | no| status of the agent, including online、away、offline
|ongoing_chats| string  | yes  | no| total number of ongoing chats the agent has
|departments| string  | yes  | no| departments the agent belongs to
|max_chats_count| integer  | no  | no| the maximum number of concurrent chats that will be automatically routed to the agent when Auto Accept Chat Requests is enabled
|api_key| string  | yes  | no| the key by which you can exchange the token when calling restful api
|first_name| string  | no  | yes| first name of the agent
|last_name| string  | no  | yes| last name of the agent
|phone| string  | no  | no| phone of the agent
|title| string  | no  | no| title of the agent
|description| string  | no  | no| description of the agent
|is_admin| boolean  | yes  | no| whether the agent is an administrator or not.
|is_active| boolean  | yes  | no| whether the agent is active or not.
|
### Get list of agents
- End Point    
  `GET /api/v1/account/agents`
    
- Parameters    
  No parameters
    
- Response    
  An array of Agent Json Object.
    
### Get a single agent
- End Point     
  `GET /api/v1/account/agents/{agent_email}`
    
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
  `PUT /api/v1/account/agents/{agent_email}`
    
- Parameters     
  Agent Json Object
    
- Response     
  Agent Json Object
    
### Reset API Key 
- End Point     
  `PUT /api/v1/account/agents/{agent_email}/reset_api_key`
    
- Parameters     
  No parameters.
    
- Response     
  Agent Json Object
    
### Remove an agent 
- End Point     
  `DELETE /api/v1/account/agents/{agent_email}`
    
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
|id | integer  | yes  | no|id of the permission.
|name | string  | no  | yes|name of the permission.
|description | string  | no  | no|the description of the permission.
|module | string  | no  | yes|module of the permission belong to.
    
### Get list of permissions
- End Point     
  `GET /api/v1/account/permissions`
    
- Parameters     
  No parameters
    
- Response     
  An array of Permission Json Object.
    
## Agent Permission 
  You need `Manage Agent & Agent Groups` permission to manage permission of agent.
  - `GET /api/v1/account/agents/{id}/permissions` -Get list of agent's permissions 
  - `POST /api/v1/account/agents/{id}/permissions` -Create a new permission for a agent
  - `DELETE /api/v1/account/agents/{id}/permissions/{permission_id}` -Remove a permission for a agent
    
### Agent Permission Json Format
 Agent Permission is represented as simple flat JSON objects with the following keys:  

|name     | Type               | Read-only    | Mandatory      |  Description                                                                                                   
| ------------- |--------------------- | ---------- | -------------------- | ------------------ 
|permission_id | integer  | yes  | yes|id of the permission.
|agent_id | integer  | yes  | no|id of the agent.
|module | string  | no  | yes|module of the permission belong to.
    
### Get list of a agent's permissions
- End Point     
  `GET /api/v1/account/agents/{id}/permissions`
    
- Parameters     
  No parameters
    
- Response     
  An array of Agent Permission Json Object.
    
### Create a new permission for a agent
- End Point     
  `POST /api/v1/account/agents/{agent_id/}/permissions`
    
- Parameters     
Agent Permission Json Object
    
- Response     
Agent Permission Json Object
    
### Remove a permission for a agent
- End Point     
  `DELETE /api/v1/account/agents/{id}/permissions/{permission_id}`
    
- Parameters     
  No parameters.
    
- Response     
  Status: 200 OK    
    
## Group Permission 
  You need `Manage Agent & Agent Groups` permission to manage permission of group.
  - `GET /api/v1/account/groups/{id}/permissions` -Get list of group's permissions
  - `POST /api/v1/account/groups/{id}/permissions` -Create a new permission for a group
  - `DELETE /api/v1/account/groups/{id}/permissions/{id}` -Remove a permission for a group
    
### Group Permission Json Format
 Group Permission is represented as simple flat JSON objects with the following keys:  

|name     | Type               | Read-only    | Mandatory      |  Description                                                                                                   
| ------------- |--------------------- | ---------- | -------------------- | ------------------ 
|permission_id | integer  | yes  | yes|id of the permission.
|group_id | integer  | yes  | no|id of the group.
|module | string  | no  | yes|module of the permission belong to.
    
### Get list of a group's permissions
- End Point     
  `GET /api/v1/account/groups/{id}/permissions`
    
- Parameters     
  No parameters
    
- Response     
  An array of Group Permission Json Object.
    
### Create a new permission for a group
- End Point     
  `POST /api/v1/account/groups/{groups_id/}/permissions`
    
- Parameters     
  Group Permission Json Object
    
- Response     
  Group Permission Json Object
    
### Remove a permission for a group
- End Point     
  `DELETE /api/v1/account/groups/{groups_id}/permissions/{id}`
    
- Parameters     
  No parameters.
    
- Response     
  Status: 200 OK    
    
## Ip Restriction
  You need `Manage Security` permission to manage ip restrictions.
  - `Get /api/v1/account/ipRestrictions/ipRanges` -Get ip range list of ip restrictions 
  - `POST /api/v1/account/ipRestrictions/ipRanges/{id} ` -Update a ip range of ip restrictions 
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
    
### Update a ip range of ip restrictions 
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
|id | integer  | yes  | no|id of the config.
|siteId | integer  | yes  | yes|id of the site.
|isEnable | boolean  | no  | yes|whether IP Restrictions is enable or not.
|isEnableForMobile | boolean  | no  | yes|whether IP Restrictions is enable or not for mobile access.
    
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
  + `Get /api/v1/account/auditLogs` -Get audit Logs list 
  + `Get /api/v1/account/auditLogs/{log_id}` -Get a single audit log 
    
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
    
### Get a single audit log 
- End Point     
  `Get /api/v1/account/auditLogs/{log_id}`
    
- Parameters     
  No parameters.
    
- Response     
  - `id` -id of the config.
  - `actionTime` -the time of the action.
  - `agentName` - the agent which do the action.
  - `application` - the module which the action belongs to.
  - `actionType` - the type of the action.
  - `actionSummary` - the summary of the action.
  - `fields` - the field which is changed in the action.
    + `fidldName` - name of the field.
    + `valueBefore` - value of the field before doing the action.
    + `valueAfter` -value of the field after doing the action.
