# General 新增

1. [Objects](#objects)

## Objects
  - [Chat Object](#chat-object)
  - [PopupWindow Object](#popupWindow-object)
  - [HeadTag Object](#headTag-object)
  - [ToolItem Object](#toolItem-object)

### Chat Object
#### currentChat
- Properties
   + `currentChat.headTags` -当前聊天的访客的所有tag对象集合
   + `currentChat.toolItems` -当前聊天的toolItem对象集合

- Actions
   + `get` -获取当前访客的所有Tag/ToolItem对象
   + `set` -设置当前访客的Tag/ToolItem对象

```javascript
  var headTags = Comm100AgentConsoleAPI.get("agentconsole.currentChat.headTags");

  const newHeadTag = {
    name: "myHeadTag",
    icon: "https://***.ico",
    tip: "myHeadTag"
  }
  headTags.add(newHeadTag);
  Comm100AgentConsoleAPI.set("agentconsole.currentChat.headTags",headTags);
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
  + `open` -弹出一个窗口
  + `close`
    
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

  Comm100AgentConsoleAPI.do("agentconsole.popupWindow.open",popupWindow);
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
  + `headTag.actived` -当点击headTag的时候触发

```javascript
    Comm100AgentConsoleAPI.on("agentconsole.headTag.actived",function(headTag){
        if("myHeadTag" == headTag.name){
            //handler code
        }
    });
``` 

### ToolItem Object
  Agent Console的聊天页面中聊天窗口中间的ToolBar里面的对象。
  - Properties
    + `toolItem.name` -toolItem对象的名称
    + `toolItem.icon` -toolItem对象的图标

```javascript
  const toolItem = {
      name: "myToolItem",
      icon: "https://***.ico"
  }
```

- Events
  + `toolItem.actived` -当点击toolItem的时候触发

```javascript
    Comm100AgentConsoleAPI.on("agentconsole.toolItem.actived",function(toolItem){
        if("myToolItem" == toolItem.name){
            //handler code
        }
    });
``` 