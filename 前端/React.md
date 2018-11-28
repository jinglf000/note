# React

## 1、JSX

* JSX comes with the full power of JavaScript. 拥有全部的js能力。
* You can put *any* JavaScript expressions within braces inside JSX. 你可以把任何JavaScript表达式放在JSX的大括号里面。甚至是函数声明。
* Each React element is a JavaScript object that you can store in a variable or pass around in your program. jsx中的x或者说是类似于div的标签这些语法，在js里面可以当做为一个React element的js对象。因此JSX元素可以被自由地赋值给变量；在jsx的大括号里面甚至可以使用函数，而且函数也可以返回对应jsx
* JSX语法的最外层，只能有一个节点。
* 大括号里面的this指向的是当前组件的实例，实例即是上下文context。
* JSX中的给元素添加class要使用className，给元素添加for要使用htmlFor；
* JSX里面，自定义的组件必须是大写字母开头（自定的组件为通用类，需要大写），不仅仅是在声明时，在使用时也是，普通的html标签都是用小写字母开头。
* 默认的on*事件只能用在普通的HTML标签上，而不能用在组件标签上；
* 了解一下ES6的proxy

## 2、react 的一些规定
* create-react-app生成的文件目录中：public 下的index.html(挂载文件是必须的)，src 下的index.js（入口也是必须的）；
* 构造组件类的时候，`props state setState super(props)`也是必须的；`props`表示传入的参数，`state`表示内部的状态；
* 推荐使用：on[event]表示事件，使用handle[event]表示事件处理函数；
* `Functional Components` and `Controled Components`
* 数据更新的方式，使用整体更新，而不是类似于Vue的单个更新。不要改变原始数据，原始数据用于保存成历史记录；
* `key ref`为react中的保留property，在列表中使用key来标记列表中的唯一元素。
* 必须使用`setState`方法去更改组件的state，这样修改state之后react会自动的以最优化的方式更新视图

##  Think in React
- React 当state 或者props变化时，会更新render，函数，更新完render之后生成Virtual DOM 通过diff 算法实现是否更新到DOM。（相比于Vue的细颗粒度的控制，React更新时，是state和props全量更新，因此能够拿到prevProps，所以还需要手动来处理是否应该去更新，所以会有`shouldComponentUpdate` 钩子判断是否更新，[生命周期 ](https://www.jianshu.com/p/325ef042d587)）

- 一种优化思路就是，避免不必要的render，（render之后会有，Virtual DOM 会进行diff比较，是否更新）如果我们确实不需要更新，就可以在`shouldComponentUpdate` 不进行更新。

- Redux 进行数据管理，状态保存设置的原则，最小化、数据派生，使用最小化的数据状态，其余数据状态可以使用selector派生出来。类似于getter

  reselector 在RN项目里面能够做数据的本地化缓存。

  RN项目里面使用的东西：内容主要在redux中，state使用了`fromJs`把普通的js对象转换为不可变对象，因此获取的时候需要使用`toJS`，同时在获取值渲染的时候使用了`reselect`使得计算后的数据能够缓存。

- React lifecycle 官方 [生命周期](http://projects.wojtekmaj.pl/react-lifecycle-methods-diagram/)

- React ，在class 类型组价时，使用箭头函数 this处理，

## RN
- 