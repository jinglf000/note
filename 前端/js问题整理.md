## JS问题整理，承接 js.md

### 1、touch事件补充
* 移动端或`chrome`移动调试时，点击会触发`touch`事件
* `touch`事件分为：`touchStart` `touchMove` `touchEnd`
* 点击时会首先触发`touchStart`事件，滑动时会不断的触发`touchMove`事件（不滑动事件不会触发），长按时也不会触发；点击离开时会触发`touchEnd`事件；

### 2、上拉刷新插件

* 微信内置浏览器`document.documentElement.scrollTop`始终为0。可以使用`document.body.scrollTop`来做兼容处理

### 3、Promise finally问题处理

* 新版的ES规则，在Promise添加了`finally` 用于处理：无论`Promise`成功与否都会执行的内容，并且本身和`then catch`一样返回`Promise`；
```js
fetch() {
  this.$loading = true;
  axios.get(url).then(res => {
    console.log(res);
    this.fetch2();
  }).finally(() => {
    this.$loading = false;
  });
},
  fetch2() {
    this.$loading = true;
    axios.get(url2).then(res => {
      console.log(res);
    }).finally(() => {
      this.$loading = false;
    });
  }
```
* `fetch fetch2`均是get请求；设想两个接口调用的同时，UI层的`loading`动画一直在。但是由于`axios.get(url).then() ..`也会返回`Promise`，所以`finally`执行是在`fetch2`代码执行之后，因此这种写法`loading`不会一直存在；可以使用`async await` 或`then catch`同时`$loading=false`;

### 4、Vue-cli 中 autoprefix 删除不符合标准的css代码的问题
```css
width: 90%;
min-height: 76px;
-webkit-line-clamp: 2;
-webkit-box-orient: vertical;
```

* 通过 `-webkit-line-clamp: 2; -webkit-box-orient: vertical;`实现两个过多文字显示`...`的效果，
* `-webkitbox-orient`  在W3C 中为非标准属性  https://developer.mozilla.org/en-US/docs/Web/CSS/box-orient   在 `autoprefix`会被删除
* 使用如下方式
```
 /*! autoprefixer: off */
...
 /*! autoprefixer: on */
```

**In vue-cli  project;** Some plugin may delete comment in css files for ugify css file; So like this
```
/* autoprefixer: off */
...
/* autoprefixer: on */
```
may be delete. In my vue project , Use this is efficient
```scss
 /*! autoprefixer: off */
...
 /*! autoprefixer: on */
```
