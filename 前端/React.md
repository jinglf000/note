# React

[TOC]
<hr/>

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

##  3、Think in React
- React 当state 或者props变化时，会更新render，函数，更新完render之后生成Virtual DOM 通过diff 算法实现是否更新到DOM。（相比于Vue的细颗粒度的控制，React更新时，是state和props全量更新，因此能够拿到prevProps，所以还需要手动来处理是否应该去更新，所以会有`shouldComponentUpdate` 钩子判断是否更新，[生命周期 ](https://www.jianshu.com/p/325ef042d587)）

- 一种优化思路就是，避免不必要的render，（render之后会有，Virtual DOM 会进行diff比较，是否更新）如果我们确实不需要更新，就可以在`shouldComponentUpdate` 不进行更新。

- Redux 进行数据管理，状态保存设置的原则，最小化、数据派生，使用最小化的数据状态，其余数据状态可以使用selector派生出来。类似于getter

  reselector 在RN项目里面能够做数据的本地化缓存。

  RN项目里面使用的东西：内容主要在redux中，state使用了`fromJs`把普通的js对象转换为不可变对象，因此获取的时候需要使用`toJS`，同时在获取值渲染的时候使用了`reselect`使得计算后的数据能够缓存。

- React lifecycle 官方 [生命周期](http://projects.wojtekmaj.pl/react-lifecycle-methods-diagram/)

- React ，在class 类型组价时，使用箭头函数 this处理

- ref attribute 执行函数，参数为DOM 或者ReactDOM 实例，对应ReactDOM 可以通过instance.props 获取实例的props 无轮实例是否使用这个props；

- props 变化更新Reander 如何实现的？？


> React supports a special attribute that you can attach to any component. The ref attribute can be an object created by React.createRef() function or a callback function, or a string (in legacy API). When the ref attribute is a callback function, the function receives the underlying DOM element or class instance (depending on the type of element) as its argument. This allows you to have direct access to the DOM element or component instance.

> Use refs sparingly. If you find yourself often using refs to “make things happen” in your app, consider getting more familiar with top-down data flow.

* 

* A -> B -> C 三层组件调用关系中，（A是B的父组件，B是C的父组件）其中Render函数的触发顺序为：A -> B ->C，正是由于父组件render的调用，才会触发子组件的render；componentDidMounted钩子触发顺序 C -> B ->A，在A组件完成之后，能够获取到整个组件的DOM结构；

  > 数据更新后如果需要网络请求，可放在此处对 prevProps、prevState 和 当前 porps、state 对比。通常我们拿到数据后可能想直接用最新的数据取请求，不用等数据渲染完，实际这样的处理方式往往代码写起来很费劲，因为 state 并不能同步更新，react 遵守的是 view = fn(state)，即 state 和 view 是一对一的映射关系，在一个渲染周期内，保持 state 和 view 的同步，而如果想拿到最新的 state，则可在下个渲染周期内根据最新的  state 做操作，这样处理起来思维更简单，更不易出错，另外就像在 componentDidMount 里说的，更早的请求并不能带来明显的用户体验。

* constructor --> DOM Diff ---> componentDidMount s 初始化渲染周期，setState props ---> shouldComponentUpdate ---> DOM Diff ---> componentDidUpdate 数据更新渲染周期；只有在渲染周期结束之后，setState和prevProps才会真正的更新到state和props上；

* 保持state数据结构的扁平化，避免过多的层级

## 4、 REACT 约定（方便开发）

* 使用同名参数，模块于模块之间传参 使用 **约定优于配置**的策略；便于理解；

* 修改state的方式：（setState 的调用方式）
  * 初始化操作使用 init
  * 事件响应 handle
  * 相同名称的参数 a _a

* 由于setState 是个异步操作，因此在需要及时传值得场合，不要使用state的值，因为它的值不一定准确。应使用及时的值进行处理，处理完之后再setState;（这种值，需要最后setState，也需要及时的值）

* 需要渲染的数据和不需要渲染的数据，需要渲染的可以放到state，或者props通过父组件传递，不需要渲染的直接挂载到this上即可；

* 5、saltUI  ifinateScroll 无限滚动组件必须要添加`overflow:auto`，属性，否则onScroll事件不会触发；或者在自己写scroll 滚动组件时，也要适时的添加overflow属性否则不会触发onScroll事件;

* 6、**dva**框架，是 React react-ruoter redux redux-saga 的一层轻量封装；精简了操作，做出了一些了的约定，而成为了一个框架；（这也就是约定优于配置，框架）；其中`state effects reducers subscriptions`   。subscriptions 的存在提供了一种全局的订阅方式，用于处理state之外的数据变化。齐结构是：

```
  subscriptions:{
      abc() {
          return fn;
      }
  }// subscriptions 里面的函数会运行，每个函数都会返回一个函数用于取消数据绑定
```

* Components 组件应该是包含内部状态且无业务逻辑的，通过派发外部事件响应结果

* refast 、dva 数据管理，如何来处理全局的数据管理？？ `dispatch={this.dispatch}`这种形式？



## 5、最佳实践

* 保持组件内render的单一明了，props --> render OR state ---> render；发生冲突时尽量聚合到一块去单一的render；
* state 内部状态，内部处理；props 外部传递值，渲染处理；现在的问题是 组件内部需要修改props？？如果数据都是props来的，修改也是修改props，这样流程就清楚了；这就是redux，dva搞得数据流；面对复杂的情况；要么单独state处理，要么使用redux管理，要么state只做内部数据，涉及到接口的时候；props对应接口，state只管渲染内容；总之让数据流变成明确的单向，而且用于数据管理；保证view = fn（props）在渲染周期内也是唯一的；
* Saltui 中iscroll 内部嵌套button时，若button绑定了点击事件，则可能会触发多次；
* 文件夹里多个组件使用 index.js 导出，使用文件夹区分不同组件，且文件夹中的主文件名和文件夹一致
* Form 表单和输入元素，有两种处理策略；表单的通常需求有：输入、回显、校验；
  * 以antd提供的组件来看，校验由`Form`组件提供，并配合高阶组件`getFieldDecorator`提供校验功能；简单一点 非控制组件无法存值；控制组件可以保存值；控制组件把组件的控制权上报给父组件管理，无论是否使用，父组件必须适配好组件需要的所有方法；非受控组件，一次性赋值使用。只关心第一次输入的值，和交互的输出值；
  * unControlled   非控制组件，通常适合于低频多级菜单的选择；通过传入defaultValue（react本身会对input元素上的defaultVlaue进行处理，设置为默认值）设置初始值，通过事件监听获取真实值；（初始值得获取，只能设置组件初次加载时，设置在组件加载完成之后，即便发生变化也不会更新）（多次使用时，而不销毁组件时，组件会保留上一次的值，并且此时defaultValue设置无效）；defaultValue 只有在表单元素重新挂载的时候才会设置，也意味着多次render时，deafultValue可能是不会生效的；
  * Controlled 控制组件，通过设置value属性设置元素的值，通过事件监听获取真实值；问题是必须在事件监听是更新该值，否则组件无法正常显示当前输入的值。好处value值发生变化，显示就会立即变化。（获取值后即可通过，重复设置value值来清空选择。缺点是和defaultValue不肯同时使用，适合于需要回显的输入场景）
* react-router中使用browserHistory，但是项目部署时有一个统一的路径前缀？原来的路由为hash路由，如`www.abc.com/project#/pageA`  要改成 `www.abc.com/project/pageA` 并且由于项目的问题project路径参数为项目固定参数，项目没有独立的域名；项目中有很多`history.push('/xxx')`路径写法；
  * 解决办法：reactRouter实现中依赖了history，在使用histroy时，实例化了一个对象，并在对象上绑定事件（hisroty.before）以监听url变化，路由更新组件发生变化；在使用history实例时，通常情况下使用的是reactRouter本身的默认history对象，对于上面这种情况，就可以自己初始化一个自定义的history对象，以供reactRouter使用；
* `<div data-id="123"></div>` 可以使用 `DOM.dataset.id` 获取到；并且还可以通过dataset进行赋值操作；注意一点无论赋值时是什么类型的值，取值操作时，取到的值都是字符串类型的值；可以认为在赋值时做了一下toString的操作；
* `componentDidUpdate(prevProps, prevState,snapshot )` 可以在didUpdate里处理更新操作，但是要注意在其中的`setState`操作一定要有条件判断，否则会出现死循环。

## 6、Redux
#### 6.1 概念
**设计思想**
- Web 应用是一个状态机，视图与状态是一一对应的。

- 所有的状态，保存在一个对象里面。
  解释：只有涉及到状态机的应用，才需要使用Redux，对于偏重展示的应用(如企业官网)不需要使用Redux；视图和状态的一一对应保证了单一的对应关系，View = fn(props/state)使得代码结构更加清晰；
  **解决问题**

- 代码结构；react中state和porops都能够渲染视图，当props能够改变state的时候？异步获取数据的时候？大型应用多人合作开发的时候？

- 组件通信；父子通信使用props或者事件，但是组件之间的进行通信如何解决？

> 从使用场景来说：需要使用Redux
>
> - 用户的使用方式复杂
> - 不同身份的用户有不同的使用方式（比如普通用户和管理员）
> - 多个用户之间可以协作
> - 与服务器大量交互，或者使用了WebSocket
> - View要从多个来源获取数据
>
> 从组件角度来说：需要使用Redux
>
> - 某个组件的状态，需要共享
> - 某个状态需要在任何地方都可以拿到
> - 一个组件需要改变全局状态
> - 一个组件需要改变另一个组件的状态

  参考自[Redux 教程](<http://www.ruanyifeng.com/blog/2016/09/redux_tutorial_part_one_basic_usages.html>)

Reducer 是纯函数，Reducer 函数里面不能改变 State，必须返回一个全新的对象；

> 最好把 State 对象设成只读。你没法改变它，要得到新的 State，唯一办法就是生成一个新对象。这样的好处是，任何时候，与某个 View 对应的 State 总是一个不变的对象。

![img](http://www.ruanyifeng.com/blogimg/asset/2016/bg2016091802.jpg)

#### 6.2、code 

```
store;// Redux 唯一实例，挂载了state、dispatch 调用了reduers
state;// 定义数据modal，通过connect 挂载到组件上；实现modal -> view
Action;// 定义好的活动，响应用户操作；用户点击(或者其他)响应对应的action，消息载体；
dispatch;// 派发方法 dispatch(Action)；调用了reducers 返回新的state 触发view更新；
reducers;// 纯函数 输入prevState 输出 新的state；(state是不可变的）
```

函数中返回函数最大的作用在于，由于闭包的存在所以返回的函数能够使用原函数的输入参数；高阶函数，高阶组件（运用函数返回一个组件）；

#### 6.3 dva 开发框架
* modal里声明的state、reducers、effects、subscriptions会放置在全局的 state里面；即便切换了路由，渲染了对应的不同的页面组件，只要页面未重新加载其他路由中的数据依然存在；
* 通过受控组件（controlled）的方式，在state组件中设置默认值；而不是通过设置default字段；减少需要判断的字段；
* 查询条件数值发生变化时直接更新到state，消费获取字段时，直接通过`select(s => s[namespace])`获取，而不是payload，传来传去；保证完整的数据周期，一个周期内只做一件事情；
* effect 中的call是一个promise的执行器，使用`yiled call()` `call` 第一个参数是能够返回promise的函数，第二个参数 给定一个函数传递参数；
* 尽可能的使用`select` 来获取对应的值，而不是通过payload 来传递值，最大程度上保证函数是高内聚的；减少传递参数造成的负担；参数过多会造成调用的不便；
* 尽可能的减少dispatch 调用的层级，能直接调用就直接调用；异步方法参数的拼装：如果涉及到多次的数据处理，那就放到modal文件里，否则直接放到router文件里；不要方法子组件的问题；
* Dva Modal 和 router 整体上来看就是一个 controlled 组件（受控组件）；所以需要使用受控组件的模式去控制整个组件。首先：通过设置state 确认默认值（而且这是唯一的方式），其次：响应更新事件时，必须要先应该更新state，然后在使用更新后的值去异步获取数据；
* 在effect 中调用effect`put({type:'name'})` 会造成死循环
* Dva 中的state为全局state，所以当页面切换回来的话，state仍然保留原来的状态，有些时候你可能需要 reset effect 来处理需要重置的情况；因此state中的默认值只会在第一次进入modal时有效，当再次进入该路由的时候，数据是上次拉取的数据；
* state尽可能使用基本数据类型；由于`connect`时候会对返回的数据进行浅比较，如果使用复杂的数据类型，而只改变了其中的属性的话，没有改变对象的引用，会造成组件无法渲染。
* **一个问题：DVA如何来实现不同的namespace，如果state发生变化的话，当其他modal存在的情况下会渲染吗？？？**


## 7、React 和 Vue的区别 View = f(data)（对data处理的区别）

React 和 Vue；Vue中约定使用data保存组件状态，并实现从数据（data）到视图（view）之前的响应式的映射`view = f(data)`；但从data 到 view 是一个异步关系，而data的更新是同步直接更新；React 中使用state保存组件状态，同样也实现了data到view之间个响应式更新；虽然data --> view和Vue一 是异步更新，但data 本身的更新（使用setState）则是异步的；所以在一下场景中需要不同的写法；

```html
<Select onSelect={(v) => { this.data / this.state}} value={value}></Select>
```

假定Vue和React都有对应的组件，在Vue组件中 onSelect 函数中的，this.data 能够拿到select 组件的新值；

但是在React组件中，onSelect 通过函数传值能够拿到最新的值，但是this.state 值得变化则要在 setState异步之后才会更新；所以可以理解为对于React来说，只会维护视图层。获取值得时候需要特别注意。



```js
this.data.name // 'tianming';
this.data.name = 'Tayor Swift';// update 
this.data.name // 'Tayor Swift' 并且该值就是view render的值；Vue
/**** React ***/
this.state.name // hello
this.setState({ name: 'wang yy'});// 
this.state.name // 仍然是hello
```

Vue：使用的依赖收集，因此data的更新时，同步的；但是data —> view 是异步的；会深入到data的每个属性上，他的思路是深入每个属性，对每个属性进行控制，进而实现view更新；（因此关于data上的变化有很多的监听方式）

React：使用另外一种思路；全量更新方式。每次更新都会提供一个全新的state对象，因此在更新的时候也需要提供一个全量的state，以供更新。所谓全量意味着：对于基础数值则要求数值更改；对于对象要求对象变化；

在dva架构中，使用扁平的数据结构，更新时全职替换更新；

* reducer 中返回state的时候，也要返回一个新的值；
* 为了避免对象造成的混淆，尽量在state中使用扁平的数据结构；一旦使用对象，注意在更新时对数据进行copy

```
dispatch({ type: 'setState', payload: { name :5}});
dispatch({ type: 'setState', payload: { name :5}});// react-redux中多次state为同一值时，view不会更新；同时
dispatch({ type: 'setState', payload: { name :obj}});
dispatch({ type: 'setState', payload: { name :obj}});// 当更新的obj为相同的obj时，也是不会更新的；
```



## 8、antd
 记录一些antd在使用过程中的问题；

 #### 8.1 form 校验

validator校验方法，是并发执行的；在执行下一次的校验规则之前；前一个校验规则是未知的；但是最后的结果，返回的错误数组和校验规则是一一对应的；

```js
getFieldDecorator('name', {
    rules: [
        {
            required: true, type: 'string'
        },
        {
            validator() {
                //xxx
            }
        }
    ]
})
```
#### 8.2 antd-design 设计原则
ANT DESIGN这个体系里面一般都是8的倍数做间距，然后灰色标示未加载出来，或者无数据等状态

## 9、react 组件，
对于任意一个可以进行输入交互的组件，必须要设计成同时支持 受控组件和非受控组件的形式；也就是说必须支持`value - onChange` `defaultValue onChange`的形式；

## 10、组合模式和继承模式(composite and inherit)
对具体问题作出合理的抽象，然后用对应的逻辑模型来实现；比如在页面逻辑的实现过程中，组合模式适合页面结构，通过把页面抽离出各种各样的区块，通过对区块的组合实现整体的页面；组件思想；而对于路由而言，则是一种层级性的结构因此对于路由而言，react-route在遵循了react的基础之上，使用层级组合的方式来实现，路由的层级关系；

## 11、路由
路由从顶级注入到组件中来，当路由发生变化，会更改组件的props，而组件会重新render；但是由于路由匹配规则的存在，所以对于的组件只会match到能匹配到的路由；location对应的pathname 不是全局的路由状态；只是匹配对应的状态；
`subscription`中能够监听路由，但同时是有弊端的;

* History.listen 会挂载到全局，路由发生变化即执行，同时路由发生变化时，render也会执行；两者次序不固定，无法确定明确的顺序；
*  对路由的监听，是一种原始的监听，不会按照既定的路由匹配顺序触发；

当props state和路由信息同时作用在组件上时，合理的数据流通方式

*数据流 action -> history -> state -> view*；让history 控制后续的动作，即便含有params参数；

## 12、PureComponent memo
* 使用时一定要注意，浅比较的情况下，如果相同，会阻止渲染；这可能会引发bug；
* shouldComponentUpdate 中对props和state进行浅比较；如果相同则不执行render；(浅比较指的是：对于基本数据类型而言，判断是否相等；引用类型判断引用的是否是同一个)；
* 适用于变化量比较小的展示性组件；
* 当props和state变化比较大时，`Component` 的性能优于`PureComponent`；
* memo 适用于函数式组件；

## 13、ReactDOM
* use `ReactDom.unmountComponentAtNode(DOM)` and `ReactDom.render()` 实现编程式DOM，实现某些toast 或者 message功能；

## 14、React 中如何触发组件的unMount
* 使用判断，在父组件中判断如何使用子组件，会触发子组件的unMount；
* 循环中，key发生变化，会造成对应的item unMount；是否进行组件销毁，在web中由react-dom来决定；