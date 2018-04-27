# gulp

### 1、gulp.src

`gulp.src` 输入流，产生消费流，用于下游流。src的`globs`可以输入多个`glob`参数，每个`glob`符合[glob语法](https://github.com/isaacs/node-glob),多个规则的实现，则是其在`glob`的基础之上封装而来。
- `['../testFile/**/*.js', '!../testFile/**/b*.js']`类似于这种的否定实现并不符合`glob`语法
- gulp的src实现分为肯定的路径和否定的路径

一下代码是gulp.src实现数组匹配的实现
```js

const glob = require('glob');

// glob('../src/+(cstj|qysb)/*.html', (err, matches) => {
// 	console.log(matches.length);
// });

// ? * {} ?*+@(|||)

// glob need string pattern but
// vinyl-fs by gulp (path and content) need string and
// array pattern use it 。you can get it by vinyl-fs

// glob('../testFile/!(b).js', (err, matches) => {
// 	console.log(matches);
// });

// glob.src('')

const Glob = glob.Glob;
// glob snytx {a,b,v} represent that chartacter can be the one of {...}

// glup.src 实现自定义排除的原理是 new Glob(pattern, {ignore: xxx}) opts的ignore属性
// 并且 数组的开头必须是肯定的匹配

// const positive = '../testFile/**/*.{js,html,css}'; // 和下面一种方式等价
const positive = '../testFile/**/*.?(js|html|css)';
const negative = '../testFile/**/b*.js';

const myGlob = new Glob(positive, { ignore: negative }, (err, matches) => {
	if (err) return;
	console.log(matches);
});

```

`gulp.src`进行流式操作时，流中每一个文件都是单独的文件；这和参数中的`buffer:true`


### 2、path 模块

在window平台了和其他（就以linux为代表）平台上，读取文件时，文件的路径分割符时不一样的；
window为`E:\github\note\前端` 分割符为：\
linux 为`E:/github/note/前端` 分割符为：/

`path.resolve()` 把给的路径或路径片段转换为 绝对路径
`path.relative()` 把给的路径或路径片段转换为 相对路径

path模块中没有对window路径和linux的转换方法，需要自己转换；
同时把window路径和linux路径传入 path对应的方法时，无法得到正确的结果；


要想在任何操作系统上处理 Windows 文件路径时获得一致的结果，可以使用 path.win32：
要想在任何操作系统上处理 POSIX 文件路径时获得一致的结果，可以使用 path.posix：


QUESTION: 转换后路径的分隔符变了
```
const path = require('path');
// const dir = "e:/github/gulp/src";
// const src = "./include/test.html";
const dir = "e:/github/gulp/src/a/b/include";
const src = "../../../styles/images/add.png";
let res = path.join(dir, src);
console.log(res); // e:\github\gulp\src\styles\images\add.png
```

### 3、cheerio 包

cheerio 能够在Node端模拟jQuery的DOM实现，并且cheerioDOM 本身特性和原生的DOM特性是一致的。
下一变量`dom`指的是`cheerioDOM`cheerio实现的DOM
譬如：DOM的唯一性，当往body里面添加元素时，`$('body').append(dom)`那么原来`dom`中含有的cheerioDOM就不在存在了
本次对`dom`进行属性的修改，在次调用时，`dom`的属性就是修改过的了；
在解析html字符串时，`cheerio`会把`script link`放到head里，元素标签方到body里；
```js
const $ = cheerio.load('<h3>sss</h3>');
```
```js
const cheerio = require('cheerio');

let str = `
	<link href="./base.css"></link>
	<script src="./base.js"></script>
	<h3>dsds</h3>
`
const $ = cheerio.load(str);
console.log($.html());
//解析结果： <html><head><link href="./base.css">
        <script src="./base.js"></script>
        </head><body><h3>dsds</h3>
</body></html>
```