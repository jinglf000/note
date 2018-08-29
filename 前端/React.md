# React

## 1、JSX

* JSX comes with the full power of JavaScript. 拥有全部的js能力。
* You can put *any* JavaScript expressions within braces inside JSX. 你可以把任何JavaScript表达式放在JSX的大括号里面。甚至是函数声明。
* Each React element is a JavaScript object that you can store in a variable or pass around in your program. jsx中的x或者说是类似于div的标签这些语法，在js里面可以当做为一个React element的js对象。
* 大括号里面的this指向的是当前组件的实例。

## 2、react 的一些规定
* create-react-app生成的文件目录中：public 下的index.html(挂载文件是必须的)，src 下的index.js（入口也是必须的）；
* 构造组件类的时候，`props state setState super(props)`也是必须的；`props`表示传入的参数，`state`表示内部的状态；
* 推荐使用：on[event]表示事件，使用handle[event]表示事件处理函数；
* `Functional Components` and `Controled Components`
* 数据更新的方式，使用整体更新，而不是类似于Vue的单个更新。不要改变原始数据，原始数据用于保存成历史记录；
* `key ref`为react中的保留property，在列表中使用key来标记列表中的唯一元素。

