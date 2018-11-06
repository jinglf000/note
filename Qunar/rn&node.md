##携程金融RN 项目

### 1、项目文档

项目结构 RN <------rn和Node进行接口交互------> Node <——Node和java后台交互 ----->java

RN层负责：页面的数据渲染（状态层使用redux，渲染层使用RN，交互使用RN对应的事件）

Node层负责：页面的接口的聚合，合并多个接口为一个，输出到前台。BFF（在Qconfig中同样可以配置相应的参数，使用node来进行访问）；

JAVA层负责：真正的业务逻辑。

[Qconfig 配置中心](http://tc.corp.qunar.com/webapp/#/qconfig/ft_finprimary/dev:/testft_finprimary.json?groupName=ft_finprimary&status=PASSED&basedVersion=0&editVersion=2&canEdit=true) 用于配制

[pmo 项目管理](http://pmo.corp.qunar.com/browse/FINANCE-11374)

[wiki接口地址](http://wiki.corp.qunar.com/confluence/pages/viewpage.action?pageId=214799547)



技术栈：react、react-native、redux

[redux官方文档](https://redux.js.org/)

[React-native样式指南](https://github.com/doyoe/react-native-stylesheet-guide)

[react生命周期](https://www.jianshu.com/p/b49fe87d2153)

[ruanyf git 命令](http://www.ruanyifeng.com/blog/2015/12/git-cheat-sheet.html)

参考项目：金融借钱RN项目 [访问地址](http://gitlab.corp.qunar.com/fe/cash_loan_rn)

### 2、RN 项目结构
数据结构：
- assets 资源路径，包括图片的路径和字体的路径
- script 代码路径
  - commmon  通用方法
  - components 通用组件
  - config 配置文件
    - const 项目数据配置，其数据结构和modal要保持一致
    - errorCode 错误代码
    - urlConst url路径前缀分beta 、线上、测试
  - models 数据模型
    - 文件夹
      - action 似乎是异步请求的封装，其使用了service层的接口
      - reducer init 数据结构和对type的响应
      - selector redux 的modal使用了reselect封装了一层
      - type 派发的类型 ，类似于可用action的集合 

  - pages 页面结构
  	- components 页面所使用到的组件 
  - services 异步逻辑
  - index.js 入口文件
  
###3、redux React中的数据管理
遵循的原则：最小化、数据派生

reselector 在RN项目里面能够做数据的本地化缓存。

### 4、项目流程
1、项目3天以上 需要写wiki设计文档 （包含 接口字段 流程图等等）
2、写代码之前需要 （和我或者李阳吧）确定一下，可行度 ，要不白干了，（我之前做过这事，白干了）
3、开始之前，一定要给产品 要设计图，需求明确，要不不能进入排期
4、联调之前一定要 前后端都达到联调 条件（我吃过亏）
5、提测之前要diff 代码，提测的时候需要给QA showcase，需要使用beta 环境 不能是本地
6、上线之前也需要diff 代码

### 5、需要注意的问题
1、解构赋值，为以相同的结构去映射**对象**中的值

### 6、node 使用egg

1、调试：`npm run debug`开启调试模式，在chrome 开发者工具中选择node，并添加监听端口`localhost:9999`

2、node使用 egg 框架来开发，egg中文件即使模块。

3、结构：

router.js // 路由

controller // 控制器，路由对应的处理函数，以文件名来划分

extend // 扩展

middleware // koa的中间件

service // 访问数据库、接口的业务处理。其中访问第三方的服务也是会封装到这里`proxy.js`

### 7、diff 代码
- 删除不需要的样式注释、代码注释
- 组件文件中包含两部分：页面结构和样式，其他的内容（函数，变量等）放提出在专门的文件中（utils、const）
- 禁止使用魔术字符串，（魔术字符串指的是，在代码之中多次出现、与代码形成强耦合的某一个具体的字符串或者数值）；