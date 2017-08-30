---
title: vue2.x事件
tags: ['javascript', 'vue','frame']
date: 2016-09-30 00:34:14
---

## 事件
### 自定义事件
使用 v-on 绑定自定义事件
- 使用 $on(eventName) 监听事件
- 使用 $emit(eventName) 触发事件


> 父组件可以在使用子组件的地方直接用v-on来监听子组件触发的事件

> 不能用 $on 侦听子组件释放的事件，而必须在模板里直接用 v-on 绑定


> 可以使用 .native修饰v-on，在某个组件的根元素上监听一个原生事件

<!--more -->

## 数据绑定

### 子组件改变父组件
> 使用.sync 修饰符,当一个子组件改变了一个prop的值时，这个变化也会同步到父组件中所绑定的值。 (注意此处在 2.3.0版本以后)

```
<comp :foo.sync="bar"></comp>
<comp :foo="bar" @update:foo="val => bar = val"></comp>
更新事件 this.$emit('update:foo', newValue)

```

### 表单组件数据双向绑定
> 自定义事件可以用来创建自定义的表单输入组件，使用 v-model 来进行数据双向绑定。


```
<input v-model="something">

(2.2.0版本 )
<my-checkbox v-model="foo" value="some value"></my-checkbox>


Vue.component('my-checkbox', {
  model: {
    prop: 'checked',
    event: 'change'
  },
  props: {
    checked: Boolean,
    value: String
  },

})

等价形式
<my-checkbox
  :checked="foo"
  @change="val => { foo = val }"
  value="some value">
</my-checkbox>

```

v-model
