Vue study from 知乎live
###1、组件
| 框架 | jQuery |
| :---: | :---:|
| 组件作为抽象的基本单元 | 页面作为基本单元 |
|web应用|网页|
|聚合，以组件的方式|以语言的方式进行分类|
提高代码的可维护性

组件的分类
- 接入型 container
- 展示型
- 交互型 比如各类加强版的表单组件，通常强调复用
- 功能型 比如 `<router-view>`，`<transition>`，作为一种扩展、抽象机制存在。


###2、变化侦测渲染机制
|框架|jQuery|
|:---:|:---:|
|declarative声明式|Imperative 命令式|
|直接描述state和view的对应关系|手动用|
命令式最终很难进行维护
view = render(state)
输入是state（数据） 输出DOM（view）
模板：允许我们使用声明的方式定义state（数据状态）和view（DOM视图）之间的关系
渲染机制解决了 state 到 view的问题

###3、状态管理
状态管理则解决了 UI应用和state之间的关系
只有当数据比较复杂时才需要，简单的CRUD是不需要的