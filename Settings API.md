# General

## Canned Messages
  You need `Manage Pulbic Canned Messages` permission to manage canned message.
  + `GET /api/v1/livechat/cannedMessages` -get list of canned Message
  + `GET /api/v1/livechat/cannedMessages/{id}`  -get a single canned Message
  + `POST /api/v1/livechat/cannedMessages` -create a new canned Message
  + `PUT /api/v1/livechat/cannedMessages/{id}`  -update a canned Message
  + `DELETE /api/v1/livechat/cannedMessages/{id}`  -remove a canned Message
  + `GET /api/v1/livechat/cannedMessageCategories` -get list of canned Messages Categories
  + `GET /api/v1/livechat/cannedMessageCategories/{id}`  -get a single canned Messages Category
  + `POST /api/v1/livechat/cannedMessageCategories` -create a new canned Messages Category
  + `PUT /api/v1/livechat/cannedMessageCategories/{id}`  -update a canned Messages Category
  + `DELETE /api/v1/livechat/cannedMessageCategories/{id}`  -remove a canned Messages Category

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

## Departments
  You need `Manage Settings` permission to manage department.
  + `GET /api/v1/livechat/departments` -get list of departments
  + `GET /api/v1/livechat/departments/{id}`  -get a single department
  + `POST /api/v1/livechat/departments` -create a new department
  + `PUT /api/v1/livechat/departments/{id}`  -update a department
  + `DELETE /api/v1/livechat/departments/{id}`  -remove a department

### Get list of departemtns 
#### End Point 
  `GET /api/v1/livechat/departments`

#### Parameters
  No parameters

#### Response
  departemtns list, including
  - `id ` -id of the department.
  - `name` -name of the department.
  - `description` -description of the department.
  - `members` - the string of the members list in the department.

### Get a single departments 
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

### Create a new departments 
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

### Update a departments 
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

### Remove a departments 
#### End Point 
  `DELETE /api/v1/livechat/departments/{id}`

#### Parameters
  No parameters

#### Response
  - `result ` -the result of operating