---
title: vue2.x组件
tags: ['javascript', 'vue','frame']
date: 2016-09-29 00:34:14
---

## 组件基础



### 组件的注册

![image](http://note.youdao.com/yws/res/1093/2EF21FDCC850470488F9EE6F087E3C5D)

---

### DOM模板解析

> Vue 只有在浏览器解析和标准化 HTML 后才能获取模版内容。

```
<ul> ， <ol>， <table> ， <select> 限制了能被它包裹的元素， <option> 只能出现在其它元素内部。在自定义组件中使用这些受限制的元素时会导致一些问题。
```



![image](http://note.youdao.com/yws/res/1098/CDB1FD29C22A4F5E8C6EEAF662DF8CAA)



自定义组件 <my-row>被认为是无效的内容，因此在渲染的时候会导致错误。变通的方案是使用特殊的 is 属性。

<!--more -->


> 如果您使用来自以下来源之一的字符串模板，这些限制将不适用
```
<script type="text/x-template">
JavaScript 内联模版字符串
.vue 组件
```
---


### data-必须是函数

> 通过 Vue 构造器传入的各种选项大多数都可以在组件里用。data 是一个例外，它必须是函数

---
### 组件命名


![image](http://note.youdao.com/yws/res/16573/D6ADCF52A5E4453C8E545A08246CDDC2)

组件未经 slot 元素传递内容，你甚至可以在组件名后使用 / 使其自闭合

---

### 可复用组件
可复用的组件的API 来自三部分—— props , events ,和 slots 
1. Props 允许外部环境传递数据给组件
2. Events 允许组件触发外部环境的副作用
3. Slots 允许外部环境将额外的内容组合在组件中。


推荐使用slot内容分发的具名slot与作用域插槽具名slot主要用于移动端的header组件，作用域插槽主要用于列表类组件

## Slot 分发内容
分发内容是在父作用域内编译

```html
<child-component>
  {{ message }}
</child-component>
message 应该绑定到父组件的数据
```

父组件模板的内容在父组件作用域内编译；子组件模板的内容在子组件作用域内编译。


```
试图在父组件模板内将一个指令绑定到子组件的属性/方法
<!-- 无效 -->
<child-component v-show="someChildProperty"></child-component>
如果someChildProperty是子组件的属性。父组件模板不应该知道子组件的状态,要绑定作用域内的指令到对应子组件的根节点
```

### 单个slot
> 除非子组件模板包含至少一个<slot>插口，否则父组件的内容将会被丢弃。当子组件模板只有一个没有属性的 slot 时，父组件整个内容片段将插入到 slot 所在的 DOM 位置，并替换掉 slot 标签本身。


在 <slot> 标签中的任何内容都被视为备用内容。备用内容在子组件的作用域内编译，并且只有在宿主元素为空，且没有要插入的内容时才显示备用内容。
![image](http://note.youdao.com/yws/res/16570/A935FD2C3B95490CB206B14C0121A7D1)

### 具名Slot
<slot> 元素可以用一个特殊的属性 name 来配置如何分发内容。多个 slot 可以有不同的名字。具名 slot 将匹配内容片段中有对应 slot 特性的元素。
![image](http://note.youdao.com/yws/res/16569/6157D12F236B410C8A91A8F5FF44F1BD)
仍然可以有一个匿名 slot ，它是默认 slot ，作为找不到匹配的内容片段的备用插槽。如果没有默认的 slot ，这些找不到匹配的内容片段将被抛弃。

---

### 作用域插槽

作用域插槽是一种特殊类型的插槽，用作使用一个(能够传递数据到) 可重用模板替换已渲染元素。

> 在父级中，具有特殊属性scope的<template>元素必须存在，表示它是作用域插槽的模板。scope的值对应一个临时变量名，此变量接收从子组件中传递的 props 对象


```html
子组件
<ul>
  <slot name="item"
    v-for="item in items"
    :text="item.text">
    <!-- 这里写入备用内容 -->
  </slot>
</ul>
父组件
<my-awesome-list :items="items">
  <!-- 作用域插槽也可以是具名的 -->
  <template slot="item" scope="props">
    <li class="my-fancy-item">{{ props.text }}</li>
  </template>
</my-awesome-list>
```
---

## 各种组件

### 动态组件
多个组件可以使用同一个挂载点，然后动态地在它们之间切换。使用保留的 <component> 元素，动态地绑定到它的 is特性。

![image](http://note.youdao.com/yws/res/16576/07C1B01FB7F4443CAF3A926A899F857B)

```
<!-- 组件在 vm.currentview 变化时改变！ -->
```
### keep-alive组件存内存
如果把切换出去的组件保留在内存中，可以保留它的状态或避免重新渲染。为此可以添加一个 keep-alive 指令参数。

```html
<keep-alive>
  <component :is="currentView">
    <!-- 非活动组件将被缓存！ -->
  </component>
</keep-alive>
```

<keep-alive> 包裹动态组件时，会缓存不活动的组件实例，而不是销毁它们。和 <transition> 相似，<keep-alive> 是一个抽象组件：它自身不会渲染一个DOM元素，也不会出现在父组件链中。当组件在 <keep-alive> 内被切换，它的 activated 和 deactivated这两个生命周期钩子函数将会被对应执行。主要用于保留组件状态或避免重新渲染。

### 递归组件
组件在它的模板内可以递归地调用自己，不过，只有当它有 name 选项时才可以。

![image](http://note.youdao.com/yws/res/16577/59F673EB9EED4491BB161469ED35432D)


### 内联模版
子组件有 inline-template特性，组件将把它的内容当作它的模板，而不是把它当作分发内容。
![image](http://note.youdao.com/yws/res/16578/0AA408327CF847FA8D72E4D27DFBFE58)

### X-Templates
![image](http://note.youdao.com/yws/res/16584/404EF58810D34B7FB18EBF69C94836BD)


### 异步组件
Vue.js 允许将组件定义为一个工厂函数，动态地解析组件的定义。Vue.js 只在组件需要渲染时触发工厂函数，并且把结果缓存起来，用于后面的再次渲染。

工厂函数接收一个resolve回调，在收到从服务器下载的组件定义时调用。也可以调用 reject(reason) 指示加载失败。
![image](http://note.youdao.com/yws/res/16575/8AA6CC10291245E08ECE8BF448DA470D)

2.3.0 新增

```
const AsyncComp = () => ({
  // 需要加载的组件. 应当是一个 Promise
  component: import('./MyComp.vue'),
  // loading 时应当渲染的组件
  loading: LoadingComp,
  // 出错时渲染的组件
  error: ErrorComp,
  // 渲染 loading 组件前的等待时间。默认：200ms.
  delay: 200,
  // 最长等待时间。超出此时间则渲染 error 组件。默认：Infinity
  timeout: 3000
})
```


### v-once静态组件
当组件中包含大量静态内容时，可以考虑使用 v-once 将渲染结果缓存起来。

![image](http://note.youdao.com/yws/res/1337/6935344FE4DA42FDAB36EF4676D06D46)

通过v-once指令，能够执行一次性的插值，但数据变化时，插值处的内容不会更新，可能会影响到该节点上的数据绑定。

```
<span v-once>{{message}}</span>
在vue1.x版本中禁止模板刷新数据使用的是
<span>{{*message}}</span>
```

### v-html

```html
插入纯html代码以前用{{{}}},现在用v-html
<div v-html="rawHtml"></div>
```




### 子组件索引
在 JavaScript 中直接访问子组件，可以使用ref为子组件指定一个索引 ID 。当ref和v-for一起使用时，ref是一个数组或对象，包含相应的子组件。
![image](http://note.youdao.com/yws/res/16586/771BD2C518724194AA4B2278A2B862DA)

$refs 只在组件渲染完成后才填充，并且它是非响应式的。它仅仅作为一个直接访问子组件的应急方案——应当避免在模版或计算属性中使用 $refs 。


---

## 组件的通信


### 父子组件通信
在 Vue 中，父子组件的关系可以总结为 props down, events up。父组件通过 props 向下传递数据给子组件，子组件通过 events 给父组件发送消息。
![image](http://note.youdao.com/yws/res/16574/CA896A5DFEC7458C8115DBCB1188D457)


#### 父组件向子组件props传递数据
> 组件实例的作用域是孤立的,让子组件使用父组件的数据,需要通过子组件的 props 选项。

prop 是父组件用来传递数据的一个自定义属性。子组件需要显式地用 props 选项 声明 "prop"。

![image](http://note.youdao.com/yws/res/16582/DF9C47262D6140E3B4D4243D65C4A2F0)



HTML 特性不区分大小写。当使用非字符串模版时，名字形式为 camelCase 的 prop 用作特性时，需要转为 kebab-case（短横线隔开）。
 

![image](http://note.youdao.com/yws/res/16587/8A6DCC7A7C4F406F98CB4A81BF38D2DB)


在模板中,用 v-bind。每当父组件的数据变化时，该变化也会传导给子组件

![image](http://note.youdao.com/yws/res/16588/EAB35643DF344DBCA6EC61D28F909E2B)



```html
<!-- 传递了一个字符串 "1" -->
<comp some-prop="1"></comp>
<!-- 传递实际的 number -->
<comp v-bind:some-prop="1"></comp>
prop传递的为字符串
使用 v-bind，让它的值被当作 JavaScript 表达式计算
```
![image](http://note.youdao.com/yws/res/16580/86E69F361CC94853A89B44693BEECA66)

- 父组件的属性变化时，将传导给子组件,防止子组件无意修改了父组件的状态。每次父组件更新时，子组件的所有 prop 都会更新为最新值。

- 不应该在子组件内部改变 prop


```
定义一个局部变量，并用 prop 的值初始化它
props: ['initialCounter'],
data: function () {
  return { counter: this.initialCounter }
}
```

```
定义一个计算属性，处理 prop 的值并返回
props: ['size'],
computed: {
  normalizedSize: function () {
    return this.size
  }
}
```

> 注意在 JavaScript中对象和数组是引用类型，指向同一个内存空间，如果 prop 是一个对象或数组，在子组件内部改变它会影响父组件的状态。


组件可以为 props指定验证要求。如果未指定验证要求，Vue会发出警告。props是一个对象而不是字符串数组时，它包含验证要求

```
<div id="test">
    <comp :prop-a="1"  prop-b="1"></comp>
</div>
Vue.component('example', {
  props: {
    // 基础类型检测 (`null` 意思是任何类型都可以)
    propA: Number,
    propB: [String, Number],// 多种类型
    propC: {// 必传且是字符串
      type: String,
      required: true
    },
    propD: {// 数字，有默认值
      type: Number,
      default: 100
    },
    propE: {// 数组/对象的默认值应当由一个工厂函数返回
      type: Object,
      default: function () {
        return { message: 'hello' }
      }
    },
    propF: {// 自定义验证函数
      validator: function (value) {
        return value > 10
      }
    }
  }
})
```
type 可以是下面原生构造器:
String Number Boolean Function Object Array
type 也可以是一个自定义构造器，使用 instanceof 检测。

> 当 prop 验证失败，Vue 会在抛出警告。注意 props 会在组件实例创建之前进行校验


#### 父组件向子组件非props传递数据


```
bs-date-input 的子组件模板
<input type="date" class="form-control">
<bs-date-input
  data-3d-date-picker="true"
  class="date-picker-theme-dark"
></bs-date-input>

```
对于多数特性来说，传递给组件的值会覆盖组件本身设定的值。即例如传递 type="large" 将会覆盖 type="date" 且有可能破坏该组件！使用 class 和 style 特性的值都会做合并(merge)操作，让最终生成的值为：form-control date-picker-theme-dark。



####  子组件向父组件传递数据
> 使用.sync 修饰符,当一个子组件改变了一个prop的值时，这个变化也会同步到父组件中所绑定的值。 (注意此处在 2.3.0版本以后)

### 其他组件之间的通信


```
var bus = new Vue()
// 触发组件 A 中的事件
bus.$emit('id-selected', 1)
// 在组件 B 创建的钩子中监听事件
bus.$on('id-selected', function (id) {
  // ...
})
```






