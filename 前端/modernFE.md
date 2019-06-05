# ModernFE

### 1、package.json

> 每个项目的根目录下面，一般都有一个`package.json`文件，定义了这个项目所需要的各种模块，以及项目的配置信息（比如名称、版本、许可证等元数据）。`npm install`命令根据这个配置文件，自动下载所需的模块，也就是配置项目所需的运行和开发环境。

特殊字段名称的含义：

`main` 指定入口文件；用于node端；如果node端存在webpack编译，优先使用module

`browser`指定浏览器环境中加载文件；用于webpack下的web端；

`module`指定ESM中加载的文件；辅助标识；

在webpack + web + commonJs(ESM)的情况下，(cjs 指使用 require module.exports。mjs 指 import xxx from 'xxx'; export xxx) 优先级都是：**browser = browser+mjs > module > browser+cjs > main**

在node + commonJs/ESM 环境下只有 **main**有；除非有webpack存在的情况下，module才有效；

无论使用的是import 或 require 都是优先获取browser 最后main；🥇🥇🥇

更详细的描述：[<https://github.com/Weiyu-Chen/blog/issues/8>](<https://github.com/Weiyu-Chen/blog/issues/8>)

### 2、用户体验指标

[<https://developers.google.com/web/fundamentals/performance/rail?hl=zh-cn>](https://developers.google.com/web/fundamentals/performance/rail?hl=zh-cn)

### 3、QA
* hook 为什么不能在react 文件下使用？一种原因应用内有多个React实例；webpack externals 会把不需要的第三方库抽取出来，避免打包到构建产物包里，举例其中使用方法为: `{‘xxxxx/react': ‘React’}`；其中xxxxx/react 必须是 import xxx from ‘xxxxx/react’ ，key值必须和from对应的一直；React为手动添加React引用时所提供个的全局变量，必须为在手动添加script标签时，其所提供的全局变量；
* react 和react dom有先后顺序吗？有，必须react在前；
* f2图表中 all min 区别。和import文件的区别？详见module文件 lib index.js index-simple.js  index-all.js 分别对应了三种版本
* f2  @antv/f2  f2/lib/index 区别？后者需要babel编译，而前者获取的是编译后的内容。无需再次编译。但是在扩展时（详见lib/index 加载其他模块的方式）需要lib中的index。如lib中的index加载其他模块一样，加载point；
* 我如何才能够看到pasred后的代码？在动态路由模式下，每个路由对应了一个js文件，在<header> 标签中找到对应的async 异步包，在source面板里面能够找到编译后的代码；由于sourceMap的存在，自带打断点的时候，会跳转到开发的文件中去；

 



