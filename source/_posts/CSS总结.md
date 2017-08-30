---
title: CSS总结
tags: ['HTML', 'CSS']
date: 2015-01-19 00:34:14
---

### 当margin的值为百分比形式时,为什么浏览器会根据父容器宽度得出计算值？

一个符合W3C标准的浏览器会根据父容器的宽度进行计算，但是这个仅限于书写模式为横向的时候。因为在横向排版时，宽度"有迹可循"，可以把浏览器宽度作为参考，但是高度是不固定的，所以margin百分比值在计算时会参考父容器的宽度。当书写模式改为纵向，其计算参考便会变为父容器的高度了。
>demo
http://dongtianee.sinaapp.com/demo6.html

```css
    /*修改书写模式*/
    .demo{
    -webkit-writing-mode: vertical-rl; /* for webkit */
    　　 writing-mode: tb-rl; /* for ie */       
    }
```

>结论：一个符合W3C标准的浏览器,当margin的值为百分比形式时,会根据书写的模式来判断根据高度还是宽度来计算 

### margin：auto为什么只能实现水平居中，不能垂直居中？
网页排版时，常规流的块级元素水平方向总是铺满浏览器窗口,垂直方向各块级元素按照先后顺序从上往下排列,当页面内容过多时网页会出现纵向滚动条，因此原理上纵向是可以无限扩展的,计算时找不到一个固定的参考值,所以纵向的auto无法生效。


margin:auto会受书写模式的影响。当书写模式为纵向时，margin：auto垂直方向是可以居中的。其实受到书写模式影响的属性除了这些外，还有margin折叠、padding百分比值的计算等。

