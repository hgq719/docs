# General
1. [Canned Messages](#canned-messages)
2. [Departments](#departments)
3. [Custom Away Status](#custom-away-status)
4. [Ban List](#ban-list)
5. [Visitor Segmentation](#visitor-segmentation)

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

### Remove a department
#### End Point 
  `DELETE /api/v1/livechat/departments/{id}`

#### Parameters
  No parameters

#### Response
  - `result ` -the result of operating

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

## Ban List
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
  ban list, including
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