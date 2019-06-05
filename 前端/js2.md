# Javascript 2

[TOC]

<hr/>

### 1、一个精简的问题

```js
// 返回的数据结构为
{
    "errorCode": "200",
    "errorMsg": null,
    "data": {
        "activedProdList": [],
        "applyingProdList": [],
        "recommendProdList": [
            {
                "tppCode": "WDPHMART",
                "tppName": "万达普惠",
                "creditAmount": 50000,
                "interestRate": "0.06%~0.10%",
                "isWaitDraw": null,
                "isOverDate": null,
                "openStatusEnum": "UN_OPEN",
                "url": null
            },
            {
                "tppCode": "MSMART",
                "tppName": "马上消金",
                "creditAmount": 50000,
                "interestRate": "0.05%~0.10%",
                "isWaitDraw": null,
                "isOverDate": null,
                "openStatusEnum": "UN_OPEN",
                "url": null
            }
        ]
    }
}
```



```js

/**
     * 是否需要显示market
     * 只有当有借贷项目时才显示
     * @param {Boolean} flag 是否需要显示market
     * @param {Object} obj market接口返回的数据
     */
    isShowMarket(flag, obj) {
        if (!flag) return false;
        const values = Object.values(obj);
        const reducer = (accumulator, item) =>
            (accumulator + Array.isArray(item) ? item.length : 0);

        const num = Object.values(obj).reduce(reducer, 0);
        console.log(values, num);
        // return num > 0;
        return num > 0;
    }
```

要求：data里面数组长度大于0的时候返回true

出现的问题：运算符的优先级、隐式类型转换、箭头函数精简代码产生的问题

### 2、antd Radio 组件的defaultValue 如何使用？ 他和 本身的value熟悉相比有什么差别？
* value 和 defaultValue 不要同时使用，同时使用时有优先级之分，value > defaultValue ？
* defaultValue 配合 onChange事件一起使用时，在change时获取新的值，问题是 若不发生change 无法获取到最初的defaultValue；
* 使用 value 和 onchange ，可以在初始化时，设定一个初始的value来实现 degaultValue的效果。而且似乎defaultValue只有在第一次初始化的时候才会设置，以后都不会设置，相比较而言，应用场景比较小。

### 3、React setState、箭头函数、dva 中的subscribtion的问题

* 箭头函数是 Class 的新语法

  ```js
  class Person {
      state = {
          isHide: false
      }
      sayName = () => {
          console.log('sayName');
      }
  }
// 上下两张方式是等价的  
  class Person {
      constructor() {
          this.state = {
              isHide: false
          };
          this.sayName = () => {
              console.log('sayName');
          }
      }
  }
  ```

### 4、常用的字段

`append delete entries forEach get set has keys set value next done`


使用命令时尽量使用这个和原声JS定义相同的，这样意义明显。

### 5、前端路由

* 要求 link 切换链接 路由变化，浏览器前进后退 路由变化，页面不会reload，初次输入地址 显示对应的路由

#### 5.1 hash路由

 使用 link `<a href="#index"> a </a>` 或者 `location.hash`控制路由变化

通过`window.onhashchange` 监听 hash 变化，以上的两种方式都可以触发事件，根据对应的hash显示对应的View；

监听 `window.onload`事件 执行初始化的操作 获取hash 显示对应的 view

#### 5.2 History路由

通过 history.pushState 或者 history.replaceState 修改页面路由，修改时页面不会reload 

通过`history.pushState`  `history.replaceState` 手动改变路由的hash，手动改变时不会触发`popchange`事件；需要手动触发 View

当使用浏览器的前进后退按钮时，会触发popchange ，监听该事件实现对应的View；

初次进入页面，则需要后端路由做对应的操作，并且需要绑定 window.onload 触发首次响应；

#### 5.3 路由响应策略
```js
// hash 路由模式下，当从#/a ==> #/b的时候，对应于 a的组件销毁 b的组件重建
// #/a ==> #/a?name=123 由于路由并没有发生跳转，而是本路由之间的切换，因此组件不会销毁重建，而是相当于是props更新一样会重新render；
```

### 6、原则 principle 
* history API 里面提供了一系列能够

### 7、ES6
* `import X from 'path'` path必须为静态路径，不能是经过计算的值；也不能是变量

