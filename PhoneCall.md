# General
1. [Role](#role)
2. [Open Account](#setup-site)
3. [Integration Ways](#integration-ways)
4. [Account Integration](#account-integration)
5. [Function Integration](#function-integration)

## Role
  - Comm100 
  - Partner -合作伙伴-需要集成Comm100产品的客户，如某个PhoneCall公司。
    + 访客 
    + 客服
    + Admin

## Open Account
   由Comm100给Partner开户，创建一个特定Site，Partner可以更新自己的Site信息

## Integration Ways
  - 界面集成  
     通过直接指定Comm100的页面地址将Comm100的功能引入到Partner的界面中。
  - 组件集成    
     通过引入Comm100的组件代码将Comm100的功能集成Partner的页面中，这种方式需要Partner的终端支持Comm100的组件。
  - 接口集成   
    Partner通过调用Comm100的Api，自己构建界面或后台来完成特定逻辑。

## Account Integration
  - Account Manage -Partner可以直接通过接口创建、删除或修改Comm100的Agent或Department
     + New Agent -Partner可以在界面中选择自己系统中的某个/某些账户直接生成对应的Comm100 Agent
     + Delete Agent -Partner在删除自己的账户的同时删除相应的Comm100 Agent；或者只删除Comm100 Agent
     + New Department -Partner可以选择自己的系统中对应的Department生成对应的Comm100 Department,生成的同时可以选择性将该部门下面的人员自动生成Comm100 Agent并加入到当前部门中
     + Delete Department -Partner可以在删除自己的部门的同时删除相应的Comm100 Department；或者只删除Comm100 Department    
  - Authority Manage  
    Partner可以在界面中配置自己系统中的账户在Comm100中权限。
  - Account Login
     - Partner在登录自己的系统后，可以直接使用嵌入在自己系统中的Comm100的页面、组件或Api，不需要再进行登录
     - 完全通过链接嵌入Agent Console，当Partner的用户登录以后，可以直接点击链接进入Agent Console


## Function Integration
  - [Agent Console](#agent-console)
  - [Control Panel Settings](#control-panel-settings)
  - [Report](#report)

### Agent Console
  将聊天功能集成到Partner的界面中，或者直接使用Comm100的Agent Console与访客进行聊天，查看访客列表等。
+ List
     * visitors   
         Partner可以在自己的界面中嵌入访客列表的界面，其Agent可以查看访客列表，并对访客列表进行相应操作
     * mychats    
         Partner可以在自己的界面中嵌入聊天窗口，其Agent可以与访客进行聊天
+ tabs
     * info  
         Partner的Agent可以在聊天窗口页面查看当前聊天的信息
     * canned   
         Partner的Agent可以在聊天页面使用canned messages
     * wrap-up
+ 状态切换  
   Partner可以在界面中切换Comm100 Agent的状态或者切换自己系统中的状态的同时通过接口来改变Comm100 Agent的状态

+ Settings： Partner可以在界面中嵌入Comm100 Agent Console中的Settings页面

### Control Panel Settings
   - Site管理
     + Update Site Profile ：Partner可以通过界面修改Site信息，需要Comm100提供Site修改接口
   - Agents管理
   - 权限配置
     + Agent Permissions：Partner可以在界面中配置自己系统中的账户在Comm100中权限
     + IP Restrictions：Partner可以在界面中配置需要限制的IP地址
   - Campaign配置
     + Chat Button：Partner的admin可以在界面中配置某个Campaign的Chat Button
     + Chat Window：Partner的admin可以在界面中配置某个Campaign的Chat Window
     + Pre-Chat：Partner的admin可以在界面中配置某个Campaign的Pre-Chat
     + Post-Chat：Partner的admin可以在界面中配置某个Campaign的Post-Chat
     + Offline Message：Partner的admin可以在界面中配置某个Campaign的Offline Message
     + Invitation：Partner的admin可以在界面中配置某个Campaign的Invitation
     + Agent Wrap-up：Partner的admin可以在界面中配置某个Campaign的Wrap-up
     + Language：Partner的admin可以在界面中配置某个Campaign的Language
     + Routing Rules：Partner的admin可以在界面中配置某个Campaign的Routing Rules
     + ChatBot：Partner的admin可以在界面中配置ChatBot的配置信息
     + Multiple Campaigns：Partner的admin可以在界面中配置是否需要使用多个Campaign
   - Settings配置
     + Canned Messages：Partner的admin可以在界面中配置Canned Messages
     + Departments
     + Auto Allocation
     + Custom Away Status
     + Auto Translation
     + Ban List
     + Visitor Sementation
     + Visitor Single Sign-On  
     
### Reports
  用户可以通过ReportApi获取到报表数据，集成到自己的报表系统中。
