# 金融壹账通前端H5技术周报(第三期)
> **本期导读**: 本期原创专题带来几个新同学的处女作，涵盖贝塞尔曲线的css3动画实现、原型链详解、混合编程的讨论以及ajax的底层实现。语言基础不再仅限于css和js，还带来了http协议层的讨论。工具框架中，红得发紫的webpack以及新贵vue占据了版面。最后，快过年了，来几个活跃气氛的场景动画，欢迎赏鉴

![](images/three/banner.jpeg)
## 原创专题
### 1) [贝赛尔曲线实现css3动画效果](http://www.jianshu.com/p/d7e3302c36e4)@林纯
贝塞尔曲线(Bézier curve)，又叫作贝兹曲线或贝济埃曲线，是应用于二维图形应用程序的数学曲线，该曲线分为一次/二次/三次/多次贝塞尔曲线
### 2) [关于原型和原型链的详细理解](http://www.jianshu.com/p/700a2a579351)@吴克炯
在浏览本文之前首先明白什么是对象？，在JavaScript中我们会用typeof( )这个函数，那么使用typeof( )输出的值一般会有number、boolean、string、undefined、function、object等这些类型，那我们本文要研究的就是object和function这两种类型，返回值是这两种类型的就是我们本文所要研究的对象
### 3) [Native App、Web App与Hybrid App的比较](http://www.jianshu.com/p/cf956e7f2054) @于小丽
“云”时代的来临正在改变App和运营团队之间的关系，一场不能避免的变革正在进行。鉴于移动终端的局限性，移动终端上的APP由本地化应用(Native App)，到基于WEB的应用（Web App），再到混合型应用（Hybrid App），这一连串的变化都源于技术的更新和市场的需要
### 4) [XMLHttpRequest简介](http://www.jianshu.com/p/61aa5d7b7248)@付美蓉
Ajax (Asynchronous Javascript And Xml )是指一种创建交互式网页应用的网页开发技术，其中，Ajax的核心是JavaScript对象XMLHttpRequest(以下简称XHR)，XHR是一种支持异步请求数据的技术，开发人员全面理解熟悉HTTP状态代码、就绪状态和 XHR 对象， 能够让 Ajax 执行得更好

## 语言基础
### 1) [你真的了解background-position](http://www.w3cplus.com/css/background-position-with-percent.html)@大漠
background属性是CSS中最常见的属性之一，它是一个简写属性，其包含background-color、background-image、background-repeat、background-attachment、background-position、background-clip、background-origin和background-size。你可能会说，这些属性再简单不过了，没有可讲的。这篇文章接下来要介绍的不是所有有关于background里面的属性，而是说说background-position属性。在详细介绍background-position之前，先要问大家，你真的了解这个属性吗？言外之意，接下来介绍是你所不了解的background-position相关细节。
### 2) [这样使用GPU动画](http://www.w3cplus.com/animation/gpu-animation-doing-it-right.html)@Bibi
大多数人知道现代网络浏览器使用GPU来渲染部分网页，特别是具有动画的部分。 例如，使用transform属性的CSS动画看起来比使用left和top属性的动画更平滑。 但是如果你问，“我如何从GPU获得平滑的动画？”在大多数情况下，你会听到像“使用transform:translateZ(0）或will-change:transform这样的建议
### 3) [transformjs污染了DOM?](http://www.alloyteam.com/2016/12/transformjs-polluting-the-dom/)@TAT.dnt
上星期在React微信群里，有小伙伴觉得transformjs直接给DOM添加属性太激进，不可取（由于不在那个微信群，不明白为什么React会谈到transformjs？！）。关于这点，其实在一年半前腾讯内部就有相关声音，腾讯内部的小伙伴建议，不要污染那么多吧~~，给个总的namespace
### 4) [HTTP,HTTP2.0,SPDY,HTTPS你应该知道的一些事](http://www.alloyteam.com/2016/07/httphttp2-0spdyhttps-reading-this-is-enough/)@TAT.tennylv
作为一个经常和web打交道的程序员，了解这些协议是必须的，本文就向大家介绍一下这些协议的区别和基本概念，文中可能不局限于前端知识，还包括一些运维，协议方面的知识，希望能给读者带来一些收获，如有不对之处还请指出。

## 工具框架
### 1) [webpack 构建性能优化策略小结](https://segmentfault.com/a/1190000007891318)@太空飛豬
技术的车轮还是要始终向前迈进，从中我们也不难发现，从前那种直接在js中写脚本。通过src嵌入到页面，然后按F5刷新页面查看结果的开发方式已经渐行渐远，基本上选择一款合适的编译和资源管理工具已经成为了所有前端工程中的标配，而在诸多的构建工具中，webpack以其丰富的功能和灵活的配置在整个2016年中大放光彩，React，Vue，angularjs2等诸多知名项目也都选用其作为官方构建工具，极受业内追捧，随者工程开发的复杂程度和代码规模不断地增加，webpack暴露出来的各种性能问题也愈发明显，极大的影响着开发过程中的体验。
### 2) [浅议技术债](http://www.zcfy.cc/article/we-need-to-talk-about-technical-debt-9670-24-ways-2097.html)@主小席（译）
有时候，不良代码就是不良代码，不要动辄就称技术债。开发人员明明是完成了低质量的工作，却非要冠以技术债的名义，实在是有粉饰能力不足的嫌疑。技术债是一个经常被误解的表述。错误地将那些老旧、维护困难甚至令人厌恶的代码与技术债混为一谈的话，是在刻意回避代码库的问题，而这些问题往往才是根源所在。是时候认真探讨一下技术债了。
### 3）[深入浅出 - vue之深入响应式原理](https://github.com/berwin/Blog/issues/11)@berwin
本文讲的内容是 vue 1.0 版本，同时为了阅读者的阅读心情，本文尽量做到不枯燥，特别适合那些想明白内部原理又讨厌看枯燥的源码的同学~
说到响应式原理其实就是双向绑定的实现，说到双向绑定，其实有两个操作，数据变化修改dom，input等文本框修改值的时候修改数据
### 4) [如何编写自己的 Native Bridge](http://efe.baidu.com/blog/how-to-create-you-own-native-bridge/)@leeight
和很多人一样，在我弄清楚 React Native 的实现机制之前，其实已经在实际项目中用过一段儿时间了。不过在我学习 React Native 实现机制的过程中，逐渐开始给这个项目贡献代码，最终成为核心开发者中的一员。

## 前端视界
> pc端查看可直接点击链接，手机端查看请识别二维码
### 1) [感恩节主题](http://dweb.pinganh5.com/show-h5.html?src=projects/586f1318314508da9a08ef40/view.html)@何文斌
![](images/three/gej.png)
### 2) [新年主题](http://dweb.pinganh5.com/show-h5.html?src=projects/586e323f314508da9a08ee9f/view.html)@林翔
![](images/three/xn.png)
### 3) [端午节主题](http://dweb.pinganh5.com/show-h5.html?src=projects/586cc32a0f81870687a5cd64/view.html)@何文斌
![](images/three/dwj.png)
