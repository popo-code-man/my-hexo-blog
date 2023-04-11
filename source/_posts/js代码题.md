---
title: js代码题
date: 2022-07-01 22:58:49
tags: js
categories: 面试题
cover: js图片.jpg
top_img: js图片.jpg
---

<!-- {% asset_img js图片.jpg 这是一张图片 %} -->

### 递归累加 1 到 100

```javascript
function getSum(n) {
	if (n == 1) {
		return 1;
	}
	return n + getSum(n - 1);
}
var res = getSum(100);
console.log("res", res);
```

### 数组去重方法

1. 循环原有数组中的每一项，每拿到一项都往新数组中添加，添加之前验证数组中是否存在这一项，不存在再添加

```javascript
let arr = [1, 4, 6, 8, 9, 5, 3, 3, 11, 3, 4, 5, 6, 74, 3, 1, 5, 3];
let newArr = [];
for (let i = 0; i < arr.length; i++) {
	//循环数组中每一项
	let item = arr[i];
	// 验证新数组中是否存在这一项
	if (newArr.includes(item)) {
		//如果存在，不再增加刀新数组中，继续下一轮循环
		continue;
	}
	//如果新数组不存在这一项，则加入到新数组中
	newArr.push(item);
}
console.log(newArr);
```

简化：

```javascript
let arr = [1, 4, 6, 8, 9, 5, 3, 3, 11, 3, 4, 5, 6, 74, 3, 1, 5, 3];
let newArr = [];
arr.forEach((item) => {
	if (newArr.includes(item)) return;
	newArr.push(item);
});
console.log(newArr);
```

2. 先分别拿出数组中的每一项 item,再用 item 和 item 后面的每一项以此进行比较，如果遇到和 item 相同的，则在原来的数组中把这项移除掉

```javascript
let arr = [1, 2, 3, 4, 3, 2, 1, 2, 3, 4, 4, 1, 2, 3, 3, 1, 2, 3];
for (let i = 0; i < arr.length; i++) {
	//item:当前项
	//i:当前项的索引
	let item = arr[i];
	// 让当前项和后面的每一项进行比较（循环）
	for (let j = i + 1; j < arr.length; j++) {
		// backItem:后面拿出来要比较的每一项
		let backItem = arr[j];
		//如果backItem和item相等，说明这一项是重复的，删掉它
		if (item == backItem) {
			arr.splice(j, 1);
			j--; //防止数组塌陷
		}
	}
}
console.log(arr);
```

3. 创建一个空对象：{},循环数组每一项，把每一项向对象中存储,如果对象中已经存在这一项，则用最后一项替换当前项，并且删除最后一项。

```javascript
let arr = [1, 2, 3, 4, 3, 2, 1, 2, 3, 4, 4, 1, 2, 3, 3, 1, 2, 3, 0];
let obj = {};
for (let i = 0; i < arr.length; i++) {
	//循环数组中的每一项
	let item = arr[i];
	if (obj[item] !== undefined) {
		//已经存在这项，则用最后一项替换当前项，并且删除最后一项（这里为解决数组塌陷问题，所以使用这种方法）
		arr[i] = arr[arr.length - 1];
		arr.length--; //arr.pop();
		i--;
		continue;
	}
	//把每一项向对象中存储
	obj[item] = item;
}
console.log(arr);
```

4. 基于 ES6 的 Set 实现去重

```javascript
let arr = [1, 2, 3, 4, 3, 2, 1, 2, 3, 4, 4, 1, 2, 3, 3, 1, 2, 3, 0];
arr = [...new Set(arr)];
console.log(arr);
```

5. 利用 Map()

> Map 对象是 JavaScript 提供的一种数据结构，结构为键值对形式，将数组元素作为 map 的键存入，然后结合 has()和 set()方法判断键是否重复。
> Map 对象：用于保存键值对，并且能够记住键的原始插入顺序。任何值（对象或者原始值）都可以作为一个键或一个值。

