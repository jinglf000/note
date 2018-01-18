# js
> https://43.240.139.9 堡垒机地址

### 1、Math数学运算
* Math.cos Math.sin Math.tan Math.acos Math.asin Math.atan 数据的单位为弧度
* `Math.PI / 180` 即可完成deg(角度) -> rad(弧度)
* css 中`transform:rotate(30deg)`角度单位 deg rad
* 一个数学问题，单独的cos值或者sin值是无法得到真实的角度（0-2PI）内的，需要sin和cos值

### 2、Vue中的computed计算属性和watch
> 计算属性会自动追踪依赖，只有当依赖值发生变化的时候，才会重新计算；
> 我们可以将同一函数定义为一个方法而不是一个计算属性。两种方式的最终结果确实是完全相同的。然而，不同的是计算属性是基于它们的依赖进行缓存的。计算属性只有在它的相关依赖发生改变时才会重新求值。这就意味着只要 message 还没有发生改变，多次访问 reversedMessage 计算属性会立即返回之前的计算结果，而不必再次执行函数。
> Vue 提供了一种更通用的方式来观察和响应 Vue 实例上的数据变动：侦听属性。当你有一些数据需要随着其它数据变动而变动时，你很容易滥用 watch——特别是如果你之前使用过 AngularJS。然而，通常更好的做法是使用计算属性而不是命令式的 watch 回调。
> js的数据类型分为两类：基本数据类型和对象

对于赋值而言，基本数据类型进行值传递，而对象赋值则是引用传递；
自动追踪依赖意味着，无法对计算属性做自定义配置，这时watch似乎更好些；vue有自己的设定规则，这意味着并不能满足你的所有需求，最好的方式就是，依照推荐的方式换一种实现思路；
对于基本数据类型而言，值发生变化意味着 watch 和 依赖于此的computed都要重新计算
对于对象，只有当对象引用发生变化的时候，依赖于此的 computed和watch 才会重新计算
测试代码如下
```
data() {
  reutrn {
    obj: { name: 'xxx', yy: 0}
  }
},
watch: {
  obj(val) {
    console.log('watch ', this.val);
  }
},
computed: {
  my() {
  	console.log('对my重新计算');
    return this.obj.yy;
  }
},
methods: {
  changeObj() {
    // this.obj = { name: new Date().getTime() };
    this.obj.name = new Date().getTime();
  }
},
updated() {
  onsole.log('obj', JSON.stringify(this.obj));
  console.log('my', JSON.stringify(this.my));
},
created() {
  const _this = this;
setInterval(() => {
  _this.changeObj();
  }, 1000);
}

```
### 3、touch事件
当touchstart在很小的元素上触发时，即便touch移动到元素外，touchmove、touchend事件依旧会触发
在VUE中动态设置样式，可以通过提供的`:style`或者`:class`扩展来实现，但是对于某些样式的获取和设置，比如`transform`直接通过DOM获取和设置时比较好的；
补充：对于VUE所擅长的数据渲染完全可以放心的使用，但是对于DOM宽度高度计算而言（需要确定DOM的状态后才能计算）直接计算比较好；
有两种设置样式的思路：
* 1、`:style="{ width: `${offsetWidth}px`}"`直接设置，受VUE的影响比较严重，必须要考虑DOM是否加载的情况；
* 2、拿到DOM的引用设置DOM，不受VUE的影响，代码会会有庸余；

DOM 中的值client(本身)，offset(偏移)，scroll(滚动)

### 4、vuex
用来进行组件间的数据传递，vuex包含了全局数据的存储state、读取getter、修改setter；vuex中不应该包含大量的计算逻辑；计算逻辑应该由组件来做，或者getter来做
使用vuex之前应该问的问题：
为什么要用vuex？不用行吗？
有什么数据需要放到vuex里面进行管理？好处坏处？
我是不是把复杂的处理逻辑也放到vuex里面了？

### 5、async JS异步处理（初步指导思路）
* 单个异步处理使用 `promise`
* 异步并发处理 `promise.all`
* 顺序异步 使用 `async await`






