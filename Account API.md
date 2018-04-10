# General
|Object     | Path               | Support                                                                                                   
| ------------- |------------------------------- | -------------------------------------- 
| Site        |/account/sites/{site_id}/profile                    | 1       
| Agent       |/account/agents                    | 1       
| Group        |/account/groups                    | 1       
| Permission        |/account/permissions                    | 1       
| Agent Permission  |/account/agents/{agent_id}/permissions                    | 1       
| Group Permission  |/account/groups/{group_id}/permissions                    | 1              
| Ip Restrictions   |/account/ipRestrictions                    | 1      
| Audit Logs |/livechat/auditLogs                    | 1                

## Account API
  You need `Manage Site Profile` permission to manage site.
  - `Site` -Site Manage
    + `GET /api/v1/account/sites/{site_id}/profile` -Get profile of a single site
    + `PUT /api/v1/account/sites/{site_id}/profile` -Update profile of a site
    + `PUT /api/v1/account/sites/{site_id}/cancel` -Cancel the site
     
  You need `Manage Agent & Agent Groups` permission to manage agent、group and permission.
  - `Agent` -Agent Manage
    + `GET /api/v1/account/agents` -Get list of agent   
    + `GET /api/v1/account/agents/{agent_email}` -Get a single agent
    + `POST /api/v1/account/agents` -Create a new agent
    + `PUT /api/v1/account/agents/{agent_id}` -Update an agent  
    + `PUT /api/v1/account/agents/{agent_id}/reset_api_key` -Reset an API key   
    + `DELETE /api/v1/account/agents/{agent_id}` -Remove an agent
  - `Group` -Group Manage
    + `GET /api/v1/account/groups` -Get list of groups
    + `GET /api/v1/account/groups/{group_id}` -Get a single group
    + `POST /api/v1/account/groups` -Create a new group
    + `PUT /api/v1/account/groups/{group_id}` -Update a group  
    + `DELETE /api/v1/account/groups/{group_id}` -Remove a group
  - `Permission` - Permission Manage
    + `GET /api/v1/account/permissions` -Get list of permission  
    + `GET /api/v1/account/permissions/{permission_id}` -Get a single permission
    + `POST /api/v1/account/permissions` -Create a new permission
    + `PUT /api/v1/account/permissions/{permission_id}` -Update a permission
    + `DELETE /api/v1/account/permissions/{permission_id}` -Remove a permission
  - `Agent Permission` -Agent's Permission Manage
    + `GET /api/v1/account/agents/{agent_id}/permissions` -Get list of agent's permission 
    + `POST /api/v1/account/agents/{agent_id}/permissions` -Create a new permission for a agent
    + `DELETE /api/v1/account/agents/{agent_id}/permissions/{permission_id}` -Remove a permission for a agent
  - `Group Permission` -Group's Permission Manage
    + `GET /api/v1/account/groups/{group_id}/permissions` -Get list of group's permission
    + `POST /api/v1/account/groups/{group_id}/permissions` -Create a new permission for a group
    + `DELETE /api/v1/account/groups/{group_id}/permissions/{permission_id}` -Remove a permission for a group
      
  You need `Manage Security` permission to manage ip restrictions.
  - `IP Restrictions` -IP Restrictions Manage
    + `Get /api/v1/account/ipRestrictions/ipRanges` -Get ip range list of ip restrictions 
    + `POST /api/v1/account/ipRestrictions/ipRanges/{rang_id}` -Update a ip range of ip restrictions 
    + `DELETE /api/v1/account/ipRestrictions/ipRanges/{rang_id}` -Remove a ip range of ip restrictions 
    + `Get /api/v1/account/ipRestrictions/config` -Get configuration of ip restrictions 
    + `PUT /api/v1/account/ipRestrictions/config` -Update configuration of ip restrictions 
    
  You need `View Audit Log` permission to view audit logs.
  + `Get /api/v1/account/auditLogs` -Get audit Logs list 
  + `Get /api/v1/account/auditLogs/{log_id}` -Get a single audit log 

