---
title: vue2过渡效果总结
tags: ['javascript', 'vue','frame']
date: 2016-09-25 00:34:14
---

## 单元素过渡

Vue 提供了 transition 的封装组件
- 条件渲染 （使用 v-if）
- 条件展示 （使用 v-show）
- 动态组件
- 组件根节点

当插入或删除包含在 transition 组件中的元素时，Vue 将会做以下处理：
  1. 自动嗅探目标元素是否有 CSS 过渡或动画，并在合适时添加/删除 CSS 类名。
  2. 如果过渡组件设置了过渡的 JavaScript 钩子函数，会在相应的阶段调用钩子函数。
  3. 如果没有找到 JavaScript 钩子并且也没有检测到 CSS 过渡/动画，DOM 操作（插入/删除）在下一帧中立即执行。

---
<!--more -->
### 过渡的-CSS-类名

会有 6 个(CSS)类名在 enter/leave 的过渡中切换
- v-enter: 定义进入过渡的开始状态。在元素被插入时生效，在下一个帧移除。
- v-enter-active: 定义过渡的状态。在元素整个过渡过程中作用，在元素被插入时生效，在 transition/animation 完成之后移除。 
- v-enter-to: 2.1.8版及以上 定义进入过渡的结束状态。在元素被插入一帧后生效（于此同时 v-enter 被删除），在 transition/animation 完成之后移除。
- v-leave: 定义离开过渡的开始状态。在离开过渡被触发时生效，在下一个帧移除。
- v-leave-active: 定义过渡的状态。在元素整个过渡过程中作用，在离开过渡被触发后立即生效，在 transition/animation 完成之后移除。 
- v-leave-to: 2.1.8版及以上 定义离开过渡的结束状态。在离开过渡被触发一帧后生效（于此同时 v-leave 被删除），在 transition/animation 完成之后移除。

![image](https://note.youdao.com/yws/res/16273/8F678DDC6FC049D590690F68619B8860) 

这些在 enter/leave 过渡中切换的类名，v- 是这些类名的前缀。使用 <transition name="my-transition"> 可以重置前缀，比如 v-enter 替换为 my-transition-enter。

![image](https://note.youdao.com/yws/res/5421/AA5F28067D684BBB98FE7A211AF86278)

---

### CSS 过渡与动画
- 主要是在css中使用transition,transform,animation,keyframes等css3属性。
- CSS 动画用法同 CSS 过渡，区别是在动画中 v-enter 类名在节点插入 DOM 后不会立即删除，而是在 animationend事件触发时删除。
 
![image](http://note.youdao.com/yws/res/5424/E0E04D2B1B444BBC9A9DDAD632A44F76)


---

### 自定义过渡类名
- 使用自定义过渡类名的特点就是优先级高于普通的类名,可以与第三方css动画库一起使用。

![image](http://note.youdao.com/yws/res/5427/ACF0A3EA7BE74C1B974DBDF0857D2DDF)


---

### 同时使用 Transitions 和 Animations
Vue 为了知道过渡的完成，必须设置相应的事件监听器。可以是 transitionend 或 animationend ，这取决于给元素应用的 CSS 规则。使用其中任何一种，Vue 能自动识别类型并设置监听。

同一个元素同时设置两种过渡动效，比如 animation很快的被触发并完成了，而transition 效果还没结束。在这种情况中，你就需要使用 type 特性并设置 animation 或 transition 来明确声明你需要 Vue 监听的类型。

---

### 过渡效果持续时间 （2.2.0版本 ）
- 一些嵌套的内部元素相比于过渡效果的根元素有延迟的或更长的过渡效果。在这种情况下你可以用 <transition> 组件上的 duration 属性定制一个显性的过渡效果持续时间 (以毫秒计)。

```
<transition :duration="{ enter: 500, leave: 800 }">...</transition>

```

---

### javascript实现过渡效果
- 当只用 JavaScript 过渡的时候， 在 enter 和 leave 中，回调函数 done 是必须的 。 否则，它们会被同步调用，过渡会立即完成。

- 使用 JavaScript 过渡的元素添加 v-bind:css="false"，Vue 会跳过 CSS 的检测。这也可以避免过渡过程中 CSS 的影响。

![image](http://note.youdao.com/yws/res/16375/WEBRESOURCE4a67d5cf26e2088e1358583f853f4f2c)

---

### 初始渲染过渡
> 可以通过 appear特性设置节点的在初始渲染的过渡。默认和进入和离开过渡一样，可以自定义 CSS 类名，也可以使用js钩子。


```
<transition
  appear
  appear-class="custom-appear-class"
  appear-to-class="custom-appear-to-class" (2.1.8+)
  appear-active-class="custom-appear-active-class"
  v-on:appear="customAppearHook"
  v-on:appear-cancelled="customAppearCancelledHook"
>
  <!-- ... -->
</transition>
```

---

## 多元素过渡


多个组件的过渡, 对于原生标签可以使用 v-if/v-else 。
当有相同标签名的元素切换时，需要通过 key 特性设置唯一的值来标记以让 Vue 区分它们，否则 Vue 为了效率只会替换相同标签内部的内容。
 
![image](http://note.youdao.com/yws/res/1255/EE6D30032C714B20A86B2F5E56551129)


```html
    <transition>
      <button v-bind:key="docState">
        {{ buttonMessage }}
      </button>
    </transition>
```

---

### 过渡模式

- 一个离开过渡的时候另一个开始进入过渡。这是 <transition> 的默认行为 - 进入和离开同时发生。



>同时生效的进入和离开的过渡不能满足所有要求，所以 Vue 提供了 过渡模式
- in-out: 新元素先进行过渡，完成之后当前元素过渡离开。
- out-in: 当前元素先进行过渡，完成之后新元素过渡进入。


```html
<transition name="fade" mode="out-in">
  <!-- ... the buttons ... -->
</transition>
```

---

## 多组件过渡


```
<div id="test">
    <transition name="component-fade" mode="out-in">
      <component v-bind:is="view"></component>
    </transition>
</div>
<script>
new Vue({
  el: '#test',
  data: {
    view: 'v-a'
  },
  components: {
    'v-a': {
      template: '<div>Component A</div>'
    },
    'v-b': {
      template: '<div>Component B</div>'
    }
  }
})
</script>
```

### 列表过渡

使用 <transition-group> 组件,同时渲染整个列表
- 不同于 <transition>,它会以一个真实元素呈现：默认为一个 <span>。也可以通过 tag 特性更换为其他元素。
- 内部元素 总是需要 提供唯一的 key 属性值




```html
<div id="list-demo" class="demo">
  <button v-on:click="add">Add</button>
  <button v-on:click="remove">Remove</button>
  <transition-group name="list" tag="p">
    <span v-for="item in items" v-bind:key="item" class="list-item">
      {{ item }}
    </span>
  </transition-group>
</div>
```

#### 列表位移过渡 
<transition-group>组件还有一个特殊之处。不仅可以进入和离开动画，还可以改变定位。要使用这个新功能只需了解新增的 v-move 特性，它会在元素的改变定位的过程中应用。像之前的类名一样，可以通过 name 属性来自定义前缀，也可以通过 move-class 属性手动设置。

 











