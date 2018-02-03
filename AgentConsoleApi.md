# General 新增

1. [Objects](#objects)

## Objects
  - [Chat Object](#chat-object)
  - [PopupWindow Object](#popupwindow-object)
  - [HeadTag Object](#headtag-object)
  - [ToolItem Object](#toolitem-object)
  - [App Object](#app-object)

### Chat Object
#### currentChat
- Properties
   + `currentChat.currentApp.customHeadTags` -当前聊天访客、当前App的所有自定义tag对象集合
   + `currentChat.currentApp.customToolBarItems` -当前聊天、当前App的所有自定义toolBarItem对象集合

- Actions
   + `get` -获取当前App的所有自定义Tag/ToolItem对象
   + `set` -设置当前App自定义Tag/ToolItem对象

```javascript
  var headTags = Comm100AgentConsoleAPI.get("agentconsole.currentChat.currentApp.customHeadTags");

  const newHeadTag = {
    name: "myHeadTag",
    icon: "https://***.ico",
    tip: "myHeadTag"
  }
  headTags.add(newHeadTag);
  Comm100AgentConsoleAPI.set("agentconsole.currentChat.currentApp.customHeadTags",headTags);
```

### PopupWindow Object
  Agent Console中弹出对话框对象。

#### currentPopupWindow
- Properties
    + `popupWindow.name` -弹出窗口的名称
    + `popupWindow.title` -弹出窗口的标题
    + `popupWindow.size`-弹出区域的大小
      * `width`-弹出区域的宽度
      * `height`-弹出区域的高度
    + `popupWindow.location`-弹出区域位置：TopRight/Center/BottomRight/绝对位置对象{left/right:10px; top/bottom:10px} ,默认值为Center，即页面中间位置
    + `popupWindow.ifmodal`-是否是模态窗口：true/false 默认false
    + `popupWindow.visible`-弹出窗口的显示状态: show/hide/toggle 默认show
    + `popupWindow.url` -弹出窗口展示的内容地址


- Actions
  + `create` -弹出一个窗口
    
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

  Comm100AgentConsoleAPI.do("agentconsole.popupWindow.create",popupWindow);
```

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

- Events
  + `customeHeadTag.actived` -当点击当前App的自定义headTag的时候触发

```javascript
    Comm100AgentConsoleAPI.on("agentconsole.customeHeadTag.actived",function(headTag){
        if("myHeadTag" == headTag.name){
            //handler code
        }
    });
``` 

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

- Events
  + `customToolBarItem.actived` -当点击toolItem的时候触发

```javascript
    Comm100AgentConsoleAPI.on("agentconsole.customToolBarItem.actived",function(toolBarItem){
        if("myToolBarItem" == toolBarItem.name){
            //handler code
        }
    });
``` 

### App Object
  Agent Console中的App对象。
  - Properties
    + `metadata` -Site级别的App元数据信息，保存数据的格式为json格式
    + `agent.metadata` -Agent级别的App元数据信息
    - `object.{objectName}` -App中导入的外部对象的值，其中objectName为导入的外部对象的名称

  - Actions
    + `get` -获取当前App对象的属性
    + `set` -设置当前App对象的属性

    
```javascript
  var appMetadata = Comm100AgentConsoleAPI.get("app.metadata");

  const metadata = {  //自定义json对象
    name: "firstCustomField",
    type: "customValue"
  }
  Comm100AgentConsoleAPI.set("app.metadata",metadata);
```