## Get profile of a single site
### End Point
  `GET /api/v1/account/sites/{site_id}/profile`

### Parameters
  No parameters

### Response
  - `id ` -id of the site.
  - `siteName` -name of the site.
  - `firstName` -first name of the site.
  - `lastName` -last name of the site.
  - `company` - company the site belongs to
  - `website` - website of the site
  - `phoneNumber` - phone number of the site
  - `mobileNumber` - mobile number of the site
  - `title` - title of the site
  - `faxNumber` - fax number of the site
  - `mailAddress` - mail address of the site
  - `city` - city which the site is in
  - `stateOrProvince` - state or provice which the site is in
  - `postalOrZipCode` - postal or zip code of the site
  - `country` - country which the site's company belongs to 
  - `companySize` - staff number of the site's company
  - `timeZone` - time zone which the site's company belongs to 
  - `datetimeFormat` - datatime format which the site will display

## Update profile of a site  
### End Point
  `PUT /api/v1/account/site/{site_id}/profile`

### Parameters
  Required parameters:
  - `siteName` -name of the site.
  - `firstName` -first name of the site.
  - `lastName` -last name of the site.
  - `company` - company the site belongs to
  - `website` - website of the site
  Optional parameters:
  - `phoneNumber` - phone number of the site
  - `mobileNumber` - mobile number of the site
  - `title` - title of the site
  - `faxNumber` - fax number of the site
  - `mailAddress` - mail address of the site
  - `city` - city which the site is in
  - `stateOrProvince` - state or provice which the site is in
  - `postalOrZipCode` - postal or zip code of the site
  - `country` - country which the site's company belongs to 
  - `companySize` - staff number of the site's company
  - `timeZone` - time zone which the site's company belongs to 
  - `datetimeFormat` - datatime format which the site will display

### Response
  - `id ` -id of the site.
  - `siteName` -name of the site.
  - `firstName` -first name of the site.
  - `lastName` -last name of the site.
  - `company` - company the site belongs to
  - `website` - website of the site
  - `phoneNumber` - phone number of the site
  - `mobileNumber` - mobile number of the site
  - `title` - title of the site
  - `faxNumber` - fax number of the site
  - `mailAddress` - mail address of the site
  - `city` - city which the site is in
  - `stateOrProvince` - state or provice which the site is in
  - `postalOrZipCode` - postal or zip code of the site
  - `country` - country which the site's company belongs to 
  - `companySize` - staff number of the site's company
  - `timeZone` - time zone which the site's company belongs to 
  - `datetimeFormat` - datatime format which the site will display

## Cancel the site
### End Point
  `PUT /api/v1/account/sites/{site_id}/cancel`

### Parameters
  - `reason` -the reason of canceling the site.

### Response
  - `result ` -the result of operating

## Get list of agents
### End Point
  `GET /api/v1/account/agents`

### Parameters
  No parameters

### Response
  Agent list, including
  - `id ` -id of the agent.
  - `displayName` -display name of the agent.
  - `email` -email of the agent.
  - `status` - status of the agent, including online、away、offline
  - `ongoing_chats` - total number of ongoing chats the agent has
  - `departments` - departments the agent belongs to
  - `max_chats_count` - the maximum number of concurrent chats that will be automatically routed to the agent when Auto Accept Chat Requests is enabled

## Get a single agent
### End Point
  `GET /api/v1/account/agents/{agent_email}`

### Parameters
  No parameters

### Response
  - `id ` -id of the agent.
  - `displayName` -display name of the agent.
  - `email` -email of the agent.
  - `status` - status of the agent, including online、away、offline
  - `ongoing_chats` - total number of ongoing chats the agent has
  - `departments` - departments the agent belongs to
  - `max_chats_count` - the maximum number of concurrent chats that will be automatically routed to the agent when Auto Accept Chat Requests is enabled
  - `api_key` - the key by which you can exchange the token when calling restful api
  - `first_name` - first name of the agent
  - `last_name` - last name of the agent
  - `phone` - phone of the agent
  - `title` - title of the agent
  - `description` - description of the agent
  - `is_admin` - whether the agent is an administrator
  - `is_active` - whether the agent is active

