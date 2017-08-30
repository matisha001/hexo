---
title: vue2.x指令
tags: ['javascript', 'vue','frame']
date: 2016-10-22 00:34:14
---



## 内置指令
v-model v-for v-if v-show v-else v-on v-once v-html v-bind v-on

## 自定义指令



### 自定义全局指令

```
// 注册一个全局自定义指令 v-focus
Vue.directive('focus', {
  // 当绑定元素插入到 DOM 中。
  inserted: function (el) {
    // 聚焦元素
    el.focus()
  }
})
```
<!--more -->
### 自定义局部指令

```js
directives: {
  focus: {
    // 指令的定义---
  }
}
<input v-focus>
```


### 钩子函数
bind: 只调用一次，指令第一次绑定到元素时调用，可以定义一个在绑定时执行一次的初始化动作

inserted: 被绑定元素插入父节点时调用

update: 所在组件的 VNode 更新时调用

componentUpdated: 所在组件的 VNode 及其孩子的 VNode 全部更新时调用

unbind: 只调用一次， 指令与元素解绑时调用

### 钩子函数参数

钩子函数被赋予了以下参数：
- el: 指令所绑定的元素，可以用来直接操作 DOM 。
- binding: 一个对象，包含以下属性：
  - name: 指令名，不包括 v- 前缀。
  - value: 指令的绑定值。
  - oldValue: 指令绑定的前一个值，仅在 update 和 componentUpdated 钩子中可用。无论值是否改变都可用。
  - expression: 绑定值的字符串形式。
  - arg: 传给指令的参数。
  - modifiers: 一个包含修饰符的对象。
- vnode: Vue 编译生成的虚拟节点
- oldVnode: 上一个虚拟节点，仅在 update 和 componentUpdated 钩子中可用。


```
Vue.directive('demo', {
  bind: function (el, binding, vnode) {
    var s = JSON.stringify
    el.innerHTML =
      'name: '       + s(binding.name) + '<br>' +
      'value: '      + s(binding.value) + '<br>' +
      'expression: ' + s(binding.expression) + '<br>' +
      'argument: '   + s(binding.arg) + '<br>' +
      'modifiers: '  + s(binding.modifiers) + '<br>' +
      'vnode keys: ' + Object.keys(vnode).join(', ')
  }
})
new Vue({
  el: '#hook-arguments-example',
  data: {
    message: 'hello!'
  }
})
```

简写

```js
Vue.directive('color-swatch', function (el, binding) {
  el.style.backgroundColor = binding.value
})
```


### 对象字面量

```html
<div v-demo="{ color: 'white', text: 'hello!' }"></div>
Vue.directive('demo', function (el, binding) {
  console.log(binding.value.color) // => "white"
  console.log(binding.value.text)  // => "hello!"
})
```








 



