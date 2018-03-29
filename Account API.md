# General

## Account API
  You need `Manage Agent & Agent Groups` permission to manage agent、group and permission.
  - `Site` -Site Manage
    + `GET /api/v1/account/sites/{site_id}/profile` -Get profile of a single site
    + `PUT /api/v1/account/sites/{site_id}/profile` -[Update profile of a site](#update-profile-of-a-site)
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

### Example
Sample request:

  `curl -u tester@comm100.com:ef43f9362aac4f60ad428cb4d072f2c8 -X GET \`   
  `"https://hosted.comm100.com/api/v1/account/sites/1000124/profile"`

Sample Response:
```javascript
  { 
    "id":"1000124",
    "name":"comm100"
    "firstName":"comm100",
    "lastName":"test",
    "company":"comm100",
    "website":"www.comm100.com", 
    "phoneNumber":"09714073257",
    "mobilePhone":"1-909-6185426",
    "title":"test",
    "faxNumber":"09714073257",
    "mailAddress":"15009 NE Airport Way Ste 100",
    "city":"Portland", 
    "stateOrProvince":"Oregon",
    "postalOrZipCode":"97230-8309",
    "country":"Unite States",
    "companySize":"1-20",
    "timeZone":"GMT-07:00",
    "datetimeFormat":"yyyy-MM-dd HH:mm:ss",
  }	       
```

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

### Example
Sample request:

  `curl –u allon@comm100.com:ef43f9362aac4f60ad428cb4d072f2c8 -X PUT -d title=testTitle&lastName=kim \`   
  `"https://hosted.comm100.com/api/v1/account/sites/1000124/profile"`

Sample Response:
```javascript
  { 
    "id":"1000124",
    "name":"comm100"
    "firstName":"comm100",
    "lastName":"kim",
    "company":"comm100",
    "website":"www.comm100.com", 
    "phoneNumber":"09714073257",
    "mobilePhone":"1-909-6185426",
    "title":"testTitle",
    "faxNumber":"09714073257",
    "mailAddress":"15009 NE Airport Way Ste 100",
    "city":"Portland", 
    "stateOrProvince":"Oregon",
    "postalOrZipCode":"97230-8309",
    "country":"Unite States",
    "companySize":"1-20",
    "timeZone":"GMT-07:00",
    "datetimeFormat":"yyyy-MM-dd HH:mm:ss",
  }	          
```

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

### Example
Sample request:

  `curl -u tester@comm100.com:ef43f9362aac4f60ad428cb4d072f2c8 -X GET \`   
  `"https://hosted.comm100.com/api/v1/account/agents"`

Sample response:
```javascript
 [ 
    {
        "api_key":"ef43f9362aac4f60ad428cb4d072f2c8", 
        "departments":[
            1,
            2
        ],
        "email":"allon@comm100.com",
        "id" : 1,
        "max_chats_count":5,
        "name":"allon",
        "ongoing_chats":2,
        "status":0
    },
    {
        "api_key":"5ce7c8010251448f91b7eedc7931c1e9", 
        "departments":[
            2,
            3
        ],
        "email":"roy@comm100.com",
        "id":2, 
        "max_chats_count":5,
        "name":"roy",
        "ongoing_chats":0,
        "status":1
    },
    ...
]
```

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

### Example
Sample request:

  `curl -u tester@comm100.com:ef43f9362aac4f60ad428cb4d072f2c8 -X GET \`   
  `"https://hosted.comm100.com/api/v1/account/agents/allon@comm100.com"`

Sample Response:
```javascript
  { 
    "api_key":"ef43f9362aac4f60ad428cb4d072f2c8",
    "departments":[ 
        1,
        2
    ], 
    "description":"live chat support"
    "display_name":"allon",
    "email":"allon@comm100.com",
    "first_name":"allon",
    "id":1, 
    "is_active":"ture",
    "is_admin":"true",
    "last_name":"lu",
    "max_chats_count":5,
    "name":"allon",
    "ongoing_chats":0, 
    "phone":"1-877-305-0464",
    "status":0,
    "title":"support",
  }	       
```

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

### Example
Sample request:

  `curl –u allon@comm100.com:ef43f9362aac4f60ad428cb4d072f2c8 -X POST -d \`
  `display_name=Kelly_Comm100&first_name=Kelly&last_name=Blair&email=kelly@comm100.com&password=Comm100&departments=1,2&max_chats_count=5 \`   
  `"https://hosted.comm100.com/api/v1/account/agents"`

Sample Response:
```javascript
{ 
    "api_key":"20d35dc30a204892b7d78d1acdf1298e",
    "departments":[ 
        1,
        2
    ], 
    "description":""
    "display_name":"Kelly_Comm100",
    "email":"kelly@comm100.com",
    "first_name":"Kelly",
    "id":11, 
    "is_active":"ture",
    "is_admin":"false",
    "last_name":"Blair",
    "max_chats_count":5,
    "name":"allon",
    "ongoing_chats":0, 
    "phone":"1-877-305-0464",
    "status":2,
    "title":"",
}	     
```

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

### Example
Sample request:

  `curl –u allon@comm100.com:ef43f9362aac4f60ad428cb4d072f2c8 -X PUT -d display_name=Allon_Comm100&max_chats_count=3&title=sales&status=1 \`   
  `"https://hosted.comm100.com/api/v1/account/agents/allon@comm100.com"`

Sample Response:
```javascript
{ 
    "api_key":"cc51a93c13e84ecfba9a9620450ce778",
    "departments":[
        1,
        2
    ], 
    "description":"live chat support"
    "display_name":"Allon_Comm100",
    "email":"allon@comm100.com",
    "first_name":"allon",
    "id":1, 
    "is_active":"ture",
    "is_admin":"true",
    "last_name":"lu",
    "max_chats_count":3,
    "name":"allon",
    "ongoing_chats":0, 
    "phone":"1-877-305-0464",
    "status":1,
    "title":"sales",
}	     
```

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

### Example
Sample request:

  `curl –u allon@comm100.com:ef43f9362aac4f60ad428cb4d072f2c8 -X PUT \`   
  `"https://hosted.comm100.com/api/v1/account/agents/allon@comm100.com/reset_api_key"`

Sample Response:
```javascript
{ 
    "api_key":"cc51a93c13e84ecfba9a9620450ce778",
    "departments":[
        1,
        2
    ], 
    "description":"live chat support"
    "display_name":"allon",
    "email":"allon@comm100.com",
    "first_name":"allon",
    "id":1, 
    "is_active":"ture",
    "is_admin":"true",
    "last_name":"lu",
    "max_chats_count":5,
    "name":"allon",
    "ongoing_chats":0, 
    "phone":"1-877-305-0464",
    "status":0,
    "title":"support",
}	 
```

## Remove an agent 
### End Point
  `DELETE /api/v1/account/agents/{agent_email}`

### Parameters
  No parameters.

### Response
  - `result ` -the result of operating

### Example
Sample request:

  `curl –u allon@comm100.com:ef43f9362aac4f60ad428cb4d072f2c8 -X DELETE \`   
  `"https://hosted.comm100.com/api/v1/account/agents/roy@comm100.com"`

Sample Response:
```javascript
{
    "result":"Operator 'roy@comm100.com' has been removed."
}
```

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

### Example
Sample request:

  `curl -u tester@comm100.com:ef43f9362aac4f60ad428cb4d072f2c8 -X GET \`   
  `"https://hosted.comm100.com/api/v1/account/groups"`

Sample response:
```javascript
 [ 
    {
        "id":"123", 
        "name":"Group A",
        "description" : "this is first group!"
    },
    {
        "id":"235", 
        "name":"Group B",
        "description" : "this is second group!"
    },
    ...
]
```
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

### Example
Sample request:

  `curl -u tester@comm100.com:ef43f9362aac4f60ad428cb4d072f2c8 -X GET \`   
  `"https://hosted.comm100.com/api/v1/account/groups/123"`

Sample Response:
```javascript
  {
    "id":"123", 
    "name":"Group A",
    "description" : "this is first group!",
    "agents":[{
        "agent_id":1234,
        "email":"allon@comm100.com"
    },{
        "agent_id":5678,
        "email":"kim@comm100.com"
    }]
   }      
```
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

### Example
Sample request:

  `curl –u allon@comm100.com:ef43f9362aac4f60ad428cb4d072f2c8 -X POST -d name=groupC&description=groupC&agents=1234,2345,5678 \`   
  `"https://hosted.comm100.com/api/v1/account/groups"`

Sample Response:
```javascript
  {
    "id":"567", 
    "name":"groupC",
    "description" : "groupC",
    "agents":[{
        "agent_id":1234,
        "email":"allon@comm100.com"
    },{
        "agent_id":2345,
        "email":"roy@comm100.com"
    },{
        "agent_id":5678,
        "email":"kim@comm100.com"
    }]
   }       
```

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

### Example
Sample request:

  `curl –u allon@comm100.com:ef43f9362aac4f60ad428cb4d072f2c8 -X PUT -d name=groupC&description=groupC&agents=123,234,456,789 \`   
  `"https://hosted.comm100.com/api/v1/account/groups/567"`

Sample Response:
```javascript
  {
    "id":"5678", 
    "name":"groupC",
    "description" : "groupC",
    "agents":[ {
        "agent_id":123,
        "email":"allon@comm100.com"
    },{
        "agent_id":234,
        "email":"roy@comm100.com"
    },{
        "agent_id":456,
        "email":"joe@comm100.com"
    },{
        "agent_id":789,
        "email":"kim@comm100.com"
    }]
   }         
```

## Remove a group 
### End Point
  `DELETE /api/v1/account/groups/{group_id}`

### Parameters
  No parameters.

### Response
  - `result ` -the result of operating

### Example
Sample request:

  `curl –u allon@comm100.com:ef43f9362aac4f60ad428cb4d072f2c8 -X DELETE \`   
  `"https://hosted.comm100.com/api/v1/account/groups/123"`

Sample Response:
```javascript
{
    "result":"Group '123' has been removed."
}
```

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

### Example
Sample request:

  `curl -u tester@comm100.com:ef43f9362aac4f60ad428cb4d072f2c8 -X GET \`   
  `"https://hosted.comm100.com/api/v1/account/permissions"`

Sample response:
```javascript
 [ 
    {
        "id":"123", 
        "module":"Live Chat",
        "name":"Accept chats",
        "description" : "Accept my department's chat requests;Accept chat requests which do not belong to any departments"
    },
    {
        "id":"234", 
        "module":"User & Contact",
        "name":"View Users",
        "description" : "View user list and user details"
    },
    ...
]
```
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

### Example
Sample request:

  `curl -u tester@comm100.com:ef43f9362aac4f60ad428cb4d072f2c8 -X GET \`   
  `"https://hosted.comm100.com/api/v1/account/permissions/123"`

Sample Response:
```javascript
  {
    "id":"123", 
    "module":"Live Chat",
    "name":"Accept chats",
    "description" : "Accept my department's chat requests;Accept chat requests which do not belong to any departments"
  }     
```

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

### Example
Sample request:

  `curl –u allon@comm100.com:ef43f9362aac4f60ad428cb4d072f2c8 -X POST -d module=Account&name=Manage%20Site%20Profile&description=View%20Site%20Profile \`   
  `"https://hosted.comm100.com/api/v1/account/permissions"`

Sample Response:
```javascript
  {
    "id":"159", 
    "module":"Account",
    "name":"Manage Site Profile",
    "description" : "View Site Profile"
  }    
```

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

### Example
Sample request:

  `curl –u allon@comm100.com:ef43f9362aac4f60ad428cb4d072f2c8 -X PUT -d module=Account&name=Manage%20Site%20Profile&description=View/edit%20Site%20Profile \`
  `"https://hosted.comm100.com/api/v1/account/groups/157"`

Sample Response:
```javascript
  {
    "id":"159", 
    "module":"Account",
    "name":"Manage Site Profile",
    "description" : "View/edit Site Profile"
  }        
```

## Remove a permission 
### End Point
  `DELETE /api/v1/account/permissions/{permission_id}`

### Parameters
  No parameters.

### Response
  - `result ` -the result of operating

### Example
Sample request:

  `curl –u allon@comm100.com:ef43f9362aac4f60ad428cb4d072f2c8 -X DELETE \`   
  `"https://hosted.comm100.com/api/v1/account/permissions/159"`

Sample Response:
```javascript
{
    "result":"Permission '159' has been removed."
}
```

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

### Example
Sample request:

  `curl -u tester@comm100.com:ef43f9362aac4f60ad428cb4d072f2c8 -X GET \`   
  `"https://hosted.comm100.com/api/v1/account/agents/123/permissions"`

Sample response:
```javascript
 [ 
    {
        "agent_id":"123",
        "permission_id":"1234", 
        "module":"Live Chat"
    },
    {
        "agent_id":"123",
        "permission_id":"2356", 
        "module":"Live Chat"
    },
    ...
]
```

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

### Example
Sample request:

  `curl –u allon@comm100.com:ef43f9362aac4f60ad428cb4d072f2c8 -X POST -d module=Account&permission_id=5689 \`   
  `"https://hosted.comm100.com/api/v1/account/agents/123/permissions"`

Sample Response:
```javascript
  {
    "agent_id":"123",
    "permission_id":"5689", 
    "module":"Account"
  }    
```

## Remove a permission for a agent
### End Point
  `DELETE /api/v1/account/agents/{agent_id}/permissions/{permission_id}`

### Parameters
  No parameters.

### Response
  - `result ` -the result of operating

### Example
Sample request:

  `curl –u allon@comm100.com:ef43f9362aac4f60ad428cb4d072f2c8 -X DELETE \`   
  `"https://hosted.comm100.com/api/v1/account/agents/123/permissions/159"`

Sample Response:
```javascript
{
    "result":"Permission '159' of agent '123' has been removed."
}
```


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

### Example
Sample request:

  `curl -u tester@comm100.com:ef43f9362aac4f60ad428cb4d072f2c8 -X GET \`   
  `"https://hosted.comm100.com/api/v1/account/group/123/permissions"`

Sample response:
```javascript
 [ 
    {
        "group_id":"123",
        "permission_id":"1234", 
        "module":"Live Chat"
    },
    {
        "group_id":"123",
        "permission_id":"2356", 
        "module":"Live Chat"
    },
    ...
]
```

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

### Example
Sample request:

  `curl –u allon@comm100.com:ef43f9362aac4f60ad428cb4d072f2c8 -X POST -d module=Account&permission_id=5689 \`   
  `"https://hosted.comm100.com/api/v1/account/groups/123/permissions"`

Sample Response:
```javascript
  {
    "group_id":"123",
    "permission_id":"5689", 
    "module":"Account"
  }    
```

## Remove a permission for a group
### End Point
  `DELETE /api/v1/account/groups/{groups_id}/permissions/{permission_id}`

### Parameters
  No parameters.

### Response
  - `result ` -the result of operating

### Example
Sample request:

  `curl –u allon@comm100.com:ef43f9362aac4f60ad428cb4d072f2c8 -X DELETE \`   
  `"https://hosted.comm100.com/api/v1/account/groups/123/permissions/159"`

Sample Response:
```javascript
{
    "result":"Permission '159' of group '123' has been removed."
}
```