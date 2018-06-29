## JS问题整理，承接 js.md

### 1、touch事件补充
* 移动端或`chrome`移动调试时，点击会触发`touch`事件
* `touch`事件分为：`touchStart` `touchMove` `touchEnd`
* 点击时会首先触发`touchStart`事件，滑动时会不断的触发`touchMove`事件（不滑动事件不会触发），长按时也不会触发；点击离开时会触发`touchEnd`事件；

### 2、上拉刷新插件

* 微信内置浏览器`document.documentElement.scrollTop`始终为0。可以使用`document.body.scrollTop`来做兼容处理