## Create a new agent
### End Point
  `POST /api/v1/account/agents`

### Parameters
  Required parameters:
  - `email` - email of the agent, (Email must be unique)
  - `password` - password of the agent
  - `display_name` - display name of the agent
  - `first_name` - first name of the agent
  - `last_name` - last name of the agent
  Optional parameters:  
  - `phone` - defaults to null
  - `title` - defaults to null
  - `description` - defaults to null
  - `is_admin` - defaults to false.
  - `is_active` - defaults to true.
  - `depsrtments` - defaults to null
  - `max_chats_count` - defaults to 3. Note: This setting only works when you separately set max chat count for each agent. If you set the max chat count together for all agents, you need to set in your Comm100 account.

### Response
  - `id ` -id of the agent.
  - `displayName` -display name of the agent.
  - `email` -email of the agent.
  - `status` - status of the agent, including online、away、offline
  - `ongoing_chats` - total number of ongoing chats the agent has
  - `departments` - departments the agent belongs to
  - `max_chats_count` - the maximum number of concurrent chats that will be automatically routed to the agent when Auto Accept Chat Requests is enabled
  - `api_key` - the key by which you can exchange the token when calling restful api
  - `first_name` - first name of the agent
  - `last_name` - last name of the agent
  - `phone` - phone of the agent
  - `title` - title of the agent
  - `description` - description of the agent
  - `is_admin` - whether the agent is an administrator
  - `is_active` - whether the agent is active

## Update an agent
### End Point
  `PUT /api/v1/account/agents/{agent_email}`

### Parameters
  Optional parameters:
  - `display_name` - display name of the agent, which is shown in the chat window
  - `first_name` - first name of the agent
  - `last_name` - last name of the agent
  - `phone` - defaults to null
  - `title` - defaults to null
  - `description` - defaults to null
  - `is_admin` - defaults to false.
  - `is_active` - defaults to true.
  - `departments` - defaults to null
  - `max_chats_count` - defaults to 3. Note: This setting only works when you separately set max chat count for each agent. If you set the max chat count together for all agents, you need to set in your Comm100 account.
  - `status` - status of the agent (online, away or offline)

### Response
  - `id ` -id of the agent.
  - `displayName` -display name of the agent.
  - `email` -email of the agent.
  - `status` - status of the agent, including online、away、offline
  - `ongoing_chats` - total number of ongoing chats the agent has
  - `departments` - departments the agent belongs to
  - `max_chats_count` - the maximum number of concurrent chats that will be automatically routed to the agent when Auto Accept Chat Requests is enabled
  - `api_key` - the key by which you can exchange the token when calling restful api
  - `first_name` - first name of the agent
  - `last_name` - last name of the agent
  - `phone` - phone of the agent
  - `title` - title of the agent
  - `description` - description of the agent
  - `is_admin` - whether the agent is an administrator
  - `is_active` - whether the agent is active

## Reset API Key 
### End Point
  `PUT /api/v1/account/agents/{agent_email}/reset_api_key`

### Parameters
  No parameters.

### Response
  - `id ` -id of the agent.
  - `displayName` -display name of the agent.
  - `email` -email of the agent.
  - `status` - status of the agent, including online、away、offline
  - `ongoing_chats` - total number of ongoing chats the agent has
  - `departments` - departments the agent belongs to
  - `max_chats_count` - the maximum number of concurrent chats that will be automatically routed to the agent when Auto Accept Chat Requests is enabled
  - `api_key` - the key by which you can exchange the token when calling restful api
  - `first_name` - first name of the agent
  - `last_name` - last name of the agent
  - `phone` - phone of the agent
  - `title` - title of the agent
  - `description` - description of the agent
  - `is_admin` - whether the agent is an administrator
  - `is_active` - whether the agent is active