* 函数进行结构赋值时，不能为undefined

* ```js
  function xx ({name}) {
      
  }
  xx(); //TypeError: Cannot destructure property `name` of 'undefined' or 'null'.
  ```


### 8、offsetHeight、clientHeight、scrollHeight
- **clientHeight**  VISIBLE content & padding 
  * Only visible height: content portion limited by explicitly defined height of the element.
- **offsetHeight** VISIBLE content & padding + border + scrollbar 
  - Height occupied by the element on document.
- **scrollHeight** ENTIRE  content & padding (visible or not)
  - Height of all content + paddings, despite of height of the element.

![scrollHeight](https://i.stack.imgur.com/NANud.png)

![clientHeight and offsetHeight](https://i.stack.imgur.com/RFxSh.png)

### 9、页面组合使用`position:sticky` 和 `height:100vh`时所产生的问题：

* 单页应用下，使用了粘性定位，同时使用了iscroll或者better-scroll （使用transform）这种变换方式；导致页面在滚动到底部的时候（此时粘性定位变为相对定位）会把整体容器（100vh）推到上方，而在重新渲染transform滚动组件之后，导致页面切滑动不下来；（滑动不下来，由于采用了transform使得只有本身内部容器滚动，整体无法滚动）解决办法：在路由切换成功后手动scrollTo(0,0);

* Element [scrollTop](<https://developer.mozilla.org/zh-CN/docs/Web/API/Element/scrollTop>) 表示element的内容向上滚动的像素数；而不是滚动元素向上滚动的像素数，left保持一致；这和jQuery.scrollTop提供的方式是有差别的；

* IOS 上`position:fixed` 不会出现弹性抖动的情况；下拉出现橡皮条弹性的时候，fixed定位的元素也会定位到固定的位置；

* 如果是相对于body滚动则调用window.scrollTo(0,0);可以回到body顶部；或者使用document.documentElement（html元素）

* ```html
  <body>
  <div class="box">
  	<div class="inner"></div>
  </div>
  </body>
  // .box { height: 100%, width: 100% }
  // 当inner高度大于box的时候，而box没有设置overflow：scroll时，可以通过监听div.box上一级元素，获取scrollTop 或者设置元素的滚动位置；
  ```

### 9、react-router路由跳转访问指南

* 1、单页应用下，路由跳转使用 `Link` 或者 history实例来进行跳转，保证跳转风格的一直；
* 2、除非需要重新打开页面否则不要使用`window.location`浏览器原声的跳转；
* 3、route子组件中可以直接使用history实例，进行跳转而不需要层层组件传递；
* 4、对于location，可以使用浏览器location query参数自己处理，或者使用`history.crateLocation(window.location)`的返回值；（包装后的location）
* 5、手动解析query，拼装query注意点：query参数是：?key=value&key=value这种形式，因此无论是解析还是拼装，只对value进行encodeURIComponent 或 decodeUIRComponent操作；对路径全解析会造成url中再次拼接的url地址参数丢失；


### 10、Math min max 方法
* 传入 ` '' null`时会转换为0，传入 `undefined`时返回NaN
* 数组`Array.of()` 返回参数所构成的数组
* `Array.filter()`实现数组过滤，返回满足条件的新数组

### 11、DOM API
* 用户解析 html 字符串，并获取内部的text；DOM的方法了解一下；
```js
let textContent = props.content;
  if (textContent) {
    const parse = new DOMParser();
    const el = parse.parseFromString(textContent, 'text/html');
    textContent = el.documentElement.textContent || '';
  }
```

### 12、meta referrer
`<meta name="referrer" content="no-referrer">`

当设置为no-referrer时，页面中的任何访问都不会携带`Referrer`参数；可以防止某些图片网站对referrer的限制；

### 13、不要在全局常量中使用get set

对于全局变量或配置变量来说，应该就是const 不变的，而在**不变的变量**中使用，get 或 set会造成每次获取或者读写时返回值不符合期望；不符合编码原则；

```
const COLOR = '#ffc';
const CODE = {
  NA: '#12f'
}; // 应该是这样

Object.defineProperty(CODE, 'NA', {
  get() {},// 而不应该这样，这样每次返回值时不固定的；
  set() {}//
})
```



#### 