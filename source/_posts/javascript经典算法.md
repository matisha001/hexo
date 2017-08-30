---
title: Javascript经典算法
tags: ['javascript']
date: 2015-09-19 00:34:14
---

### 冒泡排序

```js
function bubbleSort(arr){
  for(i=0; i<arr.length-1; i++){
    for(j=i+1; j<arr.length; j++){
      if(arr[i] > arr[j]){
        var temp = arr[i];
        arr[i] = arr[j];
        arr[j] = temp;
      }
    }
  }
  return arr;
}
```
<!-- more -->
### 数组去重

> 利用Object中key的唯一性，用key来进行筛选。

```js
function unique(arr){
  var obj = {}
  var result = []
  for(var i in arr){
    if(!obj[arr[i]]){
      obj[arr[i]] = true;
      result.push(arr[i]);
    }
  }
  return result;
}
//ES6中Set实现：
let result = new Set([1,1,1,1,3]);
```

### 数组中最大差值

```js
function getMaxProfit(arr){
  var min = arr[0],
      max = arr[0];
  for(var i = 0; i < arr.length; i++){
    if(arr[i] < min) min = arr[i];
    if(arr[i] > max) max = arr[i];
  }
  return max - min;
}
```

### 统计字符串中次数最多字母

> 利用Object中key的唯一性，用key来进行筛选并计数

```js
function findMaxDuplicateChar(str) {
  if(str.length == 1) {
    return str;
  }
  var charObj = {};
  for(var i = 0; i < str.length; i++) {
    if(!charObj[str.charAt(i)]) {
      charObj[str.charAt(i)] = 1;
    } else {
      charObj[str.charAt(i)] += 1;
    }
  }
  var maxChar = '',
      maxValue = 1;
  for(var k in charObj) {
    if(charObj[k] >= maxValue) {
      maxChar = k;
      maxValue = charObj[k];
    }
  }
  return maxChar + '：' + maxValue;
}
```

### 翻转字符串

>反向遍历字符串

```js
function reverseString(str){
  var tmp = '';
  for(var i=str.length-1; i>=0; i--)
    tmp += str[i];
  return tmp
}
```
>转化成array操作

```js
function reverseString(str){
  var arr = str.split("");
  var i = 0,j = arr.length-1;
  while(i<j){
    tmp = arr[i];
    arr[i] = arr[j];
    arr[j] = tmp;
    i++;
    j--;
  }
  return arr.join("");
----------------------
function reverseString(str) {
 str = str.split('').reverse().join('');
 return str;
}
reverseString("hello");
}
```

### 生成指定长度随机字符串

```js
function randomString(n){
  var str = 'abcdefghijklmnopqrstuvwxyz0123456789';
  var tmp = '';
  for(var i=0; i<n; i++) {
    tmp += str.charAt(Math.round(Math.random()*str.length));
  }
  return tmp;
}
```

### 生成菲波那切数列（强制）

```js
function getfib(n){
  if(n == 0) return 0;
  if(n == 1) return 1;
  if(n > 1) return getfib(n-1) + getfib(n-2);
}
function fibo(len){
    var fibo = [];
    for(var i = 0; i < len; i++){
      fibo.push(getfib(i));
    }
    return fibo;
}
```

### 快速排序

```js
 var quickSort = function(arr){
      
      if(arr.length <= 1){
          return arr;
      }
      
      //定义一个左数组，定义一个右数组
      let leftArr = [];
      let rightArr = [];
     //选定一个参照值
     let tag = arr[0];
     
     /*
      * 使用如下方式判断，会把重复元素去掉，就实现了快排的同时去重
      */
     for(let i = 0; i < arr.length; i++){
         if(arr[i] < tag){ //将比tag小的元素放在左数组中
             leftArr.push(arr[i]);
         }
         if(arr[i] > tag){ //将比tag大的元素放在右数组中
             rightArr.push(arr[i]);
         }
    }
     
     //使用如下方式就是使用快排进行排序，不去重
      for(let i = 1; i < arr.length; i++){
         if(arr[i] < tag){ //将比tag小的元素放在左数组中
             leftArr.push(arr[i]);
         }else{ //将比tag大的元素放在右数组中
         }
     }
     
     //递归调用
     return [].concat(quickSort(leftArr),[tag],quickSort(rightArr));
```
