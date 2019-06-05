# 问题

### 1、 正则表达式，字符串的问题

  `/(iPhone|iPad|android)/g;`

### 2、内嵌iframe 高度设置的问题，

  * iframe元素的高度设置；1、`style: {height: 500px}` ；2、height 属性

  * |  类型  | IOS safari | chrome | Mac safari |
    | :--: | :--: | :--: | :--: |
    |    `<iframe height="500px">`    | ❌ | ✔️ |  ✔️ |
    |  |      |      |
    |      |      |      |

  * 在不同的浏览器下指的是(safari、chrome、pc)，iframe的高度是不一样的，有可能iframe是能够被内容撑开，也有可能撑不开；

  * 跨域的情况下`iframe.contentWindow.document` 不能够获取iframe内部的document对

### 3、错引了一个文件，导致压缩版出现巨多的错误堆栈
由于dev环境中脚手架无法提供详细的错误堆栈，导致问题定位比较麻烦；
```
import { Link } from 'react-router';// 原本
import { Link } from 'app/util';// 错写成
```

### 4、JS数值计算的问题

```js
1.1 - 1 // 0.100000000009
(5.9799999999999995) * (Math.pow(10, 2))// 598
```

由于语言本身的格式问题，js在进行算术运算的时候，会出现误差；

### 5 antd Modal Form
```jsx
<Modal visible>
	<Form>
		<FormItem />
	</Form>
</Modal>
// MyModalForm
{visible ? MyModalForm: null}// 1
<MyModalForm visible={visible}></MyModalForm>//2
```

当使用第二种方式时，输入框无法输入值？？

6、React 

Cannot read property 'getHostNode' of null 在使用 antd tabs 组件时，`<TabPane tab="name"></TabPane>`
or` <TabPane tab={<span>name</span>}></TabPane>`



### 6、ant-mobile 
使用ant-mobile Tabs 组件是 传入 tabs的参数数组，不能还有 key字段，否则tab 内容无法显示
```
tabs = [
  {title: '1', key: '1'},
  {title: '2', key: '2'}
]
```
ant-mobile list-view 配合 DVA 使用时，一定要注意清除 listView dataSource 为默认值

### 7、node_modules 
package.json 文件引用的版本是多少？
node_modules 文件夹中的结构是什么？下划线的文件版本是什么？

[中台H5](https://yuque.antfin-inc.com/zhenjiang.szj/blog/kuagyi)

### 8、Content-type setting ？？？ 文件下载？

当一个元素变为inline时，text-align是能够影响到这个元素的，text-align会让元素居中；
同时原本适用的vertical-align也是适用的，vertical-align:middle。会让元素垂直居中；只不过这种方法限制比较大；

