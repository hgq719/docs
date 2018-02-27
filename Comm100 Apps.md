# General

1. [Manifest](#manifest-reference)
3. [CAF SDK](caf-sdk)
3. [CAF Client API](client-api)
5. [Apps Core API](apps-core-api)
6. [Apps LiveChat API](apps-livechat-api)

## Manifest Reference
  Comm100 Apps Framework(CAF)能让开发者在自己的Comm100产品中增加功能、开发第三方集成。所有的App都有一个`Manifest.json`文件。开发者可以在该文件中指定自己的app安装在Comm100产品的一个或者多个位置，例如`TopBar`或聊天窗口的`TabBar`中。开发者可以指定在这些位置的iframe中显示的页面地址，如：

   ```json
   "location": {
     "agentConsole_chatTabBar":  "assets/index.html"    
   }
   ```
   
   详情可参考[Manifest Reference](https://github.com/hgq719/docs/blob/master/ManifestReference.md)。   
   
## CAF SDK
  使用CAF SDK可以让开发者的app与Comm100的Apps开发框架进行交互，需要导入CAF SDK，如：

   ```javascript
    <script src="https://hosted.comm100.com/apps/sdk/1.0/comm100SDK.js"></script>
   ```   

## Cient API
  在CAF SDK中提供了一个叫做`Comm100Client`的全局对象，开发者可以通过这个client来监听事件、获取或设置对象属性、或调用方法等。如：

  ```javascript
  var client = Comm100ClientAPI.init();
  client.get("currentAgent.name").then(function(data){
      console.log(data); //{"currentAgent.name":"kim"}
  });
  ```
### Client Object
  - Actions
    + init -返回一个[client](#client-object)

  ```javascript
    Comm100ClientAPI.onReady = function () {
      // when this callback is triggered,
      // all APIs are ready to use
      var client = Comm100ClientAPI.init();
    }
  ```

### Client Methods
  - [context](#client-context)
  - [get](#client-get)
  - [instance](#client-instance)
  - [do](#client-do)
  - [on](#client-on)
  - [off](#client-off)
  - [set](#client-set)
  - [trigger](#client-trigger)


#### Client Context
  `client.context()` -请求当前对象的上下文信息，包括当前实例的id、位置等信息，返回一个`promise`对象。

  ```javascript
    var client = Comm100ClientAPI.init();
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

#### Client Get
  `client.get(parameters)` -获取当前参数对应的值，返回一个`promise`对象。

  ```javascript
    var client = Comm100ClientAPI.init();
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

#### Client Instance
  `client.instance(instanceId)` -App的每一个位置都是一个单独的实例，可以通过该方法来初始化App的一个特定位置的实例，用在实例间信息交互的时候。

  ```javascript
    var client = Comm100ClientAPI.init();
    var otherClient = Comm100ClientAPI.instance("013B7322-6895-F01E-5EAE-F4DF50016AF5");
  ```

#### Client Do
  `client.do(name [,...args])` -调用`name`标识的操作，根据要求传递参数，返回一个`promise`对象。
  
  ```javascript
    var client = Comm100ClientAPI.init();
    client.do("preload").then(function(){
        //handler code
    });
  ```

#### Client On
  `client.on(name, handler)` -在当前实例指定的`name`事件时，执行handler事件。

  ```javascript
  var client = Comm100ClientAPI.init();

  client.on("app.loaded",function(){
      //handler code
  });
  ```

  也可以通过`on`给当前实例添加一个`name`事件。

  ```javascript
  var client = Comm100ClientAPI.init();

  client.on("comming_call",function(){
      //handler code
  });
  ```

#### Client Off
  `client.off(name, handler)` -给当前实例移除一个`name`事件。

  ```javascript
  var client = Comm100ClientAPI.init();

  client.off("comming_call",function(){
      //handler code
  });
  ```

#### Client Set
  `client.set(key, value)` -设置当前`key`对应的属性的值为`value`，返回一个`promise`对象。

  ```javascript
  var client = Comm100ClientAPI.init();

  client.set("currentChat.email",email).then(function(){
      //handler code
  });
  ```

#### Client Trigger
  `client.trigger(name, [data])` -触发指定的`name`的事件，`data`为该事件的参数

  ```javascript
    var client = Comm100ClientAPI.init();

    client.on("comming_call",function(){
        //handler code
    });

    client.trigger("comming_call");
  ```

## Apps Core API
  在所有可支持Comm100 Apps framework的Comm100的产品的任何位置，都可以使用下面这些核心事件、属性及方法：
  - [Core Events](#core-events)
  - [Core Properties](#core-properties)
  - [core Actions](#core-actions)

### Core Events
  - [app.loaded](#app-loaded)
  - [app.activated](#app-activated)
  - [app.deactivated](#app-deactivated)
  - [instance.created](#instance-created)

#### App Loaded
  当App加载的时候触发的事件。

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
  当一个App的实例被创建的时候，其他的实例将收到`instance.created`事件通知。

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
  - [instances.create](#instance-create-action)

#### Resize Action
  重新设置App所在的iframe的页面大小，大小规格中的`width`和`height`可以是`px`、`%`或`vw/vh`。

  ```javascript
    client.do("resize",{
        width: "300px",
        height:"200px"
    });
  ```

#### Instances Create Action
  创建一个App的实例，实例属性包含`location`、`url`两个属性，目前`location`只支持`modal`，用来创建一个模态窗口的实例。

  ```javascript
    client.do("instances.create",{
        location: "modal",
        url:"****.html"
    });
  ```