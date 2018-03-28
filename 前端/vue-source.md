vue-source code
===
## 0、源码分析

 _注重大体框架，从宏观到微观_
> http://hcysun.me/2017/03/03/Vue%E6%BA%90%E7%A0%81%E5%AD%A6%E4%B9%A0/


## 1、Flow
> Flow is a static type checker for javascript 

**static type annotation** 
> Flow checks your code for errors through **static type annotations**. These _types_ allow you to tell Flow how you want your code to work, and Flow will make sure it does work that way.

编译时会把对应的 静态类型声明给去除



## 2、Node 

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
## 3、vue 数据观测

>  https://gitissue.com/issues/5a04398158dc9b606dad6d80


## 4、策略模式（设计模式）

> 在函数作为一等对象的语言中，策略模式是隐形的。strategy就是值为函数的变量。

在JavaScript中，除了使用类来封装算法和行为之外，使用函数当然也是一种选择。这些“算法”可以被封装到函数中并且四处传递，也就是我们常说的“高阶函数”。

实际上在JavaScript这种将函数作为一等对象的语言里，策略模式已经融入到了语言本身当中，我们经常使用高阶函数来封装不同的行为，并且把它传递到另一个函数中。当我们对这些函数发出“调用”的消息时，不同的函数会返回不同的执行结果。所以在JavaScript中，“函数对象的多态性”会更加简单些。

把复杂的运算封装到函数中，并对函数进行四处传递，实现算法的调用。

**封装提取抽象**对于代码中复杂、重复的部分我们通过抽象，封装 用以实现代码的复用，实现代码清晰明了。
**混合mixin**在复杂的框架中，会有好多预设的属性和方法，这时就会用到了属性合并，mixin混合，


## 5、tips

5.1、`||` `&&` 简化代码执行

```js
obj || obj = {};
obj && obj.context = {};
```
5.2、`requestAnimationFrame(callback)` 跟随屏幕的刷新频率执行代码，类似于`setTimeout(callback)`

要想实现动画，req需要循环去调用；参数为事件戳；
```js
var start = null;
var element = document.getElementById('SomeElementYouWantToAnimate');
element.style.position = 'absolute';

function step(timestamp) {
  if (!start) start = timestamp;
  var progress = timestamp - start;
  element.style.left = Math.min(progress / 10, 200) + 'px';
  if (progress < 2000) {
    window.requestAnimationFrame(step);
  }
}

window.requestAnimationFrame(step);
```
5.3、DOM唯一性，
无论用那种方式获取同一个DOM元素，都是获取的同一个DOM，并且DOM和标签是一一对应的。
```js
$('#id')[0] === document.getElementById('id') === document.querySelector('#id');// 真实代码不是对的，
```

在vue中，一旦组件挂载到DOM上，即便通过`parentElement.removeChild(vm1.$el)`移除对应的DOM，vue的响应式更新仍然存在。（通过vonsole 打印会发现值仍然在更新）只不过该DOM元素，没有在HTML页面上体现；反之这时使用`parentElement.removeChild(vm1.$el)`就能恢复DOM的显示状态。

5.4、移除当前DOM元素
```js
ele.parentElement.removeChild(ele);// 前提是parentElement这个属性在浏览器里是实现的

```