## Remove an agent 
### End Point
  `DELETE /api/v1/account/agents/{agent_email}`

### Parameters
  No parameters.

### Response
  - `result ` -the result of operating

## Get list of Groups
### End Point
  `GET /api/v1/account/groups`

### Parameters
  No parameters

### Response
  Group list, including
  - `id ` -id of the group.
  - `name` -name of the group.
  - `description` -the description of the group.

## Get a single group
### End Point
  `GET /api/v1/account/groups/{group_id}`

### Parameters
  No parameters

### Response
  - `id ` -id of the group.
  - `name` -name of the group.
  - `description` -description of the group.
  - `agents` - list of agents in current group
    + `agent_id` -id of the agent
    + `email` -email of the agent

## Create a new group
### End Point
  `POST /api/v1/account/groups`

### Parameters
  - `name` -name of the group.
  - `description` -description of the group.
  - `agents` - id list of agents in current group
    + `agent_id` -id of the agent
    + `email` -email of the agent

### Response
  - `id ` -id of the group.
  - `name` -name of the group.
  - `description` -description of the group.
  - `agents` - id list of agents in current group

## Update a group
### End Point
  `PUT /api/v1/account/groups/{group_id}`

### Parameters
  - `name` -name of the group.
  - `description` -description of the group.
  - `agents` - id list of agents in current group
    + `agent_id` -id of the agent
    + `email` -email of the agent
    
### Response
  - `id ` -id of the group.
  - `name` -name of the group.
  - `description` -description of the group.
  - `agents` - id list of agents in current group

## Remove a group 
### End Point
  `DELETE /api/v1/account/groups/{group_id}`

### Parameters
  No parameters.

### Response
  - `result ` -the result of operating

## Get list of permissions
### End Point
  `GET /api/v1/account/permissions`

### Parameters
  No parameters

### Response
  Permissions list, including
  - `id ` -id of the permission.
  - `module` -module of the permission belong to.
  - `name` -name of the permission.
  - `description` -the description of the permission.

## Get a single permission
### End Point
  `GET /api/v1/account/permissions/{permission_id}`

### Parameters
  No parameters

### Response
  - `id ` -id of the permission.
  - `module` -module of the permission belong to.
  - `name` -name of the permission.
  - `description` -the description of the permission.

## Create a new permission
### End Point
  `POST /api/v1/account/permissions`

### Parameters
  - `module` -module of the permission belong to.
  - `name` -name of the permission.
  - `description` -the description of the permission.

### Response
  - `id ` -id of the permission.
  - `module` -module of the permission belong to.
  - `name` -name of the permission.
  - `description` -the description of the permission.

## Update a permission
### End Point
  `PUT /api/v1/account/permissions/{permission_id}`

### Parameters
  - `module` -module of the permission belong to.
  - `name` -name of the permission.
  - `description` -the description of the permission.

### Response
  - `id ` -id of the permission.
  - `module` -module of the permission belong to.
  - `name` -name of the permission.
  - `description` -the description of the permission.

## Remove a permission 
### End Point
  `DELETE /api/v1/account/permissions/{permission_id}`

### Parameters
  No parameters.

### Response
  - `result ` -the result of operating

## Get list of a agent's permissions
### End Point
  `GET /api/v1/account/agents/{agent_id}/permissions`

### Parameters
  No parameters

### Response
  Permissions list, including
  - `agent_id` -id of the agent.
  - `permission_id ` -id of the permission.
  - `module` -module of the permission belong to.

## Create a new permission for a agent
### End Point
  `POST /api/v1/account/agents/{agent_id/}/permissions`

### Parameters
  - `permission_id ` -id of the permission.
  - `module` -module of the permission belong to.

