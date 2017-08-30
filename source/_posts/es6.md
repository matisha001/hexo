---
title: ES6新增特性
tags: ['javascript','es6']
date: 2016-02-19 00:34:14
---

## let和const命令
> 不存在变量提升
> 不可重复声明
> 只在声明所在的块级作用域内有效
> 对于const来说只声明不赋值会报错

<!--more -->
### let命令

```javascript
    var a = [];
    for (var i = 0; i < 10; i++) {
        a[i] = function () {
            console.log(i);
        };
    }
    a[6](); // 10
```
如果使用let，声明的变量仅在块级作用域内有效，最后输出的是6。
```javascript
    var a = [];
    for (let i = 0; i < 10; i++) {
    a[i] = function () {
        console.log(i);
    };
    }
    a[6](); // 6
```
另外，for循环还有一个特别之处，就是设置循环变量的那部分是一个父作用域，而循环体内部是一个单独的子作用域。
```javascript
    for (let i = 0; i < 3; i++) {
    let i = 'abc';
    console.log(i);
    }
    // abc
    // abc
    // abc
```
不存在变量提升，let所声明的变量一定要在声明后使用，否则报错。var命令会发生”变量提升“现象，即变量可以在声明之前使用，值为undefined。

### const命令


const声明一个只读的常量。一旦声明，常量的值就不能改变。
```javascript
    const a = 1;
    a // 1

    a = 2;
    // TypeError: Assignment to constant variable.
```

const声明的变量不得改变值，这意味着，const一旦声明变量，就必须立即初始化，不能留到以后赋值。
```javascript
    const foo;
    // SyntaxError: Missing initializer in const declaration
```



---

## 变量的解构赋值

> 变量的声明和赋值是一体的，使用let或者const不可以重复定义

es6允许按照一定的模式，从数组和对象中提取值，对变量进行赋值。本质是模式匹配。

### 数组的解构赋值

只要某种数据结构具有 Iterator 接口，都可以采用数组形式的解构赋值。

数组模式和赋值模式统一：

```javascript 	
    let [a,[b,c],d]=[1,[2,3],4];
```
如果等号两边形式不一样，很可能获得undefined或者直接报错。

解构的默认值：

```javascript
    let [foo = true] =[];
    console.log(foo); //控制台打印出true

    let [a,b="Feng"]=['hello']
    console.log(a+b); //控制台显示“helloFeng”
```
需要注意的是undefined和null的区别
```javascript
    let [a,b="Feng"]=['hello',undefined];
    console.log(a+b); //控制台显示“helloFeng”

    let [a,b="Feng"]=['hello',null];
    console.log(a+b); //控制台显示“hellonull”
```
undefined相当于什么都没有，b是默认值。null相当于有值，但值为null。所以b并没有取默认值，而是解构成了null。

### 对象的解构赋值

> 对象的解构与数组有一个重要的不同。数组的元素是按次序排列的，变量的取值由它的位置决定；而对象的属性没有次序，变量必须与属性同名，才能取到正确的值。

如果在解构之前就定义了变量，这时候你再解构会出现问题。加圆括号解决：
```javascript
    let foo;
    ({foo} ={foo:'Feng'});
    console.log(foo); //控制台输出Feng
```
---

## 扩展运算符和rest运算符

### 对象扩展运算符（…）

当编写一个方法时，我们允许它传入的参数是不确定的。这时候可以使用对象扩展运算符来作参数，看一个简单的列子：
```js
function foo(...arg){
    console.log(arg[0]);
    console.log(arg[1]);
    console.log(arg[2]);
    console.log(arg[3]);
 
}
foo(1,2,3);//1,2,3，undefined
```
这样，可以传入多个值，并且就算方法中引用多了也不会报错。

扩展运算符的用处：

> 我们先用一个例子说明，我们声明两个数组arr1和arr2，然后我们把arr1赋值给arr2，然后我们改变arr2的值，你会发现arr1的值也改变了，因为我们这是对内存堆栈的引用，而不是真正的赋值。
```js
let arr1=['a','b','c'];
let arr2=arr1;
console.log(arr2);//["a", "b", "c"]
arr2.push('D');
console.log(arr1);//["a", "b", "c", "D"]
```
显然这不是我们想要的，可以利用扩展运算符解决：
```js
let arr1=['a','b','c'];
//let arr2=arr1;
let arr2=[...arr1];
console.log(arr2);//["a", "b", "c"]
arr2.push('D');
console.log(arr2);//["a", "b", "c", "D"]
console.log(arr1);//["a", "b", "c"]
```
### rest运算符

如果你已经很好的掌握了对象扩展运算符，那么理解rest运算符并不困难，它们有很多相似之处，甚至很多时候你不用特意去区分。它也用…（三个点）来表示，我们先来看一个例子。
```js
function foo(first,...arg){
    for(let val of arg){
        console.log(val);
    }
}
foo(0,1,2,3,4,5,6,7);
```
---

## 字符串模版

ES6对字符串新增的操作，最重要的就是字符串模版，字符串模版的出现让我们再也不用拼接变量了，而且支持在模板里有简单计算操作。

### 字符串模版

支持html标签:

```js
let hello='hello';
let hw = `${hello}<b>world!</b><br/>字符串模版。`;
document.write(hw);
```
对运算的支持：

```js
let a=1;
let b=2;
let result=`${a+b}`;
document.write(result);
```
### 字符串查找

> ES6还增加了字符串的查找功能，而且支持中文!

查找是否存在:
```js
let hello='你好';
let hw = '。。。你好！world！';
console.log(hw.indexOf(hello));//3 ES5
console.log(hw.includes(hello));//true ES6
```
判断开头是否存在：
```js
console.log(hw.startsWith(hello));
```
判断结尾是否存在：
```js
console.log(hw.endsWith(hello));
```

### 复制字符串

```js
console.log('ha |'.repeat(3));//ha |ha |ha |
```