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
  - invoke
  - on
  - addEvent
  - removeEvent
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

### client.invoke(Name [,...args])
  调用`name`标识的操作，根据要求传递参数，返回一个`promise`对象。
  
  ```javascript
    var client = Comm100AgentConsoleAPI.init();
    client.invoke("preload").then(function(){
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

### client.removeEvent(hame handler)
  给当前实例移除一个`name`事件。

  ```javascript
  var client = Comm100AgentConsoleAPI.init();

  client.removeEvent("comming_call",function(){
      //handler code
  });
  ```

### client.addEvent(hame handler)
  给当前实例增加一个`name`事件。

  ```javascript
  var client = Comm100AgentConsoleAPI.init();

  client.addEvent("comming_call",function(){
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

    client.addEvent("comming_call",function(){
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
  表示App的所有正在运行的实例，每一个iframe都是一个实例。同一个App在Manifest中定义了多个位置，则这个App就存在多个App Instance。

  get
  
  ```javascript
    var instancesData = client.get('instances').then(function(instancesData){
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
    client.invoke("resize",{
        width: "300px",
        height:"200px"
    });
  ```

#### Instance Create Action
  创建一个App的实例，实例属性包含`location`和`instance_id`两个属性，其中`instance_id`属性不指定时，Comm100将自动生成一个实例id，推荐不指定该属性。

  ```javascript
    client.invoke("instance.create",{
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
  - [agentConsole navigationBar](#agent-console-navigations) -Agent Console的左侧列表菜单区域。
  - [agentConsole chatSideBar](#agent-console-chatsidebar) -Agent Console的聊天窗口的右侧区域。
  - [agentConsole background](#agent-console-background) -Agent Console中以后台形式(不显示UI)启动的页面。


  开发者可以在Manifest文件中定义App的所在位置，具体参考[Setting The Location](https://github.com/hgq719/docs/blob/master/open-platform.md#setting-the-location)。  
  如果开发者指定`agentconsole_topBar`，App只展示一个图标，点击图标可以打开这个App。

## All Locations
  下面的这些对象、属性及操作在Agent Console中的所有位置都是可用的。

  Objects
  - [agent object](#agent-object)


  Additional Properties
  - [visible](#visible-property)


  Additional actions
  - [hide](#hide-action)
  - [show](#show-action)
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

### Additional Properties
#### Visible Property
  `visible` -指定当前app是否是显示状态

  get
  ```javascript
  client.get("visible").then(function(data){
      console.log(data); //{"visible":true}
  });
  ```

### Additional Actions  
#### Hide Action
 `hide` -隐藏当前app的实例

 ```javascript
 client.invoke("hide");
 ```

 #### Show Action
 `show` -显示当前app的实例

 ```javascript
 client.invoke("show");
 ```

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
+ `data`-展示通知相关的数据，一般为`json`格式

 ```javascript
  // body struct
  const notification =  {
    body: "there is a phone call for you!",
    renotify: "true", //是否替换之前的通知
    sound: "https://***/call.mp3" ,  //来电声音
    location: {      
      notificationArea: true,    //右下角通知区域闪动，点击后激活AgentConsole
      navigationBar: true,       //左侧List菜单区域，点击后打开Manifest中配置的list页面
      topBar: true               //右上角全局菜单区域，点击后打开Manifest中配置的菜单页面
    },
    data: {     //展示通知相关的任意类型的数据
      //custom data
    }
  }

  client.invoke("notify",notification);
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
+ `visible`-弹出窗口的显示状态: show/hide/toggle 默认show
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

  client.invoke("popup",popupWindow);
```

## Agent Console TopBar

## Agent Console NavigationBar

## Agent Console ChatSideBar

## Agent Console Background
  