### 清除浮动有N种方式，他们间有什么共同点吗？
所谓清除浮动，一般是为了解决子元素浮动导致父容器高度坍塌。
![image](https://note.youdao.com/yws/res/16190/WEBRESOURCE2f6b5ed67cbaf70627c7593ef3f3e48c)


### 一个position:fixed的元素相对于一个容器定位而非浏览器视口吗？

CSS实现了一个position:fixed的元素相对于一个容器定位

当一个元素应用了CSS3的transform属性后，它的后代元素的fixed都将失效。

### 怪异盒模型box-sizing？弹性盒模型|盒布局?

 在标准模式下的盒模型：盒子总宽度/高度=width/height+padding+border+margin
在怪异模式下的盒模型下，盒子的总宽度和高度是包含内边距padding和边框border宽度在内的，盒子总宽度/高度=width/height + margin = 内容区宽度/高度 + padding + border + margin;
box-sizing有两个值一个是content-box，另一个是border-box。
当设置为box-sizing:content-box时，将采用标准模式解析计算；
当设置为box-sizing:border-box时，将采用怪异模式解析计算。

### a点击出现框，解决方法:

```css
a,a:hover,a:active,a:visited,a:link,a:focus{ 
    -webkit-tap-highlight-color:rgba(0,0,0,0);
    -webkit-tap-highlight-color: transparent;
    outline:none;background: none;
    text-decoration: none;border:none;
    -webkit-appearance: none; 
}
 ```

### 图片和文字在同一行显示?

1、在css中给div添加上“vertical-align:middle”属性。 
2、分别把图片和文字放入不同的div中，然后用“margin”属性进行定位，就可以使他们显示在同一行。
3、把图片设置为背景图片。


### CSS实现面板的隐藏和显示的三种方式
第一种利用了label和checkbox，使控制方和被控制方不需要有特定的HTML结构关系，但是需要额外的HTML标签来支持。第二种方式利用了hover和子元素选择器，第三种方式利用了focus和兄弟元素选择器，后两种都受限于特定的HTML结构。三种方法都只使用CSS实现了面板的隐藏显示。
>demo  http://dongtianee.sinaapp.com/demo8.html

### CSS图标
 
>demo http://www.uiplayground.in/css3-icons/


### 针对IE6，7的hack

```html
<!DOCTYPE html>
<!--[if lt IE 7 ]><html class="ie6"><![endif]-->
<!--[if IE 7 ]><html class="ie7"><![endif]-->
<!--[if IE 8 ]><html class="ie8"><![endif]-->
<!--[if IE 9 ]><html class="ie9"><![endif]-->
<!--[if (gt IE 9)|!(IE)]><!--><html class="w3c"><!--<![endif]-->
<head>
```

```css
.ie7 #hd_usernav:before, .ie8 #hd_usernav:before {
display: none
}
.ie6 .skin_no #hd_nav li, .ie7 .skin_no #hd_nav li, .ie8 .skin_no #hd_nav li {
border-right-color: #c5c5c5
}
.ie6 .skin_no #hd_nav a, .ie7 .skin_no #hd_nav a, .ie8 .skin_no #hd_nav a {
color: #c5c5c5
}
```

### 行内级元素可以设置宽高吗？ 
有一些特殊的行内元素，比如img，input，select等等，是可以被设置宽高的。一个内容不受CSS视觉格式化模型控制，CSS渲染模型并不考虑对此内容的渲染，且元素本身一般拥有固有尺寸（宽度，高度，宽高比）的元素，被称之为置换元素。比如img是一个置换元素，当不对它设置宽高时，它会按照本身的宽高进行显示。


### CSS规则根据优先级生效，低优先级的规则会被浏览器忽略还是覆盖？

多个优先级的样式都会被渲染，只不过高优先级会覆盖住低优先级，元素呈现为高优先级的样式。
浏览器只会为生效的CSS规则中的图片资源发出http请求。

在现代浏览器中，一个页面从请求到呈现，大致需要经过解析-构建DOM树-构建呈现树（框架树）-布局（重排）-绘制等几个步骤。
浏览器计算完优先级后，只有后定义的背景图案规则被构建到呈现树上。接下来浏览器会进行重排和绘制，浏览器在绘制时才会请求背景图片规则用到的图片文件。这就是为什么只发出一个HTTP请求的原因。

### 使用margin可以做出圆角按钮的原理是什么？
当不能使用border-radius时,制造1px圆角的小技巧：button中嵌套span，设置span的margin为："margin:1px -1px"。
![image](http://mmbiz.qpic.cn/mmbiz_jpg/btsCOHx9LAMOgCIzMRn1Cw6qKicmGib8GmBBhiagZutJDPPuVJ2jJWO3KZanmcO9QMCcuZI4CiaqcsSZvUVnY18aGw/640?wx_fmt=jpeg&tp=webp&wxfrom=5&wx_lazy=1)

图中红色框为span标签，蓝色框为a标签。当设置span的左右margin为-1px时，其便会在左右各突出1px，造成一种1px圆角的视觉效果。同样的道理，在实现一些古老浏览器下的圆角与底色渐变的按钮时，通常也会利用到多层元素层叠制造视觉误差的原理。


### 常见兼容性问题？

1、png24位的图片在iE6浏览器上出现背景，解决方案是做成PNG8.也可以引用一段脚本处理。

2、浏览器默认的margin和padding不同。解决方案是加一个全局的*{margin:0;padding:0;}来统一。

3、IE6双边距bug:块属性标签float后，又有横行的margin情况下，在ie6显示margin比设置的大。

4、浮动ie产生的双倍距离（IE6双边距问题：在IE6下，如果对元素设置了浮动，同时又设置了margin-left或margin-right，margin值会加倍。） #box{ float:left; width:10px; margin:0 0 0 100px;} 这种情况之下IE会产生20px的距离，解决方案是在float的标签样式控制中加入 ——_display:inline;将其转化为行内属性。(_这个符号只有ie6会识别)

5、渐进识别的方式，从总体中逐渐排除局部。 首先，巧妙的使用“\9”这一标记，将IE游览器从所有情况中分离出来。 接着，再次使用“+”将IE8和IE7、IE6分离开来，这样IE8已经独立识别。 
css// .bb{ background-color:#f1ee18; .background-color:#00deff\9; +background-color:#a200ff; _background-color:#1e0bd1; } 

6、IE下,可以使用获取常规属性的方法来获取自定义属性, 也可以使用getAttribute()获取自定义属性; Firefox下,只能使用getAttribute()获取自定义属性. 解决方法:统一通过getAttribute()获取自定义属性。

7、IE下,event对象有x,y属性,但是没有pageX,pageY属性; Firefox下,event对象有pageX,pageY属性,但是没有x,y属性. * 解决方法：（条件注释）缺点是在IE浏览器下可能会增加额外的HTTP请求数。

8、Chrome 中文界面下默认会将小于 12px 的文本强制按照 12px 显示, 可通过加入 CSS 属性 -webkit-text-size-adjust: none; 解决。

9、超链接访问过后hover样式就不出现了 被点击访问过的超链接样式不在具有hover和active了解决方法是改变CSS属性的排列顺序: L-V-H-A : a:link {} a:visited {} a:hover {} a:active {}

10、上下margin重合问题
ie和ff都存在，相邻的两个div的margin-left和margin-right不会重合，但是margin-top和margin-bottom却会发生重合。
解决方法，养成良好的代码编写习惯，同时采用margin-top或者同时采用margin-bottom。

11、ie6对png图片格式支持不好(引用一段脚本处理)

### 怎样去掉选中时的虚线框？

利用onfocus="this.blur();"例如：

```html
<a href="#" onfocus="this.blur();">测试</a>
```

### 设置图片元素上下垂直居中

1、diaplay:table-cell（IE6\7不兼容）
2、position加margin（IE6不支持）
```css
.wrap .center {
    width: 100px;
    height: 100px;
    margin: auto;
    position: absolute;
    left: 0;
    right: 0;
    top: 0;
    bottom: 0;
}
```
3、position加transform （ie9以下不支持 transform，手机端表现的比较好）
```css
.wrap .center {
    position: absolute;
    top: 50%;
    left: 50%;
    transform: translate(-50%, -50%);
}
```
4、flex;align-items: center;justify-content: center（移动端首选）
```css
.wrap {
    display: flex;
    align-items: center;
    justify-content: center;
}
```
5、display:flex;margin:auto（移动端首选）
```css
.wrap {
    display: flex;
}
.wrap .center {
    margin: auto;
}
```
6、纯position（适用于所有浏览器）
```css
/* 方法一：*/
.wrap .center {
    position: absolute;
    width: 100px;
    height: 100px;
    left: 50px;/*left=(父元素的宽 - 子元素的宽 ) / 2 */
    top: 50px;/*top=(父元素的高 - 子元素的高 ) / 2 */
}
/* 方法二：*/
.wrap .center {
    background: green;
    position: absolute;
    width: 100px;
    height: 100px;
    left: 50%;/*left值固定为50% */
    top: 50%;/*top固定为50% */
    margin-left:-50px;/*-（子元素的宽/2） */
　  margin-top:-50px;/*-（子元素的高/2） */
}
```

### px/em/rem有什么区别？ 为什么通常给font-size 设置的字体为62.5%?

相对于当前对象内文本的字体尺寸。如当前对行内文本的字体尺寸未被人为设置，则相对于浏览器的默认字体尺寸。
1、em的值并不是固定的；
2、em会继承父级元素的字体大小。使用rem为元素设定字体大小时，仍然是相对大小，但相对的只是HTML根元素。这个单位可谓集相对大小和绝对大小的优点于一身，通过它既可以做到只修改根元素就成比例地调整所有字体大小，又可以避免字体大小逐层复合的连锁反应。
rem是相对于浏览器进行缩放的。1rem默认是16px，在响应式布局中，一个个除来转换成rem，太麻烦，所以重置rem
body{font-size=62.5% } 此时1rem = 10px;若是12px则是1.2rem。

### CSS3有哪些新特性？

1、边框：border-radius、box-shadow、border-image
2、背景：background-size、background-origin
3、文本效果：text-shadow、word-wrap
4、字体：@font-face规则
5、2D转换：translate()、rotate()、scale()、skew()、matrix()
6、3D转换：rotateX()、rotateY()
7、过渡：transition：transition-property transition-duration transition-timing-function transition-delay
8、动画：@keyframes规则
@keyframes myfirst {from{}to{}}//定义动画
div{animation: myfirst 5s linear 2s infinite alternate;}


### animation对应的属性

> 写法：animation: name duration timing-function delay iteration-count direction;

下面是对应的属性的介绍 
animation-name 规定需要绑定到选择器的 keyframe 名称。
animation-duration 规定完成动画所花费的时间，以秒或毫秒计。 
animation-timing-function 规定动画的速度曲线。 
animation-delay 规定在动画开始之前的延迟。 
animation-iteration-count 规定动画应该播放的次数。 
animation-direction 规定是否应该轮流反向播放动画。

### 伪类选择器和伪元素？CSS3中引入的伪类选择器有？CSS3中伪元素有?

伪类用一个冒号来表示，而伪元素则用两个冒号来表示。
**伪类选择器：**
由于状态是动态变化的，所以一个元素达到一个特定状态时，它可能得到一个伪类的样式；当状态改变时，它又会失去这个样式。
**伪元素选择器：**
并不是针对真正的元素使用的选择器，而是针对CSS中已经定义好的伪元素使用的选择器；
**CSS3中引入的伪类选择器：**
:root()选择器，根选择器，匹配元素E所在文档的根元素。在HTML文档中，根元素始终是<html>。:root选择器等同于<html>元素。

:not()选择器称为否定选择器，和jQuery中的:not选择器一模一样，可以选择除某个元素之外的所有元素。

:empty()选择器表示的就是空。用来选择没有任何内容的元素，这里没有内容指的是一点内容都没有，哪怕是一个空格。

:target()选择器来对页面某个target元素(该元素的id被当做页面中的超链接来使用)指定样式，该样式只在用户点击了页面中的超链接，并且跳转到target元素后起作用。

:first-child()选择器表示的是选择父元素的第一个子元素的元素E。简单点理解就是选择元素中的第一个子元素，记住是子元素，而不是后代元素。

:nth-child()选择某个元素的一个或多个特定的子元素。

:nth-last-child()从某父元素的最后一个子元素开始计算，来选择特定的元素

:nth-of-type(n)选择器和:nth-child(n)选择器非常类似，不同的是它只计算父元素中指定的某种类型的子元素。

:only-child表示的是一个元素是它的父元素的唯一一个子元素。

:first-line为某个元素的第一行文字使用样式。

:first-letter 为某个元素中的文字的首字母或第一个字使用样式。

:before 在某个元素之前插入一些内容。

:after 在某个元素之后插入一些内容。 

**CSS3中伪元素：**
> ::first-line选择元素的第一行，比如说改变每个段落的第一行文本的样式

> ::before和::after这两个主要用来给元素的前面或后面插入内容，这两个常用"content"配合使用，见过最多的就是清除浮动

> ::selection用来改变浏览网页选中文的默认效果

