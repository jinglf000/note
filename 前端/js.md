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
自动追踪依赖意味着，无法对计算属性做自定义配置，这时watch似乎更好些；Vue有自己的设定规则，这意味着有时Vue并不能满足你的所有需求，最好的方式就是，依照推荐的方式换一种实现思路；
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
* 1、`:style="{ width: `${offsetWidth}px`}"`直接设置，受Vue影响比较严重，必须要考虑DOM是否加载的情况；
* 2、拿到DOM的引用设置DOM，不受VUE的影响，代码可能会有庸余；

DOM 中的值client(本身)，offset(偏移)，scroll(滚动)

### 4、vuex 全局的数据中心，
实现一个全局的单例，用来进行组件间的数据传递，控制数据的修改访问；vuex包含了全局数据的存储state、读取getter、修改setter；vuex中不应该包含大量的计算逻辑；计算逻辑应该由组件来做，或者getter来做
使用vuex之前应该问的问题：
为什么要用vuex？不用行吗？
有什么数据需要放到vuex里面进行管理？好处坏处？
我是不是把复杂的处理逻辑也放到vuex里面了？

### 5、async JS异步处理（初步指导思路）
* 单个异步处理使用 `promise`
* 异步并发处理 `promise.all`
* 顺序异步 使用 `async await`

**Promise**
Promise 中一旦执行了resolve或者reject，Promise本身的状态就会发生改变，并且不能再次改变；
Promise 构造函数中的错误可以被其后的catch捕获到；
以下情况不能捕获到，程序会在执行到`aaa * 1`就报错，并且不会调用then回调
```
new Promise((resolve, reject) => {
	setTimeout(() => {
    	resolve(aaa * 1);
	},1000);
});
```

异常处理，异常分为两种：1、程序运行抛出的异常，如果异常未被捕获，程序运行终止
2、用户自定义异常；通过`Error`类构造出的自定义异常；`const err = new Error('error')`程序不会报错，`Error`类和其他的类一样可以被调用和赋值；要想提示异常需要使用`throw err`;而这两类异常都是`Error`类的示例

> throw语句用来抛出一个用户自定义的异常。当前函数的执行将被停止（throw之后的语句将不会执行），并且控制将被传递到调用堆栈中的第一个catch块。如果调用者函数中没有catch块，程序将会终止。

>  try...catch语句将能引发错误的代码放在try块中，并且对应一个响应，然后有异常被抛出；catch能够捕获程序异常和自定义异常；

```
const err = new Promise((resolve, reject) => {
	setTimeout(() => {
    	resolve(new Error('errorrrrrr'));
    }, 1000);
});
err.then((res) => {
	console.log('then',res);
}).catch((err) => {
	cosnole.log('catch',err)
});
// output
// then Error: errorrrrrr
    at setTimeout (<anonymous>:3:14)
```

### 6、正则表达式
> .（小数点）匹配除换行符之外的任何单个字符。
> [\s\S] [^] 能匹配包括 \n 在内的所有字符

\S 非空白字符
\s 匹配空白字符 包括：空格、制表符、换页符和换行符；

一下内容对应的字符，只是表明了位置，并不代表任何字符，也就是**零宽**
\b 匹配一个词的边界
\B 匹配一个非单词边界
^ 字符开始
$ 字符结尾

肯定 positive lookahead (?=xx) 肯定，匹配列表中必须有xx,
否定 negative lookahead (?!) 否定，匹配列表不能有xx
```
const reg1 = /\b\d/g;
const reg2 = /\b\d(?=px)/g;
const reg3 = /\b\d(?!px)/g;
const str = '1px 2em 3pt 4px';

console.log(str.match(reg1));// [ '1', '2', '3', '4' ]
console.log(str.match(reg2));// [ '1', '4' ] 匹配一个数字，数字后面要有px，返回数字
console.log(str.match(reg3));// [ '2', '3' ] 匹配一个数字，数字后面不能有px，返回数字

```
如一下表明要匹配三个连续相同的字符，并且后面没有三个连续相同的字符
\1 \2 \3 表示匹配到的字符组；

```
var s = 'aaalllsss0tAAAnnn999';
var reg = /(\w)\1{2}(?!(\w)\2{2})/g;

console.log(s.match(reg));// [ 'sss', '999' ]
```
最后一问：
```
var web_development = "python php ruby javascript jsonp perhapsphpisoutdated";
```

找出其中 包含 p 但不包含 ph 的所有单词，即

[ 'python', 'javascript', 'jsonp' ]

