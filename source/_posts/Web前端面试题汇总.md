---
title: Web前端面试题汇总
tags: ['HTML', 'CSS', 'javascript']
date: 2014/7/13 20:46:25
---

### 如何理解HTML结构的语义化？

所谓标签语义化，就是指标签的含义。语义化的主要目的就是让大家直观的认识标签(markup)和属性(attribute)的用途和作用，对搜索引擎友好，有了良好的结构和语义我们的网页内容便自然容易被搜索引擎抓取，这种符合搜索引擎收索规则的做法，网站的推广便可以省下不少的功夫，而且可维护性更高，因为结构清晰,十分易于阅读。这也是搜索引擎优化SEO重要的一步。

<!-- more -->

### html5有哪些新特性?
 
1、绘画的 canvas 元素 
2、用于媒介回放的 video 和 audio 元素 
3、对本地离线存储的更好的支持 
4、新的特殊内容元素，比如：article、footer、header、nav、section 
5、新的表单控件，比如：calendar、date、time、email、url、search

### 移除了那些元素？

1、纯表现的元素：basefont，big，center，font, s，strike，tt，u； 
2、对可用性产生负面影响的元素：frame，frameset，noframes；

### 如何处理HTML5新标签的浏览器兼容问题？如何区分 HTML 和 HTML5？

IE8/IE7/IE6支持通过document.createElement方法产生的标签， 可以利用这一特性让这些浏览器支持HTML5新标签， 浏览器支持新标签后，还需要添加标签默认的样式： 
当然最好的方式是直接使用成熟的框架、使用最多的是html5shim框架
如何区分html和html5： 
DOCTYPE声明\新增的结构元素\功能元素

### 清除浮动有几种方式?将多个元素设置为同一行?

将多个元素设置为同一行：float，inline-block
清除浮动的方式：
1、父级div定义 height 
2、结尾处加空div标签 clear:both 
3、父级div定义 利用:after和:before来在元素内部插入两个元素块，从面达到清除浮动的效果：
```css
.clear{
    zoom:1;
}
.clear:after{
    content:””;
    clear:both;
    display:block;
    height:0;
    overflow:hidden;
    visibility:hidden;
}
```
4、父级div定义 overflow:hidden 
5、父级div定义 overflow:auto 
6、父级div 也一起浮动 
7、父级div定义 display:table

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

### 简述前端优化的方式

1、尽量减少HTTP请求次数
2、减少DNS查找次数
3、避免跳转
4、可缓存的AJAX
5、推迟加载内容
6、预加载
7、减少DOM元素数量
8、根据域名划分页面内容
9、使iframe的数量最小
10、不要出现404错误
11、使用内容分发网络
12、为文件头指定Expires或Cache-Control 
13、Gzip压缩文件内容
14、配置ETag
15、尽早刷新输出缓冲
16、使用GET来完成AJAX请求
17、把样式表置于顶部
18、避免使用CSS表达式（Expression）
19、使用外部JavaScript和CSS
20、削减JavaScript和CSS
21、用<link>代替@import
22、避免使用滤镜
23、把脚本置于页面底部
24、剔除重复脚本

### 你如何对网站的文件和资源进行优化？

> 文件合并
文件最小化/文件压缩
使用CDN托管
缓存的使用

### 为什么利用多个域名来提供网站资源会更有效？

1、CDN缓存更方便
2、突破浏览器并发限制（一般每个域名建立的链接不超过6个）
3、Cookieless，节省带宽，尤其是上行带宽一般比下行要慢
4、对于UGC的内容和主站隔离，防止不必要的安全问题(上传js窃取主站cookie之类的)。正是这个原因要求用户内容的域名必须不是自己主站的子域名，而是一个完全独立的第三方域名。
5、数据做了划分，甚至切到了不同的物理集群，通过子域名来分流比较省事。这个可能被用的不多。 
PS:关于Cookie的问题，带宽是次要的，安全隔离才是主要的。关于多域名，也不是越多越好，虽然服务器端可以做泛解释，浏览器做dns解释也是耗时间的，而且太多域名，如果要走https的话，还有要多买证书和部署的问题。

