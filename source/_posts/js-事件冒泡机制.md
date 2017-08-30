---
title: js-事件冒泡机制
tags: ['javascript']
date: 2016-03-19 00:34:14
---
## 应用场景
> 点击li弹出对应的innerHTML。

<!-- more -->
```html
    <ul id="ul">
       <li>item1</li>
       <li>item2</li>
       <li>item3</li>
       <li>item4</li>
       <li>item5</li>
   </ul>
```
当需要对很多元素添加事件的时，可以通过将事件添加到它们的父节点通过委托来触发处理函数。其中利用到了浏览器的事件冒泡机制。

jquery方案：
```javascript
    $("ul").on("click", function (e) {   
        console.log(e.target.innerHTML)
    })
```
javascript封装（参考）：
```javascript
    function bindEvent(el, ev, sel, fn){
        if(fn == null) {
            fn = sel;
            sel = null;
        }
        el.addEventListener(ev,function(e){
            var target;
            e.preventDefault();
            
            if(sel){
                target = e.target;
                if(target.matches(sel)){
                    fn.call(target, e)
                }
            }else{
                fn(e);
            }
        }) 
    }

    bindEvent('ul','click','li',function(e){
        console.log(this.innerHTML);
    })
```
## 补充

DOM2.0模型将事件处理流程分为三个阶段：事件捕获阶段、事件目标阶段、事件起泡阶段
    
**事件捕获**：当某个元素触发某个事件（如onclick），顶层对象document就会发出一个事件流，随着DOM树的节点向目标元素节点流去，直到到达事件真正发生的目标元素。在这个过程中，事件相应的监听函数是不会被触发的。

**事件目标**：当到达目标元素之后，执行目标元素该事件相应的处理函数。如果没有绑定监听函数，那就不执行。

**事件起泡**：从目标元素开始，往顶层元素传播。途中如果有节点绑定了相应的事件处理函数，这些函数都会被一次触发。如果想阻止事件起泡，可以使用e.stopPropagation()（Firefox）或者e.cancelBubble=true（IE）来组织事件的冒泡传播。

[2017前端面试题之Js篇（1）](http://www.jianshu.com/p/8e505fe77762)