```javascript
function removeDuplicate(arr) {
	const map = new Map();
	const newArr = [];

	arr.forEach((item) => {
		if (!map.has(item)) {
			// has()用于判断map是否包为item的属性值
			map.set(item, true); // 使用set()将item设置到map中，并设置其属性值为true
			newArr.push(item);
		}
	});

	return newArr;
}

const result = removeDuplicate(arr);
console.log(result); // [ 1, 2, 'abc', true, false, undefined, NaN ]
```

**注意：**使用 Map()也可对 NaN 去重，原因是 Map 进行判断时认为 NaN 是与 NaN 相等的，剩下所有其它的值是根据 `===` 运算符的结果判断是否相等。

### 冒泡排序

> 冒泡排序是一种简单的排序算法。它重复走访过要排列的数列，**一次比较两个元素，如果他们的顺序错误，就把它们交换过来。** 走访数列的工作重复进行，直到排序完成。这个算法的名字由来是因为越小的元素会经由交换慢慢“浮”到数列的顶端。

```javascript
let arr = [4, 5, 2, 3, 1];
for (let i = 0; i < arr.length - 1; i++) {
	for (let j = 0; j < arr.length - i - 1; j++) {
		if (arr[j] > arr[j + 1]) {
			let temp = arr[j];
			arr[j] = arr[j + 1];
			arr[j + 1] = temp;
		}
	}
}
console.log(arr);

```

### 写一个闭包

```javascript
function demo() {
	let a = 100;
	return function () {
		console.log(a);
	};
}
let a = 200;
demo();
```

### 实现深拷贝

```javascript
function deepClone(obj) {
	let copy = obj instanceof Array ? [] : {};
	for (let i in obj) {
		if (obj.hasOwnProperty(i)) {
			copy[i] = typeof obj[i] === "object" ? deepClone(obj[i]) : obj[i];
		}
	}
	return copy;
}
```

### 实现 Promise

```javascript
// 未添加异步处理等其他边界情况
// ①自动执行函数，②三个状态，③then
class Promise {
	constructor(fn) {
		// 三个状态
		this.state = "pending";
		this.value = undefined;
		this.reason = undefined;
		let resolve = (value) => {
			if (this.state === "pending") {
				this.state = "fulfilled";
				this.value = value;
			}
		};
		let reject = (value) => {
			if (this.state === "pending") {
				this.state = "rejected";
				this.reason = value;
			}
		};
		// 自动执行函数
		try {
			fn(resolve, reject);
		} catch (e) {
			reject(e);
		}
	}
	// then
	then(onFulfilled, onRejected) {
		switch (this.state) {
			case "fulfilled":
				onFulfilled(this.value);
				break;
			case "rejected":
				onRejected(this.value);
				break;
			default:
		}
	}
}
```

### 实现一个双向数据绑定

```javascript
let obj = {};
let input = document.getElementById("input");
let span = document.getElementById("span");
// 数据劫持
Object.defineProperty(obj, "text", {
	configurable: true,
	enumerable: true,
	get() {
		console.log("获取数据了");
	},
	set(newVal) {
		console.log("数据更新了");
		input.value = newVal;
		span.innerHTML = newVal;
	},
});
// 输入监听
input.addEventListener("keyup", function (e) {
	obj.text = e.target.value;
});
```

### 实现一个节流函数

```javascript
// 思路：在规定时间内只触发一次
function throttle(fn, delay) {
	// 利用闭包保存时间
	let prev = Date.now();
	return function () {
		let context = this;
		let arg = arguments;
		let now = Date.now();
		if (now - prev >= delay) {
			fn.apply(context, arg);
			prev = Date.now();
		}
	};
}

function fn() {
	console.log("节流");
}
addEventListener("scroll", throttle(fn, 1000));
```

### 实现一个防抖函数

```javascript
// 思路:在规定时间内未触发第二次，则执行
function debounce(fn, delay) {
	// 利用闭包保存定时器
	let timer = null;
	return function () {
		let context = this;
		let arg = arguments;
		// 在规定时间内再次触发会先清除定时器后再重设定时器
		clearTimeout(timer);
		timer = setTimeout(function () {
			fn.apply(context, arg);
		}, delay);
	};
}

function fn() {
	console.log("防抖");
}
addEventListener("scroll", debounce(fn, 1000));
```
