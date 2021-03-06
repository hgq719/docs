
# General

1. [用户可通过定义下面形式的Manifest文件来将phone引入进来](#phone-manifest)
2. [用户可以通过manifest配置一个Agent Console端全局菜单及页面用来显示phone的功能及配置](#agentconsole-global-menu)
3. [用户可以通过manifest中的配置添加一个Agent Console NavigationBar](#agent-console-navigationBar)
4. [用户可以通过manifest中的配置添加一个Agent Console SideBar](#agent-console-mychats-sidebar)
5. [用户可以通过manifest中的配置添加一个Agent Console Background](#agent-console-background)
6. [用户可以通过Manifest中的配置添加一个后台管理页面](#phone-manage)
7. [用户可以通过API设置topbar菜单弹出页面的大小及显示状态](#topbar-popupwindow)
8. [用户可以通过API获取/设置Agent状态](#agent-status)
9. [自定义通知](#custom-notification)
# 开放平台 Phone的接入点

## phone manifest

用户可通过定义下面形式的Manifest文件来将phone引入进来。

```json
{
  "name": "Comm100phone", //App的名字
  "author": {
    "name": "Comm100", //开发者的名字
    "email": "developer@comm100.com",  //开发者的邮箱
    "url": "https://www.comm100.com/phone" //开发者的主页地址或App的主页地址
  },
  "private": false,  //该APP是否是私有APP的标志
  "version": "1.0",
  "frameworkVersion": "2.0",
  "location": {
    "agent": {
      "topbar": "/topbar/index.html",
      "navigationBar": "navigationBar/list.html",
      "chat_tabSide":"/chat_tabSide/index.html",
      "background": "/assets/inital.html"
    },
    "admin": {
      "productBar": "/manage/index.html"
    }
  }
}
```

## AgentConsole Global Menu

用户可以在AgentConsole端配置一个全局菜单用来处理Phone的相关操作及配置；可以在APP的manifest中可以声明这个菜单.

```json
  {
    "location": {
      "agent": {
        "topbar": "/topbar/index.html"      //AgentConsole顶部全局菜单
      }
    }
  }
```

1. 安装APP以后, 会在AgentConsole的右上角区域显示phone的菜单, 点击phone以默认方式进入到phone的操作及配置界面，用户也可以通过API对弹出方式和样式进行设置
2. 菜单点击默认在菜单的下方合适区域展示一个div, div加载用户配置的这个页面`/topbar/index.html`
  - 具体的url可能为`https://hosted.comm100.com/apps/phone/index.html`
3. 该页面的权限配置及身份认证同LiveChat的Agentconsole上增加一个配置菜单

## Agent Console NavigationBar

用户可以通过manifest中的配置添加一个Agent Console NavigationBar, Agent Console的左侧导航菜单会添加title中菜单，点击该菜单会显示`/navigationBar/index.html`页面

```json
  {
    "location": {
      "agent": {
        "navigationBar": "navigationBar/list.html"
      }
    }
  }
```

## Agent Console Mychats Sidebar

用户可以通过manifest中的配置添加一个Agent Console Mychats SideBar, Agent Console的Chats右侧菜单会显示`/sidebar/index.html`页面

```json
  {
    "location": {
      "agent": {
        "chat_tabSide": "/chat_tabSide/index.html"    //聊天页面的tab区域
      }
    }
  }
```
## Agent Console Background

用户可以通过manifest配置一个Agent Console Background页面，该配置页面不会在系统中展示出来，但是会在系统启动的时候加载这个页面，可用该页面来做一些app初始化工作

```json
  {
    "location": {
      "agent": {
        "background": "/assets/inital.html"
      }
    }
  }
```

## Control Panel Phone Manage

用户可以通过Manifest中的配置在Control Panel后台添加一个ProductBar产品级菜单，Control Panel的右上角会显示`/manage/phoneManage.html`页面，用户可以用来进行Phone的管理及配置，如Agent与分机号的配置.

```json
{
  "location": {
    "admin": {
      "productBar": "/manage/phoneManage.html"
    }
  }
}
```

获取Agent列表：用户可以获取Agent列表的信息来配置Agent与电话的对应关系

1. Request

`GET 'https://hosted.comm100.com/livechatapi/operators'`

2. Response

```json
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
  }
]
```

保存Agent与电话的对应关系:用户可以通过下面的API来保存和获取agent与电话的对应关系；或者由用户自己进行维护

```javascript
  const relations = {
    siteId: 10000,
    relation:[{
      agentId: "12312hjka80asjfp",
      phoneNo: "078451356-697"  
    },{
      agentId: "7879hgktuif12313",
      phoneNo: "078451356-698"  
    }]
  }

Comm100AgentConsoleAPI.set("agentconsole.app.metadata",relations);
Comm100AgentConsoleAPI.get("agentconsole.app.metadata");
```

## TopBar PopupWindow

用户在点击Topbar全局菜单的时候，系统会在按钮下方的合适位置自动生成一个Pane区域，并激活pane.activated事件，将Manifest中Topbar中设置的`/chat_tabSide/index.html`的内容加载到pane的iframe中，可以通过下面的API设置弹出区域的大小及显示状态

```javascript
  const popupWindow = {
    size: {
      width: '300',
      height: '200'      
    },
    location: "TopRight",   //弹出区域位置：TopRight/Center/BottomRight/绝对位置对象{left/right:10px;top/bottom:10px} 
    ifModal: false, //是否是模态窗口: true/false 默认false
    visible: "show"  //显示状态: show/hide/toggle 默认show
  }
```
```javascript
  Comm100AgentConsoleAPI.on("topbar.pane.activated", function(){
    //当用户点击topbar菜单，激活popupWindow的时候进行的处理，如设置页面大小
    Comm100AgentConsoleAPI.set("topbar.popupWindow.size",{
      width:300,
      height:200
    });

    Comm100AgentConsoleAPI.set("topbar.popupWindow.visible","show");
  });
```
```javascript
  Comm100AgentConsoleAPI.on("topbar.pane.deactivated", function(){
    //在已经激活popupWindow的情况下，当用户再点击topbar菜单
    //handler code
  });
```

用户可以在Mainifest中Location的Backgroud的配置页面`/assets/inital.html`中，在登录完成后通过下面的API将Pane区域预先加载进来
```javascript
  Comm100AgentConsoleAPI.do("topbar.pane.preload", function(){
    //handler code
    Comm100AgentConsoleAPI.set("topbar.popupWindow.size",{
      width:300,
      height:200
    });

    Comm100AgentConsoleAPI.set("topbar.popupWindow.visible","show");
  });
```

## Agent Status

获取Agent的聊天状态：用户可以通过下面的API来获取当前的Agent的Status的值，来判断是否对Agent分配phone;

```javascript
  const status = Comm100AgentConsoleAPI.get("agentconsole.currentAgent.Status");   //available;busying;away
```

设置Agent的聊天状态：用户可以通过API设置agent的status状态，可以设置让Agent在接电话的时候不接聊天;

```javascript
  // body struct
  const status =  "available"; //available;busying;away
  
  Comm100AgentConsoleAPI.set("agentconsole.currentAgent.status",status);
```

Agent的电话状态：Agent的电话状态完全由App本身控制

## Custom Notification

通知提醒：用户在接收到Phone的时候可以通过下面的Agentconsol API对当前的Agent进行通知提醒

```javascript
  // body struct
  const notification =  {
    body: "there is a phone call for you!",
    icon: "https://***/icon.gif",
    renotify: "true", //是否替换之前的通知
    sound: "https://***/call.mp3" ,  //来电声音
    notificationLocation: {      
      notificationArea: true,    //右下角通知区域闪动，点击后激活AgentConsole
      navigationBar: true,       //左侧List菜单区域，点击后打开Manifest中配置的list页面
      topBar: true               //右上角全局菜单区域，点击后打开Manifest中配置的菜单页面
    },
    data: {     //展示通知相关的任意类型的数据
      callFrom: "158********",
      location: "changsha, china",
      callType: "inbound"
    }
  }

  Comm100AgentConsoleAPI.do("agentconsole.notification.sent",notification);
```