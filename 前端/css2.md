## css 2

#### 1、 background-clip 
* 控制`background-color`或者`background-image`在背景图里显示的范围。
* 该属性在chrome调试面板里不能实时响应。需要刷新才能显示。

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