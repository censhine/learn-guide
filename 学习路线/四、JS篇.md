# 四、JS篇

## 1 JS 数据类型 ?
**数据类型主要包括两部分：**

- 基本数据类型： Undefined、Null、Boolean、Number 和 String
- 引用数据类型： Object (包括 Object 、Array 、Function)
- ECMAScript 2015 新增:Symbol(创建后独一无二且不可变的数据类型 )
## 2 判断一个值是什么类型有哪些方法？
- typeof 运算符
- instanceof 运算符
- Object.prototype.toString 方法
## 3 null 和 undefined 的区别？
- null 表示一个对象被定义了，值为“空值”；
- undefined 表示不存在这个值。
- （1）变量被声明了，但没有赋值时，就等于undefined。 
- （2) 调用函数时，应该提供的参数没有提供，该参数等于undefined。 
- （3）对象没有赋值的属性，该属性的值为undefined。 
- （4）函数没有返回值时，默认返回undefined。

## 4 怎么判断一个变量arr的话是否为数组（此题用 typeof 不行）？
- arr instanceof Array
- arr.constructor == Array
- Object.prototype.toString.call(arr) == ‘[Object Array]’

## 5 “ ===”、“ ==”的区别？
- ==，当且仅当两个运算数相等时，它返回 true，即不检查数据类型
- ===，只有在无需类型转换运算数就相等的情况下，才返回 true，需要检查数据类型

## 6 “eval是做什么的？
- 它的功能是把对应的字符串解析成 JS 代码并运行；
- 应该避免使用 eval，不安全，非常耗性能（2次，一次解析成 js 语句，一次执行）。

## 7 箭头函数有哪些特点？
- 不需要function关键字来创建函数
- 省略return关键字
- 改变this指向

## 8 var、let、const 区别？
- var 存在变量提升。
- let 只能在块级作用域内访问。
- const 用来定义常量，必须初始化，不能修改（对象特殊）

## 9 new操作符具体干了什么呢？
- 1、创建一个空对象，并且 this 变量引用该对象，同时还继承了该函数的原型。
- 2、属性和方法被加入到 this 引用的对象中。
- 3、新创建的对象由 this 所引用，并且最后隐式的返回 this 。

## 10 JSON 的了解？
- JSON(JavaScript Object Notation) 是一种轻量级的数据交换格式。
- 它是基于JavaScript的一个子集。数据格式简单, 易于读写, 占用带宽小

## 11 document.write 和 innerHTML 的区别？
- document.write 只能重绘整个页面
- innerHTML 可以重绘页面的一部分

## 12 ajax过程？
- (1)创建XMLHttpRequest对象,也就是创建一个异步调用对象.
- (2)创建一个新的HTTP请求,并指定该HTTP请求的方法、URL及验证信息.
- (3)设置响应HTTP请求状态变化的函数.
- (4)发送HTTP请求.
- (5)获取异步调用返回的数据.
- (6)使用JavaScript和DOM实现局部刷新.

## 13 请解释一下 JavaScript 的同源策略？
- 概念:同源策略是客户端脚本（尤其是Netscape Navigator2.0，其目的是防止某个文档或脚本从多个不同源装载。
- 这里的同源策略指的是：协议，域名，端口相同，同源策略是一种安全协议。
- 指一段脚本只能读取来自同一来源的窗口和文档的属性。

## 14 介绍一下闭包和闭包常用场景？
- 闭包是指有权访问另一个函数作用域中的变量的函数，创建闭包常见方式，就是在一个函数的内部创建另一个函数
- 使用闭包主要为了设计私有的方法和变量，闭包的优点是可以避免变量的污染，缺点是闭包会常驻内存，会增-大内存使用量，使用不当很容易造成内存泄露。在js中，函数即闭包，只有函数才会产生作用域的概念。

**闭包有三个特性：**
- 函数嵌套函数
- 函数内部可以引用外部的参数和变量
- 参数和变量不会被垃圾回收机制回收
- 应用场景，设置私有变量的方法
- 不适用场景：返回闭包的函数是个非常大的函数
- 闭包的缺点就是常驻内存，会增大内存使用量，使用不当会造成内存泄漏
## 15 javascript的内存(垃圾)回收机制？
- 垃圾回收器会每隔一段时间找出那些不再使用的内存，然后为其释放内存
- 一般使用标记清除方法(mark and sweep), 当变量进入环境标记为进入环境，离开环境标记为离开环境
- 垃圾回收器会在运行的时候给存储在内存中的所有变量加上标记，然后去掉环境中的变量以及被环境中变量所引用的变量（闭包），在这些完成之后仍存在标记的就是要删除的变量了
- 还有引用计数方法(reference counting), 在低版本IE中经常会出现内存泄露，很多时候就是因为其采用引用计数方式进行垃圾回收。引用计数的策略是跟踪记录每个值被使用的次数，当声明了一个 变量并将一个引用类型赋值给该变量的时候这个值的引用次数就加1，如果该变量的值变成了另外一个，则这个值得引用次数减1，当这个值的引用次数变为0的时 候，说明没有变量在使用，这个值没法被访问了，因此可以将其占用的空间回收，这样垃圾回收器会在运行的时候清理掉引用次数为0的值占用的空间。
- 在IE中虽然JavaScript对象通过标记清除的方式进行垃圾回收，但BOM与DOM对象却是通过引用计数回收垃圾的， 也就是说只要涉及BOM及DOM就会出现循环引用问题。
## 16 JavaScript原型，原型链 ? 有什么特点？
- 任何对象都有 proto 隐式原型, 等于 构造函数 的 prototype
- const obj = {}
```javascript 
obj.__proto__ === Object.prototype // true
```

