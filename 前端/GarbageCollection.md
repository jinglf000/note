## 垃圾回收 GC

- 函数作用域，是由函数声明时决定的；
- this的指向是由函数运行时决定的
- 函数在执行的时候，函数会调用另外一个函数，这时候会形成执行栈，进而会形成类似火焰图
- 而函数能够访问的变量是有
- 闭包，由于返回了函数，而函数的作用域是由函数定义时决定的，因此返回闭包的那个函数，在执行时所占用的内存就不会被释放；同时在决定是否释放作用域中的内存时，会扫描函数内部，是否用到作用域里的变量，发现没有被引用；
- GC（garbage collection）垃圾回收；分新生代空间和老生代空间。新生代空间主要是获取继续使用的对象，把不使用的对象，一次性删除；（对于程序而言，在运行时，会出现大量的未使用的对象，因此使用这种方式）；老生代空间，由于变动较小，都是内存一直占用的对象，因此使用标记，清除掉不使用的对象。这个地方也是产生内存泄露，导致内存增长的地方；

```
let theThing = null;
const replaceThing = function () {
  let originalThing = theThing;
  theThing = {
    longStr: new Array(1000000).join('*'),
    someMethod: function () {
      console.log(originalThing);
    }
  };
};
replaceThing()
```

多次调用replaceThing会造成内存泄露，由于theThing.someMethod有对originalThing 上一次 theThing引用，循环引用导致每次重写的theThing没有被回收；GC会扫秒函数已确定哪些变量是否被引用，不被引用的会被回收；

```
let theThing = null;

// let list = [];

const replaceThing = function () {

  let originalThing = theThing;

  let unused = function () {

    if (originalThing)

      console.log("hi");

  };


  // const stx = new Array(1000000).join('--0-0-0-0-0-')

  theThing = {

    longStr: new Array(1000000).join('*'),

    someMethod: function () {

      console.log('');

    }

  };

  // list.push(new Array(1000000).join('-*-'));

};
```

这个例子中，虽然 someMethod 没有引用originalThing，但是却是被一个没用的函数unused所引用，虽然unused没有被使用，但是，originalThing还是被标记为引用，因此仍然不能被GC回收。仍然会造成内存泄露。