### Response
  - `agent_id` -id of the agent.
  - `permission_id ` -id of the permission.
  - `module` -module of the permission belong to.

## Remove a permission for a agent
### End Point
  `DELETE /api/v1/account/agents/{agent_id}/permissions/{permission_id}`

### Parameters
  No parameters.

### Response
  - `result ` -the result of operating

## Get list of a group's permissions
### End Point
  `GET /api/v1/account/groups/{group_id}/permissions`

### Parameters
  No parameters

### Response
  Permissions list, including
  - `group_id` -id of the group.
  - `permission_id ` -id of the permission.
  - `module` -module of the permission belong to.

## Create a new permission for a group
### End Point
  `POST /api/v1/account/groups/{groups_id/}/permissions`

### Parameters
  - `permission_id ` -id of the permission.
  - `module` -module of the permission belong to.

### Response
  - `group_id` -id of the group.
  - `permission_id ` -id of the permission.
  - `module` -module of the permission belong to.

## Remove a permission for a group
### End Point
  `DELETE /api/v1/account/groups/{groups_id}/permissions/{permission_id}`

### Parameters
  No parameters.

### Response
  - `result ` -the result of operating

## Get ip range list of ip restrictions
### End Point
  `Get /api/v1/account/ipRestrictions/ipRanges`

### Parameters
  No parameters

### Response
  ip range list, including
  - `id` -id of ip range.
  - `ipFrom` -ip which ip range start from.
  - `ipTo` - ip which ip range end to.

## Update a ip range of ip restrictions 
### End Point
  `POST /api/v1/account/ipRestrictions/ipRanges/{rang_id}`

### Parameters
  - `ipFrom` -ip which ip range start from.
  - `ipTo` - ip which ip range end to.

### Response
  - `id` -id of ip range.
  - `ipFrom` -ip which ip range start from.
  - `ipTo` - ip which ip range end to.

## Remove a ip range of ip restrictions
### End Point
  `DELETE /api/v1/account/ipRestrictions/ipRanges/{rang_id}`

### Parameters
  No parameters.

### Response
  - `result ` -the result of operating

## Get configuration of ip restrictions 
### End Point
  `Get /api/v1/account/ipRestrictions/config`

### Parameters
  No parameters.

### Response
  - `id` -id of the config.
  - `siteId` -id of the site.
  - `isEnable` -whether IP Restrictions is enable or not.
  - `isEnableForMobile` -whether IP Restrictions is enable or not for mobile access.

## Update configuration of ip restrictions 
### End Point
  `PUT /api/v1/account/ipRestrictions/config`

### Parameters
optional:  
  - `isEnable` -whether IP Restrictions is enable or not.
  - `isEnableForMobile` -whether IP Restrictions is enable or not for mobile access.

### Response
  - `id` -id of the config.
  - `siteId` -id of the site.
  - `isEnable` -whether IP Restrictions is enable or not.
  - `isEnableForMobile` -whether IP Restrictions is enable or not for mobile access.

  You need `View Audit Log` permission to view audit logs.
  + `Get /api/v1/account/auditLogs` -
  + 

## Get audit Logs list 
### End Point
  `Get /api/v1/account/auditLogs`

### Parameters
  - `dateFrom` - the date from which agent do the action.
  - `dateTo` - the date end which agent do the action.
  optional：
  - `product` - the product which the action belongs to, including `liveChat`、`userContact` and `account`.
  - `type` - the type of the action.
  - `agentId` - id of the agent who do the action.
  - `keywords` - the key words of inquiring the action

### Response
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

## Get a single audit log 
### End Point
  `Get /api/v1/account/auditLogs/{log_id}`

### Parameters
  No parameters.

### Response
  - `id` -id of the config.
  - `actionTime` -the time of the action.
  - `agentName` - the agent which do the action.
  - `application` - the module which the action belongs to.
  - `actionType` - the type of the action.
  - `actionSummary` - the summary of the action.
