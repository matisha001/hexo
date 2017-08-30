
---
title: vue1.x 与vue 2.x的区别
tags: ['javascript', 'vue','frame']
date: 2016-09-19 00:34:14
---

### vue1.x 与vue 2.x的生命周期区别

![image](http://note.youdao.com/yws/res/4079/9BA996B72E374A578B5F89B7A5C56049)

<!--more -->
---
### 数据绑定
> 在版本vue1.x中,prop默认是单向绑定：当父组件的属性变化时，将传导给子组件，但是反过来不会。这是为了防止子组件无意修改了父组件的状态——这会让应用的数据流难以理解。可以使用.sync 或 .once 绑定修饰符显式地强制双向或单次绑定。

```
  <!-- 默认为单向绑定 -->
  <child v-bind:my-message="parentMsg"></child>
  <!-- 双向绑定 -->
  <child v-bind:my-message.sync="parentMsg"></child>
  <!-- 单次绑定 -->
  <child v-bind:my-message.once="parentMsg"></child>
```


详细见[vue2.x事件与数据绑定](http://github.matisha.pw)

