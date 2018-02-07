# Introduction
  Comm100AgentConsoleAPI Client可以让开发者的App与Comm100的产品进行交互。开发者可以使用client来监听事件、设置/获取属性、执行特定方法。如：

  ```javascript
  var client = Comm100AgentConsoleAPI.init();
  client.get("currentAgent.name").then(function(data){
      console.log(data); //{"currentAgent.name":"kim"}
  });
  ```

## Comm100AgentConsole Object
  Agent Console中调用API的对象。

  - Actions
    + init -返回一个[client](#client-object)

  ```javascript
    Comm100AgentConsoleAPI.onReady = function () {
      // when this callback is triggered,
      // all APIs are ready to use
      var client = Comm100AgentConsoleAPI.init();
    }
  ```

## Client Object
Methods
  - context
  - get
  - instance
  - do
  - on
  - off
  - set
  - trigger


### client.context()
  请求当前对象的上下文信息，包括当前实例的id、位置等信息，返回一个`promise`对象。

  ```javascript
    var client = Comm100AgentConsoleAPI.init();
    client.context().then(function(context){
        console.log(context);
        /*
            {
                "instance_id":"013B7322-6895-F01E-5EAE-F4DF50016AF5",
                "location":"agentConsole_topBar",
                .....
            }
        */
    });
  ```

### client.get(parameters)
  获取当前参数对应的值，返回一个`promise`对象。

  ```javascript
    var client = Comm100AgentConsoleAPI.init();
    client.get("currentChat.visitor").then(function(data){
        console.log(data);
        /*
            {
                "currentChat.visitor": {
                    ......
                }
            }
        */
    });
  ```

### client.instance(instanceId)
  初始化一个App的另外一个位置实例，用在实例间信息交互的时候。

  ```javascript
    var client = Comm100AgentConsoleAPI.init();
    var otherClient = Comm100AgentConsoleAPI.instance("013B7322-6895-F01E-5EAE-F4DF50016AF5");
  ```

### client.do(Name [,...args])
  调用`name`标识的操作，根据要求传递参数，返回一个`promise`对象。
  
  ```javascript
    var client = Comm100AgentConsoleAPI.init();
    client.do("preload").then(function(){
        //handler code
    });
  ```

### client.on(hame handler)
  在当前实例指定的`name`事件时，执行handler事件。

  ```javascript
  var client = Comm100AgentConsoleAPI.init();

  client.on("app.loaded",function(){
      //handler code
  });
  ```

  也可以通过`on`给当前实例添加一个`name`事件。

  ```javascript
  var client = Comm100AgentConsoleAPI.init();

  client.on("comming_call",function(){
      //handler code
  });
  ```

### client.off(hame handler)
  给当前实例移除一个`name`事件。

  ```javascript
  var client = Comm100AgentConsoleAPI.init();

  client.off("comming_call",function(){
      //handler code
  });
  ```

### client.set(key, value)
  设置当前`key`对应的属性的值为`value`，返回一个`promise`对象。

  ```javascript
  var client = Comm100AgentConsoleAPI.init();

  client.set("currentChat.email",email).then(function(){
      //handler code
  });
  ```

### client.trigger(name, [data])
  触发指定的`name`的事件，`data`为该事件的参数

  ```javascript
    var client = Comm100AgentConsoleAPI.init();

    client.on("comming_call",function(){
        //handler code
    });

    client.trigger("comming_call");
  ```

## Core Apps API
  Comm100在App开发框架中提供了下面一些核心的事件、核心和行为供开发者在开发App的时候使用。
  - [Core Events](core-events)
  - [Core Properties](core-properties)
  - [core Actions](core-actions)

### Core Events
  - [app.loaded](app-loaded)
  - [app.activated](app-activated)
  - [app.deactivated](app-deactivated)
  - [instance.created](instance-created)

#### App Loaded
  当App加载以后触发的事件。

  ```javascript
  client.on("app.loaded",function(){
      //hanler code
  });
  ```

### App Activated
  当App被激活以后触发的事件。

  ```javascript
  client.on("app.activated",function(){
      //hanler code
  });
  ```
  
### App Deactivated
  当App从激活状态变成非激活状态以后触发的事件。

  ```javascript
  client.on("app.deactivated",function(){
      //hanler code
  });
  ```

### Instance Created
  当App的实例状态创建以后触发的事件。

  ```javascript
  client.on("insance.created",function(){
      //hanler code
  });
  ```

### Core Properties
  - [instances](#instances-property)

#### Instances Property
  表示App的所有正在运行的实例，每一个iframe都是一个实例，返回一个`promise`对象。同一个App在Manifest中定义了多个位置，则这个App就存在多个App Instance。

  get
  
  ```javascript
    client.get('instances').then(function(instancesData){
        console.log(instancesData);
        /*
        {
            "instances":[{
                "instance_id":"013B7322-6895-F01E-5EAE-F4DF50016AF5",
                "location":"agentConsole_topBar",
                ....
            }]
        }
         */
    });
  ```

### Core Actions
  - [resize](#resize-action)
  - [instance.create](#instance-create-action)

#### Resize Action
  重新设置App所在的iframe的页面大小，大小规格中的`width`和`height`可以是`px`、`%`或`vw/vh`。

  ```javascript
    client.do("resize",{
        width: "300px",
        height:"200px"
    });
  ```

#### Instance Create Action
  创建一个App的实例，实例属性包含`location`和`instance_id`两个属性，其中`instance_id`属性不指定时，Comm100将自动生成一个实例id，推荐不指定该属性。

  ```javascript
    client.do("instance.create",{
        "location": "agentConsole_topBar",
        "instance_id": "013B7322-6895-F01E-5EAE-F4DF50016AF5" //建议不指定id，让系统自动生成
    });
  ```


## Agent Console Location
  Comm100在Agent Console端提供了可用的事件、对象、属性及操作，开发者可以使用这些来开发自己的App。每一个App实例都存在于Agent Console的某一个位置接口的iframe中，这些位置都定义了：
  - 所有的位置都共享了一些事件、属性及操作
  - 每个位置有自己独特的事件、属性及操作
  

  下表中列出了Agent Console端所有可用的位置：
  - [all locations](#all-locations) -所有可用位置。
  - [agentConsole topBar](#agent-console-topbar) -Agent Console的头部全局菜单区域。
  - [agentConsole chat headTag](#agent-console-chat-headtag) -Agent Console的聊天页面中的访客头部tag区域。
  - [agentConsole chat toolBar](#agent-console-chat-toolBar) -Agent Console的聊天页面中间的toolBar区域。
  - [agentConsole navigationBar](#agent-console-navigations) -Agent Console的左侧列表菜单区域。
  - [agentConsole chatSideBar](#agent-console-chatsidebar) -Agent Console的聊天窗口的右侧区域。
  - [agentConsole background](#agent-console-background) -Agent Console中以后台形式(不显示UI)启动的页面。


  开发者可以在Manifest文件中定义App的所在位置，具体参考[Setting The Location](https://github.com/hgq719/docs/blob/master/open-platform.md#setting-the-location)。  
  如果开发者指定`agentconsole_topBar`，App只展示一个图标，点击图标可以打开这个App。

## All Locations
  下面的这些对象、属性及操作在Agent Console中的所有位置都是可用的。

  Objects
  - [agent object](#agent-object)


  Additional actions
  - [notify](#notify-action)
  - [popup](#popup-action)  

### Agent Object
  `currentAgent` -当前登录的agent对象

  get
  ```javascript
  client.get("currentAgent").then(function(currentAgent){
      console.log(currentAgent);
      /*
      {
        "id": 1,    // number
        "name": '', // string
        "email": '',// string
        "status": '', // string, online/away
        "apikey": '', // string, 
        "chats": 3,   // number, ongoing chats
        "isAdmin": false, // boolean
      }
      */
  });
  ```

  Properties
  - `agent.id` -当前agent的Id
  - `agent.name` -当前agent的名称
  - `agent.email` -当前agent的邮箱
  - `agent.status` -当前agent的状态
  - `agent.apikey` -当前agent的apikey
  - `agent.chats` -当前agent正在进行的聊天
  - `agent.isAdmin` -当前agent是否是管理员


### Additional Actions  

#### Notify Action
 `notify` -发送一个通知

  Notification Properties
+ `body` -通知的消息主体内容
+ `renotify` -是否替换之前的通知
+ `sound`-通知声音
+ `location`-通知区域
  * `notificationArea` -是否显示右下角通知区域显示通知
  * `navigationBar` -是否在左侧List菜单区域显示通知
  * `topBar` -是否在右上角全局菜单区域显示通知

 ```javascript
  // body struct
  const notification =  {
    body: "there is a phone call for you!",
    icon: "***.ico",
    renotify: "true", //是否替换之前的通知
    sound: "https://***/call.mp3" ,  //来电声音
    location: {      
      notificationArea: true,    //右下角通知区域闪动，点击后激活AgentConsole
      navigationBar: true,       //左侧List菜单区域，点击后打开Manifest中配置的list页面
      topBar: true               //右上角全局菜单区域，点击后打开Manifest中配置的菜单页面
    }
  }

  client.do("notify",notification);
```

#### Popup Action
 `popup` -打开一个弹出窗口。

 PopupWindow Properties
+ `name` -弹出窗口的名称
+ `title` -弹出窗口的标题
+ `size`-弹出区域的大小
    * `width`-弹出区域的宽度
    * `height`-弹出区域的高度
+ `location`-弹出区域位置：TopRight/Center/BottomRight/绝对位置对象{left/right:10px; top/bottom:10px} ,默认值为Center，即页面中间位置
+ `ifmodal`-是否是模态窗口：true/false 默认false
+ `visible`-弹出窗口的显示状态: true/false 默认true
+ `url` -弹出窗口展示的内容地址

 ```javascript
  const popupWindow = {
      name: "myPopup",
      title: "popupTitle",
      size: {
          width:  300,
          height: 200
      },
      url: "https://****.html"
  }

  client.do("popup",popupWindow);
```

## Agent Console TopBar
  指定将App安装在Agent Console的头部全局菜单区域，呈现的方式是一个icon图标，点击该图标即可打开App。当App第一次被打开的时候，Comm100会在Dom中添加一个`Pane`容器，容器中展示的即为用户配置的地址的页面内容。

  ```json
  "location": {
    "agentConsole_topBar": "/assets/topBar.html"
  }
  ```

#### TopBar Actions
  在Control Panel的TopBar中，app可执行下面的动作：
  - [popover](#popover-action)
  - [preloadPane](#preloadpane-action)

##### Popover Action
  开发者可通过`popover`的API来显示、隐藏topBar App窗口或调整窗口的大小。

 popover Properties
+ `size`-弹出区域的大小
    * `width`-弹出区域的宽度
    * `height`-弹出区域的高度
+ `visible`-弹出窗口的显示状态: show/hide 默认show

 ```javascript
  client.do("popover",{
      width: 300,
      height: 200
  });

  client.do("popover","show");
 ```

##### PreloadPane Action
  在TopBar App还没有被打开过的情况下，`Pane`容易还没有被加载到Dom中来，开发者可通过`preloadPane`的API来预加载`Pane`。

  ```javascript
    client.do("preloadPane");
  ```

#### TopBar Events
  在Control Panel的TopBar中，app可使用的下面的事件：
  - [pane.activated](#topbar-pane-activated)
  - [pane.deactivated](#topbar-pane-deactivated)

##### TopBar pane.activated
  可通过下面的API来设置在pane激活的时候需要做的事情。

  ```javascript
    client.on("pane.activated", function(){
      //handler code
    }
  ```

##### TopBar pane.deactivated
  可通过下面的API来设置在pane取消激活的时候需要做的事情。

  ```javascript
    client.on("pane.deactivated", function(){
      //handler code
    }
  ```

## Agent Console Chat HeadTag
  指定在Agent Console的聊天窗口的访客头部Tag区域添加一个自定义`HeadTag`，此区域可通过API进行配置，不需要在Manifest中的location中配置该区域。

### HeadTag Object
  Agent Console的聊天页面头部的Tag对象。
- Properties
  + `headTag.name` -HeadTag的名称
  + `headTag.icon` -HeadTag的图标
  + `headTag.tip` -HeadTag的tips

```javascript
  const headTag = {
      name: "myHeadTag",
      icon: "https://***.ico",
      tip: "myHeadTag"
  }
```

- Actions
  + `get/set` -表示在Agent Console的聊天区域的头部，App的所有自定义HeadTag集合，返回一个`promise`对象。

  get

  ```javascript
    client.get('customHeadTags').then(function(headTags){
            //handler code
     });
  ```
  
  set

  ```javascript
    const newHeadTag = {
        name: "myHeadTag",
        icon: "https://***.ico",
        tip: "myHeadTag"
    };

    client.set('customHeadTags', headTags).then(function(){
            //handler code
     });
  ```

- Events
  + `customeHeadTag.actived` -当点击当前App的自定义headTag的时候触发

```javascript
    client.on("customeHeadTag.actived",function(headTag){
        if("myHeadTag" == headTag.name){
            //handler code
        }
    });
``` 

## Agent Console Chat ToolBar
  指定在Agent Console的聊天窗口的中间ToolBar区域添加一个自定义`ToolBarItem`，此区域可通过API进行配置，不需要在Manifest中的location中配置该区域。

### ToolBarItem Object
  Agent Console的聊天页面中聊天窗口中间的ToolBar里面的对象。
  - Properties
    + `toolBarItem.name` -toolBarItem对象的名称
    + `toolBarItem.icon` -toolBarItem对象的图标

```javascript
  const toolBarItem = {
      name: "myToolBarItem",
      icon: "https://***.ico"
  }
```

- Actions
  + `get/set` 表示在Agent Console的聊天区域的toolBar区域，App的所有自定义toolBarItem集合，返回一个`promise`对象。

  get

  ```javascript
    client.get('customToolBarItems').then(function(toolBarItem){
            //handler code
     });
  ```
  
  set

  ```javascript
    const toolBarItem = {
        name: "myToolBarItem",
        icon: "https://***.ico"
    }

    client.set('customToolBarItems', toolBarItem).then(function(){
            //handler code
     });
  ```

- Events
  + `customToolBarItem.actived` -当点击toolItem的时候触发

```javascript
    client.on("customToolBarItem.actived",function(toolBarItem){
        if("myToolBarItem" == toolBarItem.name){
            //handler code
        }
    });
``` 

## Agent Console NavigationBar
  指定将App安装在Agent Console的左侧导航区域，呈现的方式是一个`tab`，点击该tab即可打开App。
  
  ```json
  "location": {
    "agentConsole_navigationBar": "/assets/navBar.html"
  }
  ```

## Agent Console ChatSideBar
  指定将App安装在Agent Console的聊天窗口的右侧SideBar中，呈现的方式是一个`tab`,，点击该tab激活app，在tab的下方展示app的内容。

```json
  "location": {
    "agentConsole_chatSideBar": "/assets/chatSideBar.html"
  }
  ```

### ChatSideBar Objects
  在聊天区域的SideBar中，可用的对象如下：
  - [visitor](#visitor-object)
  - [chat](#chat-object)
  - [agent](#agent-object)

  ### Visitor Object
  `visitor` -当前聊天中的访客对象

  get
  ```javascript
  client.get("currentChat.visitor").then(function(visitor){
      console.log(visitor);
      /*
      {
        id: 1,    // number
        name: '', // string
        email: '',// string
        status: '', // string, waiting for chat/chatting/prechat/inviting/offline message/refused by agent/refused by visitor/chat ended/in site/out of site/transferring/system processing
        enterSiteTime: 1502934947,  // number, unix time
        referrer: '', // string, the referrer url
        landingPage: {
            title: '',  // string
            url: '',    // string
        }
        currentPage: {
            title: '',  // string
            url: '',    // string
        },
        currentPageStayTime: 20, // number, time of this visitor stay in current page, unit(second)
        numOfPages: 20, // number, the number of this visitor view pages
        location: {
            ip: '',   // string, ip address in dotted form
            city: '', // string
            state: '',// string
            country: '',  // string
        },
        device: {
            os: '', // string
            browser: '',  // string
            screenResolution: '', //string
            language: '', // string
            timezone: '', // string
        },
        history: {
            firstVisitorTime: 1502934947, // number, unix time
            visitTimes: 0,  // number, visit times of this visitor
            chatTimes: 0,   // number, chat times of this visitor
        }
        visitorSegmentations: [], // array<string>, names of segmentation
        customVariables: [
            {
            name: '', // string
            value: '',// string
            },
        ]
      }
      */
  });

  client.get("currentChat.visitor.email").then(function(email){
      console.log(email);
  ```

  set
  ```javascript
    client.set("currentChat.visitor.email","kim@comm100.com").then(function(){
        //handler code
    });
  ```

  Properties
  - `visitor.id` -当前聊天的visitor的Id
  - `visitor.name` -当前聊天的visitor的名称
  - `visitor.email` -当前聊天的visitor的邮箱
  - `visitor.status` -当前聊天的visitor的状态
  - `visitor.enterSiteTime` -当前聊天的visitor进入站点的事件
  - `visitor.referrer` -当前聊天的visitor的来源站点
  - `visitor.landingPage` -当前聊天的visitor访问当前站点的着陆页面对象
    + `title` -页面标题
    + `url` -页面地址
  - `visitor.currentPage` -当前聊天的visitor正在访问的页面对象
    + `title` -页面标题
    + `url` -页面地址
  - `visitor.currentPageStayTime` -当前聊天的visitor在当前页面的停留时间
  - `visitor.numOfPage` -当前聊天的visitor访问当前站点页面的数量
  - `visitor.location` -当前聊天的visitor的地址
    + `ip` -ip地址
    + `city` -城市
    + `state` -州、省
    + `country` -国家
  - `visitor.device` -当前聊天的visitor的设备信息
    + `os` -操作系统
    + `browser` -浏览器
    + `screenResolution` -屏幕分辨率
    + `language` -语音
    + `timezone` -时区
  - `visitor.history` -当前聊天的visitor的历史记录
    + `firstVisitorTime` -首次访问时间
    + `visitTimes` -访问次数
    + `chatTimes` -聊天次数
  - `visitor.visitorSegmentations` -当前聊天的visitor的细分数组
  - `visitor.customVariables` -当前聊天的visitor的自定义变量
    + `name` -变量名
    + `value` -变量值
  - `visitor.ssoFlag` -当前聊天的visitor的SSO标志

### Chat Object
  `currentChat` -当前聊天对象

  get
  ```javascript
    client.get("currentChat").then(function(currentChat){
      console.log(currentAgent);
      /*
      {
        id: 1,  // number
        visitorId: 1, // number
        status: ''  // string,  chatting/waiting/transferring/chat ended/audio chatting/video chatting/inviting
        name: '',     // string
        email: '',    // string 
        company: '',  // string
        phone: '',    // string
        productService: '', // string
        department: '',     // string, name of department
        fields: [
            {
            name: '',   // string
            value: '',  // string
            }
        ]
        rating: {
            score: 1,   // number, 0 - 5
            comment: '',  // string,
        }
        agents: [], // array<string>, agent's name
        requestPage: {
            title: '',  // string
            url: '',    // string
        },
        requestTime: 1502934947,  // number, unix time
        waitingTime: 15,  // number, how long the visitor waiting time, unit(second)
        duration: 180, //number, how long the chat duration, unit(second)、
        messages: [
            {
            sender: '',
            senderType: '', // string, system/agent/visitor
            time: 1502934947,
            content: '',  // string, html 
            }
        ]
      }
      */
    });

    client.get("currentChat.messages").then(function(messages){
      console.log(messages);
    }
  ```

Properties
  - `chat.id` -当前聊天的Id
  - `chat.visitorId` -当前聊天的访客id
  - `chat.name` -当前聊天的访客名称
  - `chat.email` -当前聊天的访客邮箱
  - `chat.status` -当前聊天的状态 `chatting/waiting/transferring/chat ended/audio chatting/video chatting/inviting`
  - `chat.company` -当前聊天的访客的公司
  - `chat.phone` -当前聊天的访客的电话
  - `chat.fields` -当前聊天的访客填入的字段信息
    + `name` -字段名
    + `value` -字段值
  - `chat.rating` -当前聊天的访客评分
    + `score` -分值
    + `comment` -备注
  - `chat.agents` -当前聊天的客服数组
  - `chat.requestPage` -当前聊天访客的初始请求页面
    + `title` -页面标题
    + `url` -页面地址
  - `chat.requestTime` -当前聊天的访客的请求时间
  - `chat.waitingTime` -当前聊天的访客的等待时间
  - `chat.duration` -当前聊天的持续时间
  - `chat.messages` -当前聊天的信息
    + `sender` -信息发送对象
    + `senderType` -信息发送类型， `system/agent/visitor`
    + `time` -信息发送时间
    + `content` -信息内容

### ChatSideBar Actions
  在ChatSideBar中，App中可使用下面的行为:
  - [Chat Acionts](#chatsidebar-chat-actions)

#### ChatSideBar Chat Actions
  在ChatSideBar中，对于聊天对象app可用的行为如下：
  - `send` -在当前聊天中发送一条信息
  - `input` -在当前聊天的输入框中插入一条信息

```javascript
  client.do("currentChat.send","newMessage");
  client.do("currentChat.input","inputMessage");
```

### ChatSideBar Events
  在ChatSideBar中，对于聊天对象可用的事件如下：
  - [chats.chatStart](#chats-start)
  - [chats.chatEnd](#chats-end)
  - [Chats.selectChange](#chats-select-change)` 
  - [currentChat.submitWrapup](#chat-submit-Wrapup)`
  - [currentChat.receiveVisitorMessage](#chat-receive-visitor-message)`
  - [currentChat.visitor.status.change](#visitor-status-change)

#### Chats Start
  `chats.chatStart`事件发生在聊天开始的时候，开发者可以通过该事件指定需要在聊天开始的时候所做的事情，该事件的处理程序接收一个[Chat](#chat-object)对象。

  ```javascript
    client.on('chats.chatStart',function(chat){
        //handler code
    });
  ```

#### Chats End
  `chats.chatEnd`事件发生在聊天结束的时候，开发者可以通过该事件指定需要在聊天结束的时候所做的事情，该事件的处理程序接收一个[Chat](#chat-object)对象。

  ```javascript
    client.on('chats.chatEnd',function(chat){
        //handler code
    });
  ```
  
#### Chats Select Change
  `chats.selectChange`事件发生在聊天选择变更的时候，开发者可以通过该事件指定需要在聊天选择变更的时候所做的事情，该事件的处理程序接收一个[Chat](#chat-object)对象。

  ```javascript
    client.on('chats.selectChange',function(chat){
        //handler code
    });
  ``` 

#### Chat Submit Wrapup
  `currentChat.submitWrapup`事件发生在聊天提交Wrapup的时候，开发者可以通过该事件指定需要在聊天提交Wrapup的时候所做的事情，该事件的处理程序接收一个[Chat](#chat-object)对象。

  ```javascript
    client.on('currentChat.submitWrapup',function(chat){
        //handler code
    });
  ``` 

#### Chat Receive Visitor Message
  `currentChat.receiveVisitorMessage`事件发生在当前聊天接收到访客信息的时候，开发者可以通过该事件指定需要在当前聊天接收到访客信息的时候所做的事情，该事件的处理程序接收一个`message`字符串。

  ```javascript
    client.on('currentChat.receiveVisitorMessage',function(message){
        //handler code
    });
  ``` 

#### Visitor Status Change
  `currentChat.visitor.status.change`事件发生在当前聊天的访客状态发生变更的时候，开发者可以通过该事件指定需要在聊当前聊天的访客状态发生变更的时候所做的事情，该事件的处理程序接收一个[Visitor](#visitor-object)对象。

  ```javascript
    client.on('chats.chatStart',function(visitor){
        //handler code
    });
  ```

## Agent Console Background
  指定App在Agent Console中以后台形式(不显示UI)启动的页面，一般用于App初始化或持续运行的一些服务。

  ```json
  "location": {
    "agentConsole_background": "/assets/agentConsole_initial.html"
  }
  ```

### Agent Console Background Events
  除了框架本身的一些[核心事件](#core-events)外，在Agent Console的Background中还可以使用下面的事件来进行App的开发。
  - [chats.chatStart](#chats-start)
  - [chats.chatEnd](#chats-end)



