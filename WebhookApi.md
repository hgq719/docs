# General

## Webhook编号
  为了让Webhook的使用者能识别到当前执行的事件来源于Comm100的哪个Webhook，Comm100为每个Webhook添加了自己的编号。
  - Chat Webhook API（No：101~199）
    + 101：[Chat.Request.start](#chat-request-start)
    + 102：[Chat.beforeAssigning](#chat-beforeassigning)
    + 103：[Chat.afterAssigning](#chat-afterassigning)
    + 104：[Chat.started](#chat-started)
    + 105：[Chat.Message.received](#chat-message-received)
    + 106：[Chat.Message.sent](#chat-message-sent)
    + 107：[Chat.Agent.joinChat](#chat-agent-joinchat)
    + 108：[Chat.Visitor.banned](#chat-visitor-banned)
    + 109：[Chat.ended](#chat-ended)
    + 110：[Chat.wrapup](#chat-wrapup)
  - OfflineMessage Webhook API (No:201~299)
    + 201：[OfflineMessage.submitted](#offlinemessage-submitted)
  - APP Webhook API (No:301~399)
    + 301：[App.installed](#app-installed)

## Webhook容错
  - 超时重试  
    Webhook的超时时间默认为10s，如果10s内没有返回结果则超时；超时后默认重试三次，每次间隔60s；若重试继续超时，则1个小时后继续重试三次；若再超时，24小时后继续重试三次；2天后重试失败则丢弃。

## Chat.request.start
  当聊天请求开始的时候触发。

## Chat.beforeAssigning
  当聊天分配到Agent之前触发

## Chat.afterAssigning
  当聊天分配到Agent之后触发

## Chat.started
  当聊天开始的时候触发。Webhook中可用的对象如下：
  - [Visitor object](#visitor-object)

## Chat.Message.received
  当Agent收到一条消息以后触发

## Chat.Message.sent
  当Agent发出一条消息以后触发

## Chat.Agent.joinChat
  当Agent加入到某个聊天的时候触发

## Chat.Visitor.banned
  当访客被ban的时候触发

## Chat.ended
  当聊天结束的时候触发

## Chat.wrapup
  当聊天wrap up的时候触发

## OfflineMessage.submitted
  当离线消息提交的时候触发

## App.installed 
  当App安装完成以后触发

## Visitor Object
```json
"visitor":{
    "browser":"Google Chrome 29.0.1547.76",
    "chats":2,
    "city":"Vancouver",
    "company":"Comm100",
    "country":"Canada",
    "current_browsing":"https://www.comm100.com/",
    "custom_fields":[
        {
        "field_id":5000001,
        "name":"order_id",
        "value":"1780064"
        },
        {
        "field_id":5000002,
        "name":"bill_amount",
        "value":"500.00"
        }
    ],
    "custom_variable":[
        {
        "name":"user_login",
        "value":"facebook"
        },
        {
        "name":"have_sales",
        "value":"yes"
        }
    ],
    "department":"livechat",
    "email":"allon@comm100.com",
    "first_visit_time":"/Date(13584868423)/",
    "flash_version":"11.8.800.170",
    "id":1024768,
    "ip":"192.168.8.1",
    "keywords":"comm100",
    "landing_page":"https://www.comm100.com/livechat/",
    "language":"en_us",
    "name":"allon",
    "operating_system":"Windows 7",
    "page_views":3,
    "phone":"12983782710",
    "product_service":"livechat",
    "referrer_url":"http://www.google.com/q=comm100",
    "screen_resolution":"1440*900",
    "search_engine":"Google",
    "state":"British Columbia",
    "status":1,
    "time_zone":"UTC-08:00",
    "visit_time":"/Date(13584868542)/",
    "visits":5
}
```