### 请说出三种减少页面加载时间的方法

1、优化图片
2、图像格式的选择（GIF：提供的颜色较少，可用在一些对颜色要求不高的地方）
3、优化CSS（压缩合并css，如margin-top,margin-left…)
4、网址后加斜杠（如www.campr.com/目录，会判断这个“目录是什么文件类型，或者是目录。）
5、标明高度和宽度（如果浏览器没有找到这两个参数，它需要一边下载图片一边计算大小，如果图片很多，浏览器需要不断地调整页面。这不但影响速度，也影响浏览体验。当浏览器知道了高度和宽度参数后，即使图片暂时无法显示，页面上也会腾出图片的空位，然后继续加载后面的内容。从而加载时间快了，浏览体验也更好了。）
6、减少http请求（合并文件，合并图片）。

### 解释下JavaScript中this是如何工作的

this永远指向函数运行时所在的对象，而不是函数被创建时所在的对象。匿名函数或不处于任何对象中的函数指向window 。

1、如果是call，apply,with，指定的this是谁，就是谁。
2、普通的函数调用，函数被谁调用，this就是谁。

### 解释下原型继承的原理

以下代码展示了JS引擎如何查找属性：

```js
function getProperty(obj,prop) {
    if (obj.hasOwnProperty(prop)) {
        return obj[prop];
    } else if (obj.__proto__!==null) {
        return getProperty(obj.__proto__,prop);
    } else {
        return undefined;
    }
}
```
![image](http://s10.sinaimg.cn/mw690/001Z3Vflgy71PuAfaMF39)

### 事件绑定与冒泡机制

### Ajax

> XMLHttpRequest对象

### Jsonp

### 一道js基础综合题

> 此题涉及的知识点众多，包括变量定义提升、this指针指向、运算符优先级、原型、继承、全局变量污染、对象属性及原型属性优先级等等。

```js
function Foo() {
    getName = function () { alert (1); };
    return this;
}
Foo.getName = function () { alert (2);};
Foo.prototype.getName = function () { alert (3);};
var getName = function () { alert (4);};
function getName() { alert (5);}

//请写出以下输出结果：
Foo.getName();//2
getName();//4
Foo().getName();//1
getName();//1
new Foo.getName();//2
new Foo().getName();//3
new new Foo().getName();//3
```
http://www.cnblogs.com/xxcanghai/p/5189353.html

### TCP三次握手和四次挥手

**三次握手：**
> 第一次握手：建立连接时，客户端A发生SYN包（SYN=j）到服务器B,并进入SYN_SEND状态，等待服务器B确认；
第二次握手：服务器B收到SYN包，必须确认客户A的SYN，ACK=j+1,同时自己也发送一个SYN包，SYN=k 即，SYN+ACK包，此时服务器进入SYN_RECV状态；
第三次握手：客户端A收到服务器B的SYN+ACK包,向服务器B发送确认包ACK(ACK=k+1),此包发送完毕，客户端A和服务器B进入ESTABLISHED状态，完成三次握手。

**四次挥手：**
> 客户端A发送一个FIN.用来关闭客户A到服务器B的数据传送(报文段4)；
服务器B收到这个FIN. 它发回一个ACK，确认序号为收到的序号+1（报文段5）。和SYN一样，一个FIN将占用一个序号；
服务器B关闭与客户端A的连接，发送一个FIN给客户端A（报文段6）；
客户端A发回ACK报文确认，并将确认序号设置为序号加1（报文段7）。

### 输入URL到展现页面的全过程

1、域名解析
2、建立TCP连接
3、发起HTTP请求
4、服务器响应HTTP请求
5、浏览器渲染页面

### Http协议