## css 2

[TOC]
<hr/>
#### 1、 background-clip 
* 控制`background-color`或者`background-image`在背景图里显示的范围。
* 该属性在chrome调试面板里不能实时响应。需要刷新才能显示。
* 默认情况下，`background-color`会扩充到 `content - padding - border`border；border-color的颜色排列是在背景色之上的；默认情况下：`border-color:rgba(@color, 0.1) background-color:@color;`会显示不出来borde颜色，因为透明度的关系；

#### 2、border-radius
可能的设置方式：
```css
border-radius: 24px 12px 24px 10px;// 按照上右下左的顺序依次设置，圆角矩形的宽度，类似于padding、margin、border
border-top-left-raduis: 24px 24px;// 表示圆角的横轴和竖轴，不一致是圆角可能为椭圆，如果只设置一个值，表明横轴和竖轴是一致的
// 单位为百分制的时候，相对于元素的（包含border的）宽高
border-radius: 50%;
border-top-left-raduis: 50% 50%;// 若元素的宽高为 40px 20px那么 radius为 20px 10px;
```

#### 3、查阅MDN文档
- 查询方法、样式、标签的详细定义，获得方法调用的边界情况，属性取值的准确描述，譬如：不同样式属性对百分制取值有不同的定义，属性的一些准确丰富的用法。

#### 4、footer 部分一直固定到底部
无论body内容高度是多少，footer始终在底部；
```css
html{
  height: 100%;
}
body {
  min-height:100%;
  position:relative;
}
body:after {// 使用伪类撑开内容，或者使用padding-bottom;
  content: ' ';
  height: 80px;
  display: block;
  width: 100%;
}
footer {
  position: absolute;
  width: 100%;
  bottom: 0;
  height: 80px;
  left:0;
}
```
### 5、垂直居中的方式：（未完待续...）

* transfrom `transform:translate3d(-50%, -50%, 0)`;
* flex：`justify-content: center; flex: 0;`;
* 

### 6、伪类：after ：before
* 必须要添加 content 属性才能显示

### 7、touch-action
> touch-action is a CSS property that controls filtering of gesture events, providing developers with a declarative mechanism to selectively disable touch scrolling (in one or both axes) or double-tap-zooming.

`touch-action:none` 当为none时，安卓无法滚动；记录一个项目里面比较坑使用；

[touch-action](https://developer.mozilla.org/zh-CN/docs/Web/CSS/touch-action)
移动端有输入区域的弹层不要使用`position:fix`会导致IOS下弹出键盘无法把输入框推上去，这样键盘会覆盖到输入框()；

### 8、less 文件编译
less中会对变量进行运算，可以使用`~`避免less进行运算；在`calc(100vh - 35px)` ---> less `calc(75vh)` 会出现计算错误；因此使用`calc('~100vh -35px') calc('~100vh - @{@val}')`

### 9、sticky 慎用sticky
sticky可以实现粘性布局，但是要把他和fixed区分来了。在不滚动的情况下，sticky的行为和releative行为是一致的，这有可能会造成一些问题；
```html
<div class="upper"></div> // height:100vh
<div class="inner"></div> // postion: sticky; 当页面滚动到底部的时候，整体页面会被撑大；
```

### 10、多行文本显示 ...
```css
word-break: break-all;
overflow: hidden;
text-overflow: ellipsis;
display: -webkit-box;
-webkit-line-clamp: 2;
-webkit-box-orient: vertical;
```

### 11、iphone X 适配
* 添加 <meta name="viewport" content='width=device-width,initial-scale=1,minimum-scale=1,maximum-scale=1,user-scalable=0,viewport-fit=cover'>
* 应用 constant 和 env 为底部栏预留位置；
```
  // padding-bottom: constant(safe-area-inset-bottom);
  // padding-bottom: env(safe-area-inset-bottom);
```

### 12、scroll 
描述Element的高度相关的属性有：(其中的width、height描述元素本身)css 中
`clientXXX`  描述元素本身的特性
`offsetXXX` 描述元素相对于**最近的** **offsetParent**的父元素的距离；
`scrollXXX` 描述元素本身的滑动效果，子元素之所以能够在父元素中滚动，是由于父元素的原因；scroll的属性和对应的方法都是在描述父元素所拥有的功能；

更详细的描述：<https://github.com/pramper/Blog/issues/10>

父元素的overflow 决定了内部内容是如何显示的；CSS属性 **overflow** 定义当一个元素的内容太大而无法适应 [块级格式化上下文](https://developer.mozilla.org/zh-CN/docs/CSS/block_formatting_context) 时候该做什么。它是 [`overflow-x`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/overflow-x) 和[`overflow-y`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/overflow-y)的 [简写属性 ](https://developer.mozilla.org/zh-CN/docs/Web/CSS/Shorthand_properties)

<iframe class="interactive" frameborder="0" height="250" src="https://interactive-examples.mdn.mozilla.net/pages/css/overflow.html" width="100%" style="font-style: normal !important; margin: 0px; padding: 10px; border: 1px solid rgb(234, 242, 244); max-width: 100%; box-sizing: border-box; background-color: rgb(245, 249, 250); color: rgb(51, 51, 51); height: 390px; width: 1038.75px;"></iframe>

默认值为 visible；scroll 和 auto的区别是，auto在内容不超过父元素时，不显示滚动条，超过时，等价于scroll；而scroll 无论何时都会显示滚动条；(忽略mac和window环境的差异)



### 13、meta viewport 

视图实际绘制的区域为viewport，而meta中标签则定义了具体宽度；

width="device-width" 定义设备宽度
initial-scale:定义初始缩放比；定义 device-width 和veiwport 的比例；@2x iphone 375 x 667下。当initial-scale缩放为0.5时，viewport宽度为750px，也就是`window.innerWidth=750`

### 14、referrer 
使用 `<meta name="referrer" content="no-referrer">`给整个页面设置
或者单独为`<img referrerpolicy="no-referrer"/>` img a 设置，以解决403（禁止访问的问题）的；
https://javascript.ruanyifeng.com/dom/image.html#toc1 

### 15、z-index
`position:absolute; z-index:xxx;` 会相对于最近的postion不为元素预留空间，通过指定元素相对于最近的非 static 定位祖先元素的偏移，来确定元素位置。绝对定位的元素可以设置外边距（margins），且不会与其他边距合并。
z-index的情况；父元素级别 > 子元素 ；z-index 描述了在z 轴层面的元素排列顺序；在下面的例子中，红色10，白色为8；即便绿色块 在高整体的排列层级也不会高于 红色块；优先级 层级 > 区块(z-index 不同值只有在同一层级才有效)

![20190510184752](/Users/jinglf000/Github/note/imgs/20190510184752.jpg)

### 16、safe-area-inset-bottom
由于部分安卓手机不支持苹果bottom兼容写法；因此最兼容的写法应该是：注意添加兼容写法
```
height: 0;
height: env(safe-area-inset-bottom);
height: constant(safe-area-inset-bottom);
```

### 17、移动端 fixed 闪动问题；可能由于层级计算错误导致；通过添加 z-index 即可解决；

### 18、ios placeholder 无法居中的问题；
需要在input元素上设置`line-height:normal`;

### 19、单行文本省略号， 多行文本省略号

单行显示...：

```css
display: block;
overflow: hidden;
text-overflow: ellipsis;
white-space: no-wrap;
```

多行显示...：

```
overflow:hidden;
text-overflow: ellipise;
display: -webkit-box;
-webkit-line-clamp: 2;// 显示多少行
-webkit-box-orient: vertical; // 方向
```

