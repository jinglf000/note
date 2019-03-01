#  浏览器事件

> Event接口表示在DOM中发生的任何事件; 一些是用户生成的（例如鼠标或键盘事件），而其他由API生成(例如指示动画已经完成运行的事件，视频已被暂停等等)。有许多类型的事件，其中一些使用基于主要事件接口的其他接口。事件本身包含所有事件通用的属性和方法。
> 更详细的介绍 https://developer.mozilla.org/zh-CN/docs/Learn/JavaScript/Building_blocks/Events
> 观察者模式和订阅-发布模式（Observe and Publish-Subscribe Pattern）
>
> -  在观察者模式中，观察者是知道Subject的，Subject一直保持对观察者进行记录。然而，在发布订阅模式中，发布者和订阅者不知道对方的存在。它们只有通过消息代理进行通信。

> - 在发布订阅模式中，组件是松散耦合的，正好和观察者模式相反。

> - 观察者模式大多数时候是同步的，比如当事件触发，Subject就会去调用观察者的方法。而发布-订阅模式大多数时候是异步的（使用消息队列）。

> - 观察者 模式需要在单个应用程序地址空间中实现，而发布-订阅更像交叉应用模式。

事件的注册监听机制，是观察者模式的一种实现；

## 1、标准事件方法

事件的绑定、解绑、手动派发。

`addEventListener('eventname', fn, Boolean(userCapture), options)`通过传入可配置的参数实现绑定事件的控制。

```js
var ele = document.querySelector('box');
ele.addEventListener('click', clickFnHandle);// 绑定
ele.removeEventListener('click', clickFnHandle);// 解除绑定

var event = new Event('click');// 初始化事件

ele.dispatchEvent(event);// 手动派发事件
```

## 2、事件流eventflow

![事件流](.\imgs\eventflow.svg)

事件的执行分为三个阶段：捕获阶段、处于目标阶段、冒泡阶段

## 3、事件委托、代理及 jquery事件委托的实现

```js
$(document).on('click', '.box', function(e) {});
```

* 事件委托本质上是对父元素绑定事件；并没有对子元素进行绑定事件。（如`document`)；
* js本身并不提供事件的委托，事件委托是一种优化事件处理的最佳实践。
* 事件委托的实现原因：元素的之间的层级关系和事件冒泡的存在。

* 推论：如果父元素上有对子元素的事件委托（使用jquery实现），子元素本身也绑定了事件，并且在事件处理中有阻止事件冒泡，那么：委托中的事件不会触发；

#### 3.1 `jQuery`中事件委托的实现：

* 1、父元素事件触发
* 2、判断`on` 中第二个参数是否是字符串，否直接触发事件；
* 3、是，根据事件对象中的`event.target`DOM元素，层层查找直到当前事件绑定的DOM元素；
* 4、循环时判断DOM元素是否是选择符所选择的元素。如果是添加到执行队列里面；
* 5、得到所有执行队列，分次执行；

循环的伪代码

```js
var target = document.querySelector('.inner');
do {
	console.log(`事件冒泡到：${target.nodeName}，文本内容为：${target.getAttribute('index')}`);
} while ( (target = target.parentNode) )
```




`event.target` 事件触发时的DOM元素
`event.currentTarget`事件绑定的DOM元素



## 4、IOS下事件委托到`document body`的问题
``` js
$(document).on('click', '.box', function () {
   //... 
});
```
#####  问题描述：
当使用委托给一个元素添加click事件时，如果事件是委托到 document或 body上，并且委托的元素是默认不可点击的（如 div, span等），此时 click事件会失效。
##### 解决办法：
- 1、将 click 事件直接绑定到目标元素（即 .target）上；
- 2、将目标元素换成 a 或者 button元素；
- 3、将 click 事件委托到非 document 或 body 的父级元素上；
- 4、给目标元素加一条样式规则 cursor: pointer。
## 5、浏览器的 eventLoop
https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/EventLoop


## 6、派发自定义事件

```js
document.addEventListener('customeEvent', fn, false);// 绑定事件处理
document.removeEventListener('customeEvent', fn);// 移除对应事件
var event = new CustomEvent('customeEvent', { detail: {}})// 创建自定义事件对象，并在event.detail属性上添加自定义数据，以供回调函数使用；
document.dispatchEvent(event);// 派发自定义事件，这时绑定的事件处理就会触发了
```
