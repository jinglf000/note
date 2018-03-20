vue-source code
===

## Flow
> Flow is a static type checker for javascript 

**static type annotation** 
> Flow checks your code for errors through **static type annotations**. These _types_ allow you to tell Flow how you want your code to work, and Flow will make sure it does work that way.

编译时会把对应的 静态类型声明给去除



## Node 

通过设置node进程中的 **process.env.NODE_ENV**变量来区分`production`mode`development`
而在真实打包后的代码中，开发环境中该变量 `process.env.NODE_ENV` 会被替换为`development`
生产环境中会被替换为 `production`；所以会看到如下代码
```js
/**
* Show production mode tip message on boot? source code
*/

productionTip:  process.env.NODE_ENV  !==  'production',

/**
* Show production mode tip message on boot? vue.js 文件
*/

productionTip:  "development"  !==  'production',

/**
* production mode 中 vue.min.js
*/
productionTip:!1
```
## vue 数据观测

>  https://gitissue.com/issues/5a04398158dc9b606dad6d80

