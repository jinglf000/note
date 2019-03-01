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