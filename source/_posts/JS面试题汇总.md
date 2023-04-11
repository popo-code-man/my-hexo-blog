---
title: JS面试题汇总
date: 2022-07-09 21:20:02
tags: js
categories: 面试题
cover: js图片.png
top_img: 
---


### js 的数据类型有哪些？

基本类型:

- String
- Array
- Boolean
- Null
- undefined
- symbol ( ES6 新增 )

引用类型:Object 包括 Array Function Date

### 从输入 URL 到页面加载发生了什么

- DNS 解析
- TCP 连接
- 发送 HTTP 请求
- 服务器处理请求并返回 HTTP 报文
- 浏览器解析渲染页面
- 连接结束

### == 和 === 有什么区别？

`==` 不会判断类型，而 `===` 会先判断类型

### 的指向问题

- 单独的 this，指向 window
- 默认指向调用自己的对象
- 构造函数中的 this 指向生成的新对象
- 定时器中的 this，指向 window

### this 的指向？

- call: 第一个参数为要指向的对象，第二个参数之后跟普通函数传参一样
- apply: 第一个参数为要指向的对象，第二个参数之后以数组形式传参
- bind: 调用不会立即执行，而是返回一个新的改变过 this 指向的方法，而以上两个方法是立即执行的。

### 作用域和作用域链

- 作用域：在 js 预编译时、代码执行之前，对全局或者局部的变量进行收集，存放在相应的 scope 中，执行时从 scope 获取数据，scope 就是全局或者局部的作用域

- 访问变量时，会沿着 scope 一层一层找，这就叫做作用域链

### 闭包

两个连接 scope 的函数，关闭了函数的自由变量，让它暂时不会被销毁

### 闭包的特点

- 函数嵌套函数
- 函数内部可以调用外部的参数和变量
- 参数和变量不会被垃圾回收机制回收

### 数组操作方法

- push 从后新增
- pop 从后删除
- unshift 从前添加
- shift 从前删除
- sort 从小到大排序
- reverse 翻转
- concat 拼接数组
- slice 提取数组
- splice 删除 插入 替换

**遍历方法：**

| 方法    | 特点                                                 |
| ------- | ---------------------------------------------------- |
| forEach | 不会返回新的数组                                     |
| map     | 会根据条件返回一个新的数组                           |
| filter  | 过滤器                                               |
| some    | 只要数组中有一项满足回调函数中设置的条件就返回 true; |
| reduce  | 叠加器或者累加器                                     |

### 字符串操作方法

- indexOf 查找首次出现的位置
- lastIndexOf 查找最后一次出现的位置
- slice 提取字符串 可以接收负值
- subString 提取字符串 不能接收负值
- replace 用一个值替换字符串中的一个值
- concat 链接多个字符串

### 浅拷贝

- es6 的扩展运算符 “ ... ”
- 遍历赋值
- Object.assign()

### 深拷贝

- 递归遍历 + 一些判断
- JSON.parce( JSON.stringify ( Object ) )

### 防抖

在第一次触发事件时，不立即执行，而是等一段时间比如 200ms ，如果相应时间内没有再次触发事件，则执行函数，如果再次触发了，则重新开始计时

### 节流

在函数执行后，让这个函数在一定时间内失效，防止用户频繁操作

### 本地存储

<table>
  <tr>
    <th>属性</th>
    <th>特点</th>
  </tr>
  <tr>
    <td rowspan="3">cookie</td>
    <td>存储较小</td>
  </tr>
  <tr>
    <td>可以设置过期时间</td>
  </tr>
  <tr>
    <td>可与服务器传递</td>
  </tr>
  <tr>
    <td rowspan="3">localStorage</td>
    <td>存储较大</td>
  </tr>
  <tr>
    <td>永久有效，除非手动删除</td>
  </tr>
  <tr>
    <td>只在客户端保存</td>
  </tr>
  <tr>
    <td rowspan="3">sessionStorage</td>
    <td>存储较大</td>
  </tr>
  <tr>
    <td>关闭当前窗口删除</td>
  </tr>
  <tr>
    <td>只在客户端保存</td>
  </tr>
</table>

### 同步、异步？

JS 的同步异步始终都是单线程的，也就是一条任务线，但是异步时可以改变执行顺序的。

### 什么是事件冒泡

多层嵌套的元素，子元素触发事件会冒泡到父级元素

### 事件代理

本来应该加到子元素的事件，我们把他加到父元素上，event 里边存储着事件源，也就是说，我们可以知道执行事件的元素时哪个

### 定时器

- setTimeout: 只执行一次
- setInterval: 无限次执行

### 什么是原型？

每个函数都有一个 propotype 属性，它默认指向一个 Object 空对象，这个对象就叫做原型，原型对象中都有一个 constructor 属性，它指向原型

### 什么是原型链？