引用一个大神的答案
> https://stackoverflow.com/questions/39570875/find-all-words-that-contains-p-but-not-ph/39571868#39571868
```
\b(?:p(?!h)|[^p\s])*?p(?!h)(?:p(?!h)|[^p\s])*?\b
```


### 7、字符串的操作
`str.substr(start,length)` 从指定位置获取指定长度的字符串
`str.substring(start,end)` 返回开始和结束位置的字符串


### 8、XHR对象的header
> 浏览器不允许用户手动设置敏感的Http header
包括但不限于
cookie
host
referer

因此 XHR请求中的host和referer是无法通过手动来设置的

### 9、VUE js 源码学习
http://hcysun.me/2017/03/03/Vue%E6%BA%90%E7%A0%81%E5%AD%A6%E4%B9%A0/


### 10、字符编码
>  https://www.cnblogs.com/gavin-num1/p/5170247.html   很好的介绍性文章；

计算机的符号有两种0,1；人类语言的符号则有很多，要想让语言符号能够在计算机系统之间传播必须要对字符进行编码；
* ASCII 对英文字符进行了编码；用8bit两个字节byte表示了128个符号；
* 为了能够在计算机中处理汉字，国家标准出台了GBK标准，兼容原有的ACSII并添加了独一无二的汉字，并编码了汉字对应的码集；（GBK GB2312 ...）
* Unicode 编码，将世界上所有的符号都纳入其中，每一个符号都有一个独一无二的编码；它规定了符号的二进制代码；同样也是ASCII的超集；原有的ASCII不变
* Unicode 编码是一个符号集，他只规定了符号的二进制代码，却没有规定这个二进制代码如何存储；


utf-8是unicode 的一种实现；

js中：escape 返回：返回一个字符的Unicode编码值；对应的解码为unescape
encodeURI 返回内容的编码方式，decodeURI解码；不对“; / ? : @ & = + $ , #”英文 数字编码
encodeURIComponent decodeURIComponent 对所有内容进行编码

JavaScript的字符串本来就是unicode，即不存在utf-8的字符串，也不存在gb2312的字符串；（utf-8和GB312为了存储而实现的）

``` js
const str = '你好 utf8';//
console.log(escape(str));// 返回str的unicode编码
console.log(encodeURI(str));// 返回中文的utf-8的编码（通常用于url上内容传递，因此要进行编码）
```

node.js中的 描述二进制的对象，buffer是有文件格式的可以是 utf-8 也可以是 gbk的，因此在解码的时候需要对buffer进行解码，使用`iconv-lite`

Q&A:
- 1、js中的utf-8编码，这种说法对吗？
ans：不对，js中所有的代码都是unicode（前提示文件为utf-8格式）；utf-8或者gbk都是文件存储的方式；也就是说涉及到文件存储的时候才有编码方式这一说；存储也就是对原有的unicode码的在编码；
- 2、js中涉及到文件编码的有哪些？
ans：直接读取文件时，服务器接受内容时，都是以流的方式进行存取，此时的流是有编码方式的；需要用正确的编码方式才能打开，否则的话就会出现乱码；
- 3、乱码？
ans：要想正确的打开一个文件，必须知道文件的编码方式，用utf-8的方式去打开GBK文件肯定是乱码的

### 11、js ES6+

* 后续的ES新增内容为ES5的扩充，这也就意味着，老式的js程序仍然可以在新式的浏览器中运行，原有的js写法不会发生变化，ES+标准推荐使用新的方式去书写，以便能编写出更健壮的代码；同时也就意味新增的内容也是遵循原有的规范的；


### 12、对象的valueOf toString方法
对象的`valueOf`方法能够返回对象的**原始值**（primitive），默认情况下object的原始值是对象本身，对一些js中的核心对象，返回值又各有各的不同
| 对象| 返回值 |
|---|---|
| Array | 返回数组对象本身。 |
| Boolean| 布尔值。|
| Date| 存储的时间是从 1970 年 1 月 1 日午夜开始计的毫秒数 UTC。（返回值类型为number）|
| Function| 函数本身。 |
| Number| 数字值|
| Object| 对象本身。这是默认情况。 |
| String| 字符串值。|
|Math Error| Math 和 Error 对象没有 valueOf 方法。|

**valueOf** 方法返回对象的原始值，不经常使用
**toString**方法返回对象的字符串表示，在隐式类型转换中会用到
```js
var obj = {
  name: 'hello',
  age: 12
};

obj.toString = function () {
	console.log('obj 调用了toSting方法');
	return obj.name + obj.age;
}
var str = '这是一个str';

console.log(str + obj);// 这是一个strhello12，调用了toString方法

obj = {};

console.log(str + obj);// 这是一个str[object Object]，默认toString返回'[object Object]'
```