- 任何函数都有 prototype 显示原型 等于 原型对象(就是一个普通对象包含公共属性)
- *(通过Function.prototype.bind方法构造出来的函数是个例外，它没有prototype属性)
```javascript 
function Person () {}
Person.prototype = 原型对象
Person.prototype.constructor === Person // true

const person1 = new Person
person1.__proto__ === Person.prototype // true
person1.constructor == Person // true
``` 

- 对象还具有 constructor 属性，指向构造函数（Person.prototype.constructor == Person）
- 原型链是依赖于__proto__, 查找一个属性会沿着 proto 原型链向上查找，直到找到为止。
- 特殊
```javascript 
// 原型链最终点是 null 
Object.prototype.__proto__ === null // true
obj.__proto__.__proto__ === null // true
``` 

- 每个对象都会在其内部初始化一个属性，就是prototype(原型)，当我们访问一个对象的属性时，
- 如果这个对象内部不存在这个属性，那么他就会去prototype里找这个属性，这个prototype又会有自己的prototype，
- 于是就这样一直找下去，也就是我们平时所说的原型链的概念。
- 关系：instance.constructor.prototype = instance.proto
- **特点：**
- JavaScript对象是通过引用来传递的，我们创建的每个新对象实体中并没有一份属于自己的原型副本。当我们修改原型时，与之相关的对象也会继承这一改变。
## 17 用js递归的方式写1到100求和？
```javascript 
function add(num1, num2) {
	const num = num1 + num2;
    if(num2 === 100) {
        return num;
	} else {
	    return add(num, num2 + 1)
    }
}
var sum = add(1, 2);              
``` 
## 18 事件队列（宏任务微任务）
- 可以分为微任务（micro task）队列和宏任务（macro task）队列。

- 微任务一般比宏任务先执行，并且微任务队列只有一个，宏任务队列可能有多个。另外我们常见的点击和键盘等事件也属于宏任务。

- 下面我们看一下常见宏任务和常见微任务。

**常见宏任务：**

- setTimeout()
- setInterval()
- setImmediate()

**常见微任务：**

- promise.then()
- promise.catch()
- new MutaionObserver()
- process.nextTick()

**微任务和宏任务的本质区别:**

- 宏任务特征：有明确的异步任务需要执行和回调；需要其他异步线程支持。
- 微任务特征：没有明确的异步任务需要执行，只有回调；不需要其他异步线程支持。
```javascript 
setTimeout(function () {
    console.log("1");
}, 0);

async function async1() {
    console.log("2");
    const data = await async2();
    console.log("3");
    return data;
}

async function async2() {
    return new Promise((resolve) => {
        console.log("4");
        resolve("async2的结果");
    }).then((data) => {
        console.log("5");
        return data;
    });
}

async1().then((data) => {
    console.log("6");
    console.log(data);
});

new Promise(function (resolve) {
    console.log("7");
  resolve()
}).then(function () {
    console.log("8");
});

// 2 4 7 5 8 3 6 async2的结果 1
```
## 19 async/await
- async 是一个通过异步执行并隐式返回 Promise 作为结果的函数。是Generator函数的语法糖，并对Generator函数进行了改进。

**改进：**

- 内置执行器，无需手动执行 next() 方法。
- 更好的语义
- 更广的适用性：co模块约定，yield命令后面只能是 Thunk 函数或 Promise 对象，而async函数的await命令后面，可以是 Promise 对象和原始类型的值（数值、字符串和布尔值，但这时会自动转成立即 resolved 的 Promise 对象）。
- 返回值是 Promise，比 Generator 函数返回的 Iterator 对象方便，可以直接使用 then() 方法进行调用。
- async 隐式返回 Promise 作为结果的函数，那么可以简单理解为，await后面的函数执行完毕时，await会产生一个微任务(Promise.then是微任务)。
## 20 JavaScript 是单线程的，浏览器是多进程的
- 每打开一个新网页就会创建一个渲染进程
- 渲染进程是多线程的
- 负责页面渲染的 GUI 渲染线程
- 负责JavaScript的执行的 JavaScript 引擎线程，
- 负责浏览器事件循环的事件触发线程，注意这不归 JavaScript 引擎线程管
- 负责定时器的定时触发器线程，setTimeout 中低于 4ms 的时间间隔算为4ms
- 负责XMLHttpRequest的异步 http 请求线程
- GUI 渲染线程与 JavaScript 引擎线程是互斥的
- 单线程JavaScript是因为避免 DOM 渲染的冲突，web worker 支持多线程，但是 web worker 不能访问 window 对象，document 对象等。

---