访问一个对象的属性时，现在自身原型中查找，如果没有找到，再在 `__proto__` 这条链上查找，一直找到最上层，由 `__proto__` 连接起来的就叫原型链

### 如何实现继承？

- es6 使用: extend 继承
- 构造函数:
  - 原型链继承，让新实例的原型指向父级的实例
  - call、apply

### .call() 和 .apply() 的含义和区别？

**含义：**

call() 和 apply() 是预定义的函数方法。两个方法可用于调用函数，两个方法的第一个参数必须是对象本身。 后面的参数都是传递给当前对象的参数。

**区别：**

apply 传入的是一个参数数组，也就是将多个参数组合成为一个数组传入，而 call 则作为 call 的参数传入（从第二个参数开始）。

```javascript
Object.call(this, obj1, obj2, obj3);
Object.apply(this, arguments);
```

> 在 JavaScript 严格模式(strict mode)下, 在调用函数时第一个参数会成为 this 的值， 即使该参数不是一个对象。 在 JavaScript 非严格模式(non-strict mode)下, 如果第一个参数的值是 null 或 undefined, 它将使用全局对象替代。

### . new 操作符具体干了什么呢?

- 1、创建一个空对象，并且 this 变量引用该对象，同时还继承了该函数的原型。
- 2、属性和方法被加入到 this 引用的对象中。
- 3、新创建的对象由 this 所引用，并且最后隐式的返回 this 。

### document load 和 document ready 的区别？

- Document.onload 是在结构和样式加载完才执行 js
- window.onload：不仅仅要在结构和样式加载完，还要执行完所有的样式、图片这些资源文件，全部加载完才会触发 window.onload 事件
- Document.ready 原生中没有这个方法，jquery 中有 $().ready(function)

### 什么是同源策略？

一段脚本只能读取来自于同一来源的窗口和文档的属性

### ajax 的步骤

- 创建 XMLHttpRequest 异步对象
- 创建一个新的 HTTP 请求,并指定该 HTTP 请求的方法、URL 及验证信息
- 设置响应 HTTP 请求状态变化的函数
- 发送 HTTP 请求
- 获取异步调用返回的数据.

### DOM 节点的增删改查

- dom.appendChild() 添加
- dom.insertBefore() 插入
- dom.replaceChild() 替换
- dom.removeChild() 删除

### 怎么判断数据类型？

- typeof
  - 返回数据类型，包含这 7 种： number、boolean、symbol、string、object、undefined、function。
  - 引用类型，除了 function 返回 function 类型外，其他均返回 object。
  - 其中，null 有属于自己的数据类型 Null ， 引用类型中的 数组、日期、正则 也都有属于自己的具体类型，而 typeof 对于这些类型的处理，只返回了处于其原型链最顶端的 Object 类型
- instanceof

```javascript
console.log({} instanceof Object); //true
console.log([] instanceof Array); //true
console.log([] instanceof Object); //true
let fn = function (a, b) {
  return a + b;
};
console.log(fn instanceof Function); //true
```

- toString 结合 call

```javascript
console.log(Object.prototype.toString({})); //[object Object]
console.log(Object.prototype.toString.call("")); //[object String]
console.log(Object.prototype.toString.call(1)); //[object Number]
console.log(Object.prototype.toString.call(true)); //[object Boolean]
console.log(Object.prototype.toString.call(undefined)); //[object Undefined]
console.log(Object.prototype.toString.call(null)); //[object Null]
console.log(Object.prototype.toString.call(Symbol())); //[object Symbol]
console.log(Object.prototype.toString.call(new Error())); //[object Error]
```

- constructor

```javascript
console.log(new Number(1).constructor == Number); //true
console.log(new String(1).constructor == String); //true
console.log(true.constructor == Boolean); //true
console.log(new Object().constructor == Object); //true
console.log(new Error().constructor == Error); //true
```

### 你对Promise的理解

异步编程的一种解决方案，可以很好地解决回调地狱的问题（避免了层层嵌套的回调函数）。
- promise.then()：获取异步任务的正常结果。
- promise.catch()：获取异步任务的异常结果。
- promise.finaly()：异步任务无论成功与否，都会执行。

### Promise.all() 和 Promise.race()
- Promise.all()：并发处理多个异步任务，所有任务都执行成功，才能得到结果。
- Promise.race(): 并发处理多个异步任务，只要有一个任务执行成功，就能得到结果。
### 除了Promise还有其他异步写法？
- es7 的async await
- generator函数和yield

### es6有哪些新特性
- Let和const关键字
- 模板字符串
- 对象数组的解构赋值
- 扩展运算符
- 箭头函数
- Promise
- class
### try catch
异常捕获，只要代码中有出错，catch就会捕捉到

### 数组塌陷问题
如循环数组的过程中删除了数组的某一项 那么后边的所有索引值都会-1，最终循环结果会错误



