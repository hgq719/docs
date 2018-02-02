# Manifest Reference

## Manifest.json文件示例
```json
{
  "name": "Comm100Bot", //App的名字
  "author": {
    "name": "Comm100", //开发者的名字
    "email": "developer@comm100.com",  //开发者的邮箱
    "url": "https://www.comm100.com/bot" //开发者的主页地址或App的主页地址
  },
  "private": false,  //该APP是否是私有APP的标志
  "version": "1.0",  //App版本
  "frameworkVersion": "1.0",  //Comm100API框架版本
  "signedUrls": "false",    //指定是否所有页面都需要添加JWT，让开发者通过JWT来校验location中配置的页面接收的请求是否来自Comm100 
  "location": {            //App的安装位置
    "controlPanel_topBar": "/assets/cp_topBar.html",
    "agentConsole_chatSideBar": "/assets/ac_chatSideBar.html"
  },
  "settings":{            //App配置页面
    "url": "assets/settings.html"
  },
  "visitor": {           //访客端需要引入的对象
    "customCSS": [       //访客端引入的css
      "/assets/visitor_custom_css.css"
    ],
    "customJS": [        //访客端引入的js
      "/assets/visitor_custom_js.js"
    ]
  },
  "webhook":[{                          //Webhook配置
    "name": "app.installed",            //webhook名称 
    "url": "******/logicalProcess"      //webhook请求地址
  }],
  "objects":[{                          //需要引入到Comm100的外部对象
    "name": "Bot",                      //外部对象的名字
    "property":[{                       //外部对象的属性
      "name": "BotId",                  //字段名字
      "type": "string"                  //字段类型
    },{
      "name": "BotName",
      "type": "string"
    }]
  }],
  "bot": {
    "endpoint": {
      "list": {     //机器人列表Endpoint配置
        "method": "POST",
        "url": "https://api.chatbot.com/comm100/{siteId}/bots", // {siteId}为宏, Comm100在处理这个地址时会替换掉这个参数
        "headers": {
          "Authorization": "Bearer {app.metadata.token}", // {app.metadata.token} 为后台安装这个app时设置的元数据, 
          "x-api-version": "v2",
        }
      },
      "message": {   //机器人回答问题Endpoint配置
        "method": "POST", //必须为post
        "url": "https://api.chatbot.com/comm100/{siteId}/bots/{botId}/message", // {botId}为宏参，表示使用的bot Id, 用户可以选择设置或者不设置, body中的内容也会有botId的属性
        "headers": {
          "Authorization": "Bearer {app.metadata.token}", // {app.metadata.token} 为后台安装这个app时设置的元数据, 
          "x-api-version": "v2",
        }
      }
    }
  }
}
```
## Manifest Properties
  - [name](#name)
  - [author](#author)
  - [private](#private)
  - [version](#version)
  - [frameworkVersion](#frameworkversion)
  - [signedUrls](#signedurls)
  - [location](#location)
  - [settings](#settings)
  - [visitor](#visitor)
  - [webhook](#webhook)
  - [objects](#objects)
  - [bot](#bot)

## Name
  指定App的名字，在Manifest中定义的App出现的位置也会以这个名字命名，如应用程序管理、产品菜单、tab标题等位置。必须指定。

## author 
  指定App开发者的信息，为一个包含`name`、`email`、`url`属性的json对象。必须指定。
   - `name` 指定当前App的开发者的名字。
   - `email` 指定当前App的开发者的邮箱。
   - `url` 指定当前App的开发者的主页地址或App的主页地址。


   ```json
   "author": {
      "name": "Comm100",                    
      "email": "developer@comm100.com",     
      "url": "https://www.comm100.com/bot"  
   }
   ```

## private
  指定当前App是否是私有的，默认值为`true`。私有的App只能被App开发者安装和使用，需要提交到Marketplace的App该属性必须设置为`false`。

   ```json
   "private": false             //指定当前App是否是私有的，默认值为true
   ```

## version
  指定当前App的版本。该版本信息出现在Marketplace的App详细信息中。

   ```json
   "version": "1.0"              //指定App的版本
   ```

## frameworkVersion
  指定当前App开发过程中使用Comm100的框架版本。必须指定。

   ```json
   "frameworkVersion": "1.0"    //指定当前App开发过程中使用Comm100的框架版本     
   ```

## signedUrls
  指定页面是否需要添加JSON Web Token(JWT)，让开发者通过JWT来校验打开location中配置的页面的请求是否来自Comm100。默认值为`false`。当前属性只适用于远程托管的页面，不适用于由Comm100托管的页面。   
  开发者可以通过`signedUrls`属性来设置是否对所有App中所有页面启用JWT。

  ```json
  "signedUrls": false 
  ```

  开发者还可以通过给`location`中特定位置添加`signed`属性来设置是否对当前位置的App页面启用JWT。

   ```json
   "location": {
     "agentConsole_chatSideBar": {
       "signed": true,     //包含JWT
       "url": "https：//*****/index.html"    //非Comm100托管，开发者远程托管页面
     }
   }
   ```

## location
  指定当前App安装以后App出现在Comm100的产品界面中的位置。必须指定。目前Comm100的`Livechat`产品开放的界面位置如下：  

  - [controlPanel_topBar](#control-panel-topbar) 
  - [controlPanel_background](#control-panel-background)
  - [agentConsole_topBar](#agent-console-topbar)
  - [agentConsole_navigationBar](#agent-console-navigations)
  - [agentConsole_chatSideBar](#agent-console-chatsidebar)
  - [agentConsole_background](#agent-console-background)  


  每个位置可指定下面的属性。
  + `autoHide` 指定当前App在系统启动后是否默认隐藏。默认值为`false`。
  + `autoLoad` 指定当前App在系统启动以后是否自动加载。默认值为`false`。
  + `url` 指定当前位置下的iframe中显示的页面地址，该地址可以是开发者远程托管的绝对页面地址，也可以是由Comm100托管的相对路径地址。必须指定。
  + `signed` 当前位置下的iframe为远程托管(非Comm100托管)页面时，开发者可通过指定该属性是否在Comm100当前页面中的请求包含一个JSON Web Token(JWT)，开发者可以用来验证该请求是否来自Comm100合法请求。默认值为`false`。  

   ```json
   "location": {
     "agentConsole_chatSideBar": {
       "autoHide": false,  //自动隐藏
       "autoLoad": false,  //自动加载
       "signed": true,     //包含JWT
       "url": "https：//*****/index.html"    //非Comm100托管，开发者远程托管页面
     }
   }
   ```
   
   也可以只指定位置的url，其他都为默认值。如：

   ```json
   "location": {
     "agentconsole_chatSidebar": "/assets/index.html"
   }
   ```

   可以指定多个位置

   ```json
   "location": {
     "agentConsole_topBar": "/assets/ac_topBar.html",
     "agentConsole_background": "/assets/inital.html",
     "controlPanel_topBar": "/assets/cp_topBar.html"       //指定产品级菜单
   }
   ```

### Control Panel TopBar
  指定将App安装在Control Panel的右上方产品级菜单区域。安装此App以后，在Control Panel的右上方会多一个名字为`App Name`的产品级菜单，点击菜单，默认在菜单的下方弹出一块区域，该区域的显示内容为配置的`url`的内容。

  ```json
  "location": {
    "controlPanel_topBar": "/assets/index.html"
  }
  ```

### Control Panel Background 
  指定App在Control Panel中以后台形式(不显示UI)启动的页面。安装此App以后，默认在Control Panel启动后自动加载`background`中配置的页面内容，但该页面不显示。

  ```json
  "location": {
    "controlPanel_background": "/assets/controlPanel_initial.html"
  }
  ```

### Agent Console TopBar
  指定将App安装在Agent Console的头部全局菜单区域。安装此App以后，在Agent Console的头部全局菜单区域中的最后一个位置会添加一个App的菜单，点击该菜单，默认弹出一个窗口，窗口的内容为该处配置的页面内容。

  ```json
  "location": {
    "agentConsole_topBar": "/assets/topBar.html"
  }
  ```

#### Events
  在Control Panel的TopBar中，app可使用的下面的事件：
  - [pane.activated](#topbar-pane-activated)
  - [pane.deactivated](#topbar-pane-deactivated)

##### TopBar pane.activated
  可通过下面的API来设置在pane激活的时候需要做的事情。

  ```javascript
    Comm100AgentConsoleAPI.on("topBar.pane.activated", function(){
      //handler code
    }
  ```

##### TopBar pane.deactivated
  可通过下面的API来设置在pane取消激活的时候需要做的事情。

  ```javascript
    Comm100AgentConsoleAPI.on("topBar.pane.deactivated", function(){
      //handler code
    }
  ```

#### Objects
  - [PopupOver](#popupover-object)

##### PopupOver Object
  - Properties
    + `popupOver.size`-弹出区域的大小
      * `width`-弹出区域的宽度
      * `height`-弹出区域的高度
    + `popupOver.visible`-弹出窗口的显示状态: show/hide/toggle 默认show

  - Actions
    + `set` -设置popupOver的属性，如：


  ```javascript
    Comm100AgentConsoleAPI.set("topBar.popupOver.size",{
      width:  300,
      height: 200
    });   //设置popupover区域大小

    Comm100AgentConsoleAPI.set("topBar.popupOver.visible","show"); //设置popupover区域的可见性
  ```

### Agent Console NavigationBar
  指定将App安装在Agent Console的左侧列表菜单区域。安装此App以后，默认在Agent Console的左侧列表菜单中的最后一个位置添加一个App菜单，点击该菜单，右侧内容区域展示的内容为该处配置的页面内容。

  ```json
  "location": {
    "agentConsole_navigationBar": "/assets/navigationBar.html"
  }
  ```

### Agent Console ChatSideBar
  指定将App安装在Agent Console的聊天窗口的右侧区域。安装此App以后，在Agent Console的聊天窗口的右侧区域的最后一个位置添加一个Tab菜单，点击该菜单，下方的内容区域展示的内容为该处配置的页面内容。

  ```json
  "location": {
    "agentConsole_chatSideBar": "/assets/chatSideBar.html"
  }
  ```
 
### Agent Console Background
  指定App在Agent Console中以后台形式(不显示UI)启动的页面。安装此App以后，默认在Agent Console启动后自动加载`background`中配置的页面内容，但该页面不显示。

  ```json
  "location": {
    "agentConsole_background": "/assets/agentConsole_initial.html"
  }
  ```

## settings
  指定当前App安装以后的配置页面。安装App以后，Control Panel的应用管理中会增加一个当前App的对应菜单，点击按钮菜单上的配置按钮，会在应用配置tab中加载`settings`中配置的`url`页面。
   - `url` - 指定App的配置页面的地址。

  ```json
  "settings":{            //App配置页面
    "url": "assets/settings.html"
  }
  ```

## visitor
  指定需要在访客端需要引入的对象，包括自定义CSS和JavaScript。安装App以后, 前端在加载完系统的访客端对象的时候会加载该区域设置的自定义对象。
   - `customCSS` - 指定当前App在访客端需要引用的自定义CSS。
   - `customJS` - 指定当前App在访客端需要引用的自定义JavaScript。  


   ```json
   "visitor": {
     "customCSS": [        //自定义css
       "/assets/visitor_custom_css.css"
     ],
     "customJS": [         //自定义js    
       "/assets/visitor_custom_js.js"
     ]
   }
   ```

## webhook
  指定在Comm100的特定webhook中的请求地址。安装App以后, Comm100会在Manifest文件的`webhook`属性中配置的`name`的Webhook的位置请求`url`的地址。
   - `name` - 指定Webhook的名称，详情可参考[Webhook API](https://github.com/hgq719/docs/blob/master/WebhookApi.md)。
   - `url` - 指定当前的webhook中需要请求的地址。  


   ```json
   "webhook": [{
     "name": "app.installed",        //Comm100定义的webhook名字
     "url": "****/logicalProcess"    //配置webhook中的请求地址
   }]
   ```

## objects
  指定将外部对象引入到Comm100中，通过配置外部对象属性与Comm100对象属性的映射关系来实现系统之间的数据流转。安装App以后，可以通过Comm100的API来设置和获取外部对象。
  - `name` - 指定需要引入的外部对象的对象名
  - `property` - 指定当前引入的外部对象的属性
  - `fieldName` - 指定外部对象的字段名称
  - `fieldType` - 指定外部对象的数据类型,类型包括:`int/float/string/date`


  ```json
  "objects":[{
      "name": "Bot",    //外部对象名字
      "property":[{            //外部对象属性数组
        "fieldName": "BotId",    //字段名
        "fileType": "string"     //字段类型
      },{
        "fieldName": "BotName",
        "fileType": "string"
      }]
    }]
  ```

## bot
  指定需要将自己的Bot系统接入Comm100产品需要进行的配置，安装该Bot App以后，可配置使用当前Bot参与聊天。
  - `endpoint` 指定接入Bot需要配置的Endpoint节点。
  - `list` 指定接入Bot时获取Bot列表的接口信息，具体方式参考[Bot List](https://github.com/hgq719/docs/blob/master/open-platform-chat-bot.md#bot-list)
  - `message` 指定接入Bot时，Bot回答问题的接口信息,具体方式参考[Bot Message](https://github.com/hgq719/docs/blob/master/open-platform-chat-bot.md#bot-engine-handle-visitor-message)
  - `method` 指定接入Bot时对应接口的请求方式：`POST/GET` ,目前Bot的两个接口全部为`POST`
  - `url` 指定接入Bot时调用的Bot的接口地址
  - `headers` 指定接入Bot调用Bot的接口的头部信息,Manifest中可用宏定义参考[Micro Define](https://github.com/hgq719/docs/blob/master/open-platform-chat-bot.md#micro-define)


   ```json
   "bot": {
     "endpoint": {
       "list": {     //机器人列表Endpoint配置
         "method": "POST",
         "url": "https://api.chatbot.com/comm100/{siteId}/bots", // {siteId}为宏, Comm100在处理这个地址时会替换掉这个参数
         "headers": {
           "Authorization": "Bearer {app.metadata.token}", // {app.metadata.token} 为后台安装这个app时设置的元数据, 
           "x-api-version": "v2",
         }
       },
       "message": {   //机器人列表回答问题Endpoint配置
         "method": "POST", //必须为post
         "url": "https://api.chatbot.com/comm100/{siteId}/bots/{botId}/message", // {botId}为宏参，表示使用的bot Id, 用户可以选择设置或者不设置, body中的内容也会有botId的属性
         "headers": {
           "Authorization": "Bearer {app.metadata.token}", // {app.metadata.token} 为后台安装这个app时设置的元数据, 
           "x-api-version": "v2",
         }
       }
     }
   }
   ```

