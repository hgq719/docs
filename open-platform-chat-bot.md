
# General

1. [用户可通过定义下面形式的Manifest文件来将自己的Bot引入进来](#bot-manifest)
2. [用户可以通过manifest配置一个顶级菜单及页面用来显示Bot的功能配置](#product-menu)
3. [用户可以通过manifest中的配置添加一个Agent Console SideBar](#agent-console-sidebar)
4. [用户可以通过manifest中Bot的配置接入一个自己的Bot系统](#external-bot)
5. [用户可以通过manifest中访客端的js配置,接入处理Bot消息的接口](#visitor-side-handle-bot-message)
6. [Campaign中关于bot的配置在Live Chat中写死,暂时不提供开放性](#campaign-bot)
7. [Manifest中可用宏定义](#micro-define)
# 开放平台 Chat Bot的接入点

## Bot manifest

用户可通过定义下面形式的Manifest文件来将自己的Bot引入进来。


```json
{
  "name": "Comm100Bot", //App的名字
    "author": {
      "name": "Comm100", //开发者的名字
      "email": "developer@comm100.com",  //开发者的邮箱
      "url": "https://www.comm100.com/bot" //开发者的主页地址或App的主页地址
    },
  "private": false,  //该APP是否是私有APP的标志
  "version": "1.0",
  "frameworkVersion": "2.0",
  "location": {
    "Menu": {
      "level": 1,
      "name": "Bot",
      "url": "/manage/index.html"
    },
    "chat": {
      "agent": {
        "chatsSidebar": "/sidebar/index.html",
      },
      "visitor": {
        "customCSS": [
          "/assets/visitor_custom_css.css"
        ],
        "customJS": [
          "/assets/visitor_custom_js.js"
        ],
      },
      "bot": {
        "endpoint": {
          "list": {     //机器人列表Endpoint配置
            "method": "POST",
            "url": "https://api.chatbot.com/comm100/{siteId}/bots", // {siteId}为宏, Comm100在处理这个地址时会替换掉这个参数
            "headers": [
              "Authorization": "Bearer {app.metadata.token}", // {app.metadata.token} 为后台安装这个app时设置的元数据, 
              "x-api-version": "v2",
            ]
          },
          "message": {   //机器人列表回答问题Endpoint配置
            "method": "POST", //必须为post
            "url": "https://api.chatbot.com/comm100/{siteId}/bots/{botId}/message", // {botId}为宏参，表示使用的bot Id, 用户可以选择设置或者不设置, body中的内容也会有botId的属性
            "headers": [
              "Authorization": "Bearer {app.metadata.token}", // {app.metadata.token} 为后台安装这个app时设置的元数据, 
              "x-api-version": "v2",
            ]
          }
        }
      }
    }
  },
}
```

## Product Menu

用户可以配置一个顶级菜单及页面用来配置Bot的功能配置, 可以在APP的manifest中可以声明一个产品级菜单的功能

```json
  {
    "location": {
      "product": {
        "name": "Bot",
        "title": "Bot",
        "url": "/manage/index.html"
      }
    }
  }
```

1. 安装APP以后, 会在后台一级菜单上显示一个Bot的菜单, 点击Bot进入到配置界面
2. 菜单下面的内容为一个iframe, iframe加载用户配置的这个页面`/manage/index.html`
  - 具体的url可能为`https://hosted.comm100.com/apps/chat-bot/manage/index.html`
3. 该页面的权限配置及身份认证同LiveChat后台菜单上增加一个配置页面

## Agent Console Sidebar

用户可以通过manifest中的配置添加一个Agent Console SideBar, Agent Console的Chats右侧菜单会显示`/sidebar/index.html`页面

```json
  {
    "location": {
      "chat": {
        "agent": {
          "chats_sidebar":  "/sidebar/index.html"
        }
      }
    }
  }
```

## External Bot

用户可以通过manifest中Bot的配置接入一个自己的Bot系统, 这个bot会参与到聊天的分配，并且在特定的时候会调用bot提供的两个接口

```json
  {
    "location": {
      "chat": {
        "bot": {
          "endpoint": {
            "list": {
              "method": "GET",
              "url": "https://api.chatbot.com/comm100/{siteId}/bots", // {siteId}为宏, Comm100在处理这个地址时会替换掉这个参数
              "headers": [  //  用户可以自定义请求头
                "Authorization": "Bearer {app.metadata.token}", // {app.metadata.token} 为后台安装这个app时设置的元数据, 
                "x-api-version": "v2",
              ]
            },
            "message": {
              "method": "POST", //必须为post
              "url": "https://api.chatbot.com/comm100/{siteId}/bots/{botId}/message", // {botId}为宏参，表示使用的bot Id, 用户可以选择设置或者不设置, body中的内容也会有botId的属性
              "headers": [
                "Authorization": "Bearer {app.metadata.token}",
                "x-api-version": "v2",
              ]
            }
          }
        }
      }
    }
  }
```

### Bot List

用户加载campaign >> bot页面时请求对应的接口获取具体的bot列表, 另外Chat Server将聊天分配到具体的bot时，需要从这个接口重新获取列表，检查列表中的具体id的bot, 读取name, avatar, greetingMessage等信息用作具体的聊天 

  1. Request

  `GET 'https://api.chatbot.com/comm100/10000/bots'`

  2. Response

  ```json
    [
      {
        "id": "@bot_id",
        "name": "Bot 1",
        "avatar": "https://cdn.chatbot.com/avatar/ig923udjfoew89.png",
        "greetingMessage": "Hello {visitor.name}, I'm ChatBot. What can I do for you?",
        "language": "en_us"
      }
    ]
  ```

### Bot Engine Handle Visitor Message

  1. Chat Server收到visitor的消息时会将使用下面的Request来请求message接口

  `POST 'https://api.chatbot.com/comm100/10000/bots/i934ru90ruoewq/message'`

  ```javascript
  // body struct
  const botMessage =  {
    siteId: 10000,
    botId: '@bot_id',
    chatId: 28888,
    visitor: {
      id: 77777777,
      name: 'Allon',
      email: 'allon.lu@comm100.com',
      phone: '18888888888',
      ssoId: ''
      customFields: [
        {
          name: 'product',
          value: 'livechat,ticket',
        }
      ],
      customVariable: [
        {
          name: 'age',
          value: '88',
        }
      ],
    }
    message:       
    {    
      type: "question",   //question / action / custom  
      ...... 
      //消息主体，包括访客问的问题、访客进行的操作、用户自定义消息三个大类
      //如下所示
    }
  }
  ```

  Question Message Body

  ```javascript
    const questionMessage = {
      type: 'question',  
      transcript: 'I have submit this form.',
      content: [{
        contentType : "text",    // text/image/file
        contentValue: "I want to buy some apple"
      },{
        contentType : "image",    
        contentValue: {
          name: "***.png",
          url: "*****/***.png"
        }
      },{
        contentType : "file",    
        contentValue: {
          name: "***.doc",
          url: "*****/***.doc"
        }
      }] 
    }
  ```

  Action Message Body

  ```javascript
    const actionMessage = {
      type: 'action',  
      transcript: 'I have submit this form.',
      content: {
        contentType: "Form",
        contentValue:[{
          fieldName: "age",
          fieldValue: 20
        },{
          fieldName: "sex",
          fieldValue: "female"
        },]
      }
    }
  ```

  ```javascript
    const actionMessage = {
      type: 'action',  
      transcript: 'I have submit this form.',
      content: {
        contentType: "helpful",
        contentValue:{
          messageId: "has79fasjhfla0",
          intentId: "hjkashdf797a9sf",
          ifHelpful: true    //是否有帮助， helpful： true   nothelpful ： false
        }
      }
    }
  ```

  Custom Message Body

  ```javascript
    const actionMessage = {
      type: 'custom',  // text/image/file
      transcript: 'this is a custom message.',
      content: { 
        // 动态对象, custom类型用户可以设置任意的属性和值, 
        // 这个对象是由Bot自己在访客端提交的时候定义的, 在bot engine中处理
      }
    }
  ```

  2. Bot收到ChatServer转发过来的问题后，可返回标准的Message/form类型的答案，也可以返回custom类型的用户自定义答案，如下：

  Message response Anwser
  
  ```javascript
    const messageAnswer = {
      type: 'message',   //消息类型： message/form/custom
      transcript: 'This is a message answer!',    //用于ChatServer保存聊天记录脚本
      messageId: "jlkasdf7979asfhkah",
      content: [                          //真实消息内容，用于标准化答案或自定义答案处理
        {
          contentType : "text",    //text/htmlLink/intentLink/image/signIn
          contentValue: "Sure,here are some apples Image FYI,please click the"
        },{
          contentType : "htmlLink",  
          contentValue: {
            textDisplay: "link",
            url: "http://******html",
            openIn: "SideWindow", //打开方式 :NewWindow/Tab;CurrentBrowserWindow;SideWindow
            pushPage: true
          }
        },{
          contentType : "text",
          contentValue: "to buy them"
        },{
          contentType : "intentLink",
          contentValue: {
            textDisplay: "link",
            intentId: "696asdhfashlfa070",
            intentName: "intall"
          }
        },{
          contentType : "image",
          contentValue: {
            name: "apple.png",
            url: "https://resources.chatbot.com/download/ig923udjfoew89"
          }
        }
      ],
      ifDisplayHelpful: true  //是否需要helpful/nothelpful按钮，true：需要 false：不需要
    }
  ```

    signin response Answer

  ```javascript
    const signInResponse = {
      type: 'message',
      transcript: 'Please verify yourself by signing into your account.',  //用于ChatServer保存聊天记录脚本
      messageId: "jlkasdf7979asfhkah",
      content:   //真实消息内容，用于标准化答案或自定义答案处理
      {
        contentType : "signIn",     //Signin类型为一类特殊的message答案
        contentValue: {
          textDisplay: "Sign in",
          ifVisitorSSO: false             //是否是SSO标记
          url: "http://******html",       //如果ifVisitorSSO标记为false的情况，url可设置为空，由系统自动生成登录地址；否则需要设置相应的SignIn地址
          openIn: "SideWindow", //打开方式 :NewWindow/Tab;CurrentBrowserWindow;SideWindow
          pushPage: false,
          question: "I want apples",                   //用于访客登录成功后将问题重新发回到bot在访客端的显示
          intentId: "asdfaj423402sajfl",               //用于Bot直接通过之前查询的意向结果直接返回答案
          intentdName: "I want to buy some apples!",   //和intentId用途一致，如果不需要可为空
        }
      },
      ifDisplayHelpful: false  //是否需要helpful/nothelpful按钮，true：需要 false：不需要
    }
  ```

  form response Answer
  
  ```javascript
    const formAnswer = {
      type: 'form',
      transcript: 'This is a webhook answer!',  //用于ChatServer保存聊天记录脚本
      messageId: "jlkasdf7979asfhkah",
      content: //真实消息内容，用于标准化答案或自定义答案处理
      {
        fields:[
          {
            type: "Dropdownlist",
            name: "Fruit",
            required: true,
            masked: true,
            entity:{
              id: "hlahfs797897ashf",
              name: "Fruit"
            },
            options: ["Apple","Banana","Pear"]
          },{
            type: "text"
            name: "Weight",
            required: true,
            isMasked: false,
            entity:{
              id: "hlasodfanlj79234hkh",
              name: "Weight"
            }
          }
        ],
        ifDisplayConfirm: true   //提交form的时候是否需要进行confirm确认
      },
      ifDisplayHelpful: false  //是否需要helpful/nothelpful按钮，true：需要 false：不需要
    }
  ```

  custom response answer 

  ```javascript
    const customAnswer = {
      type: 'custom',
      transcript: '[Booking Room]',   //用于ChatServer保存聊天记录脚本，FORM表单只保存[表单名称]
      messageId: "jlkasdf7979asfhkah",
      content: {    //真实消息内容，用于标准化答案或自定义答案处理
        // 动态对象, 针对custom类型用户可以设置任意的属性和值, Bot可以在访客端前端处理这个对象来构建一个自己的界面
        intent: {
          id: 'jlasuo70978jhlasdf',
          type: "form",
          title: 'Order',
          loginRequired: false,
          form: {
            fields: [
              {
                type: 'text',
                name: 'email',
                required: true,
                value: 'allon@comm100.com',
              },
              {
                type: 'text',
                name: 'address',
                required: false,
                value: 'Hangzhou',
              },
              {
                type: 'checkbox',
                name: 'useSSL',
              }
            ]
          },
          openIn: "SideWindow", //打开方式 :NewWindow/Tab;CurrentBrowserWindow;SideWindow 
        },
      ifDisplayHelpful: true  //是否需要helpful/nothelpful按钮，true：需要 false：不需要
      }
    }
  ```

## Visitor Side Handle Bot Message

用户可以通过manifest中访客端的js配置,接入处理Bot消息的接口

```json
  {
    "location": {
      "chat": {
        "visitor": {
          "customJS": [
            "/assets/visitor_custom_js.js"
          ]
        }
      }
    }
  }
```

安装这个APP以后, 前端在加载访客端的js以后会加载上面的js

### JS API

在特定区域打开窗口
```javascript
  const window = {
    url: "https://****/***.html",
    openIn: "SideWindow", //打开方式 :NewWindow/Tab;CurrentBrowserWindow;SideWindow
  }

  const promise = Comm100API.do("livechat.chat.openWindow", window);
```

登录结果处理
```javascript
   promise.then(function(data){
     if(data.result === "OK"){
       //登录成功,将当前需要登录的问题以访客的身份重新请求一次答案
       Comm100API.do('livechat.chat.message.send', data.message);
     }
   }).catch(function(reason){
     //handle exception 
   });
```

自定义消息界面渲染

```javascript
  Comm100API.on('livechat.chat.message.received', (message) => {
    if (message.type === 'custom') { //自定义消息界面渲染
      const messages = Comm100API.get('livechat.chat.message');
      const newMessags = messages.update((msg) => {
        if (message.id === msg) 
          return Object.assign({}, msg, { render: renderCustom })
        else
          return msg;
      });
      Comm100.API.set('livechat.chat.message', messages);
    }
  });

  const renderCustom = (message) => {
    if (message.extend && message.extend.intent) {
      if (message.extend.intent.responseType === 'form') {
          const form = buildForm((message.extend);
          // return custom form
        }
      } 
    } 
  }
```

## Campaign Bot

Campaign中关于Bot中的配置目前不开放设置，Campaign对应bot的关系由Comm100维护, 列表由上面的List接口获取, 从列表中获取到的信息会列在Comm100本身bot的后面, 其他关于分配的逻辑由Comm100定死, 用户只能配置公开的两个选项。

## Micro Define

Manifest中可用的宏如下所示：

```javascript
    const site = {
      id: '10000',            // {siteId}
      name: 'comm100',        // {siteName}
    }

    const chat = {
      id: '@chat_id',
      campaignId: '@campaign_id',
      visitor: {
        id: '@visitor_id',
        name: 'Allon',
        email: 'allon.lu@comm100.com',
      },
      bot: {
        id: '@bot_id',
        language: 'en_us',
      }
    }

    const app = {
        app:{
          metadata:{ 
            token: '@token'   //{app.metadata.token}
          }
        }      
    }

    const agent = {
      agent:{
        metadata:{ 
          token: '@token',  // {agent.metadata.token}
          email: 'allon.lu@comm100.com',
        }
      }      
    }
```