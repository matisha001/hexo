---
title: react基础学习
tags: ['javascript', 'react','frame']
date: 2016-09-29 00:34:14
---

### React 简介

#### 起源
React起源于Facebook的内部项目，该公司积极尝试引入HTML5技术用来架设Instagram网站，开发中发现HTML5的性能下降明显，达不到预期的效果。他们就自己开发了React框架。

<!-- more -->

#### 特点
**虚拟DOM:**  React也是以数据驱动的，每次数据变化React都会扫码整个虚拟DOM树，自动计算与上次虚拟DOM的差异变化，然后针对需要变化的部分进行实际的浏览器DOM更新。
**组件化:**  React可以从功能角度横向划分，将UI分解成不同组件，各组件都独立封装，整个UI是由一个个小组件构成的一个大组件，每个组件只关系自身的逻辑，彼此独立。
**单项数据流:** React设计者认为数据双向绑定虽然便捷，但在复杂场景下副作用也是很明显，所以React更倾向于单向的数据流动-从父节点传递到子节点。（使用ReactLink也可以实现双向绑定，但不建议使用）
### Hello world
#### 下载地址
ReactJS官方地址：https://facebook.github.io/react/

GitHub地址：https://github.com/facebook/react

引用react.js和react-dom.js（注意引用顺序）

**react.js：** 实现React核心逻辑，且于具体的渲染引擎无关，从而可以跨平台公用。如果应用要迁移到React Native，这一部分逻辑是不需要改变的。
**react-dom.js：**  包含了具体的DOM渲染更新逻辑，以及服务端渲染的逻辑，这部分就是与浏览器相关的部分了。
```js
<script src="./common/react.js"></script>
<script src="./common/react-dom.js"></script>
```

``` html
<div id="reactContainer"></div>
```

```js
<script>
    var HelloComponent = React.createClass({
        render:function() {
            return React.createElement('h1', null, 'Hello world');
        }
    });
    ReactDOM.render(
        React.createElement(HelloComponent, null),
        document.getElementById('reactContainer')
    );
</script>
```
#### React.createClass

