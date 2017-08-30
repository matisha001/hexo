---
title: vue-router2.x
tags: ['javascript', 'vue','vue-router','frame']
date: 2016-10-21 00:34:14
---

### 基本写法

在vue-router2.x中使用v-link 指令已经被 <router-link> 组件替代。



![image](http://note.youdao.com/yws/res/2946/C5AC7BFABBE54BEC9C6F9C1FD299422B)


当 <router-link> 对应的路由匹配成功，将自动设置 class 属性值 .router-link-active。


![image](http://note.youdao.com/yws/res/2965/6274DED77A5E4A038FA14442CE4C7CAC)



![image](http://note.youdao.com/yws/res/2968/B28F389F5C8E47DA894D78726D9FB3B5)

![image](http://note.youdao.com/yws/res/2970/A9FBED3A15764655951E550A4755FF6A)


![image](http://note.youdao.com/yws/res/2972/D6A0EBE67F0C44328387C55A40AF43E3)

### 动态路由的匹配

![image](http://note.youdao.com/yws/res/2977/1D37DB31749540C2B2E0398B33CF8364)


![image](http://note.youdao.com/yws/res/2982/F2F4A6F449824E4EBC7AD746C50349DB)

![image](http://note.youdao.com/yws/res/2981/85F978ED29E1434AB670111378ACC191)

### 嵌套路由
![image](http://note.youdao.com/yws/res/2985/B43AD070CBD649E28BA1BBB52C49FDCE)


![image](http://note.youdao.com/yws/res/2988/33729C1EBC4B4B54856938C0E3953557)

> 在vue-rouer0.7x中，子路由用subRoutes。


### 编程式的导航
 router.push(location)
 
 ![image](http://note.youdao.com/yws/res/2995/6083B85E020F48B68E8D64075C4ECCDC)
 
 
 
 ![image](http://note.youdao.com/yws/res/2997/A51384F60CBA4F91B5826F60C9C9A4B6)
 
 
 router.replace(location)
 
 ![image](http://note.youdao.com/yws/res/3002/1698F38B082A411B9297F1C1B8BFC4C7)
 
 
 ![image](http://note.youdao.com/yws/res/3004/895C265CDAA042839CD0AB8591AE57F1)
 
 
 ![image](http://note.youdao.com/yws/res/3008/C9C38B563407464FB7230D9871A595EB)
 
 
 
### 命名路由
![image](http://note.youdao.com/yws/res/3013/C8762E3BE8B14513ABB9EE2C0B3DC5FD)


![image](http://note.youdao.com/yws/res/3015/7165CFF4B76A44A8954CF6F3A3AED763)


![image](http://note.youdao.com/yws/res/3017/385294F604A744BF8FBC155EE9D97162)

### 命名视图

![image](http://note.youdao.com/yws/res/3022/5AA4BAB9EBD7420EB2FF7F43C82D66D2)


![image](http://note.youdao.com/yws/res/3024/0FA2DADB5C294E70A31DE5A657CC4874)


![image](http://note.youdao.com/yws/res/3026/F69A299302CC45A6A7833C2AFA8DF39C)


![image](http://note.youdao.com/yws/res/3028/5C6B8C56EA7645EEB582B3CBFC771F7C)

### 重定向和别名
![image](http://note.youdao.com/yws/res/3033/6780F81C4551452FB79B8EEB7492A0B5)

![image](http://note.youdao.com/yws/res/3035/6FA4FA88243A4F48B6CBAF7C20CE6E0C)


### HTML5 History 模式
![image](http://note.youdao.com/yws/res/3038/7E34CB88E6FE4E5581E6A5E3696F1629)


### 全局钩子
![image](http://note.youdao.com/yws/res/3041/B57C389FA54E4A079B44687AB544F49E)

### 某个路由独享的钩子

![image](http://note.youdao.com/yws/res/3044/E5E1D442454041DE811778D38CD9ACCF)


![image](http://note.youdao.com/yws/res/3046/21B3A8718F1542E58729C057D07C9C4B)


### 组件内的钩子
![image](http://note.youdao.com/yws/res/3051/E55E20AF7A1D40E6A002F48E2A1E97B3)

- 使用组件自身的生命周期钩子函数来替代activate 和 deactivate
- 在$router 上使用 watcher 来响应路由改变 (e.g. 比如基于新的路由参数获取数据)
- canActivate 可以被router 的配置中的 beforeEnter 中实现。
- canDeactivate 已经被 beforeRouteLeave 取代, 后者在一个组件的根级定义中指定。这个钩子函数在调用时是将组件的实例作为其上下文的。
- canReuse 已经被移除，因其容易混淆且很少被用到。


### 路由元信息 

![image](http://note.youdao.com/yws/res/3057/D342AD7A23E34711ACD7A559323FF0FB)

![image](http://note.youdao.com/yws/res/3059/D46D4D6FBFF74F4D83291CF7FD3ED97C)


### 过渡特效
![image](http://note.youdao.com/yws/res/3064/069ED312D7E24B16A13FE853DD21A40D)


![image](http://note.youdao.com/yws/res/3067/4E669B9DC36B4DE98812361799E1028F)



### 滚动行为
![image](http://note.youdao.com/yws/res/3071/94906A03CA0B475B848818139F2B4676)


![image](http://note.youdao.com/yws/res/3073/33CBC4A3E54F421FBE3D96612F58F996)


路由信息对象

![image](http://note.youdao.com/yws/res/3077/9BC1FECBB8AD42788E302776BF7328D7)

![image](http://note.youdao.com/yws/res/3079/CCC143565CF64714B159E43DE2BE15FB)

![image](http://note.youdao.com/yws/res/3081/5E64CA0F992D44348977E9EBB4E24960)


Router_构造配置
![image](http://note.youdao.com/yws/res/3085/A7A753BF820A4CDEB4888C9AC991B7AE)

![image](http://note.youdao.com/yws/res/3088/DECAA8A466754677B706DA23E1B710A4)

![image](http://note.youdao.com/yws/res/3090/CB92B55532014DFAB4746B7DD203C88C)

### Router_实例
![image](http://note.youdao.com/yws/res/3097/A734474E1E9D40C492CE9EB92BD84A7A)


### 对组件注入
![image](http://note.youdao.com/yws/res/3102/74F0496BBFF746DA9E226410E58A0F22)