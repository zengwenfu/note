# 金融壹账通前端H5技术周报(第九期)
> **本期导读**: 本周大家都很忙，没有文章产出，只好拿自己的小程序登录态控制探索来充数了，希望对大家能有一些帮助。语言基础带来js中this、object的深入解读，另外你是否了解贝塞尔曲线呢？如果你觉得js很简单，那么来看看“谁说 JavaScript 很简单了？”这篇文章有没有你踩过的坑。工具框架带来了工具：github markdown规范，以及Tutorialzine悉心整理的15个js和css库，“基于Docker、NodeJs实现高可用的服务发现”则企图开启你的全栈之路。文末还是小鲜肉昱宏的VR demo，欢迎赏鉴

![](images/night/banner.jpeg)
## 原创专题
### 1) [小程序登录态控制探索全过程](http://mp.weixin.qq.com/s?__biz=MzA3MjU2MjUzNA==&mid=2647718902&idx=1&sn=b132525a3255c8ac845a95fea794edf3&chksm=873839ffb04fb0e9cc44ccc303f715acd45d4a217875d1570a155fa1ef92ad0f0f13ae11d69a&mpshare=1&scene=23&srcid=0414kvwlvqyKz69QRTiPFvaI#rd) @曾文富
最近微信小程序终于开放了个人注册，我当然不能浪费这个炫技的好机会，“菲麦日程”小程序正在全力推进中，尽请期待~~    
在登录态控制中，摸索尝试了小一阵子，特此分享

## 语言基础
### 1) [谁说 JavaScript 很简单了？](http://huziketang.com/blog/posts/detail?hmsr=toutiao.io&postId=58e06b98a58c240ae35bb8dd&utm_medium=toutiao.io&utm_source=toutiao.io) @胡子大哈
本文介绍了 JavaScript 初学者应该知道的一些技巧和陷阱。如果你是老司机，就当做回顾了，哪里有写的不好的地方欢迎指出。

### 2) [JavaScript深入之从ECMAScript规范解读this](https://github.com/mqyqingfeng/Blog/blob/master/JavaScript%E6%B7%B1%E5%85%A5%E4%B9%8B%E4%BB%8EECMAScript%E8%A7%84%E8%8C%83%E8%A7%A3%E8%AF%BBthis.md?hmsr=toutiao.io&utm_medium=toutiao.io&utm_source=toutiao.io) @mqyqingfeng
在《JavaScript深入之执行上下文栈》中讲到，当JavaScript代码执行一段可执行代码(executable code)时，会创建对应的执行上下文(execution context)。

### 3）[Canvas学习：贝塞尔曲线](http://www.w3cplus.com/canvas/drawing-curve.html)@大漠
在绘制圆和圆弧一节中，了解到在Canvas中可以使用arc()和arcTo()绘制制圆或弧线，但很多时候，仅这两个方法还不能满足我们实际的需求，特别是绘制复杂的曲线。不过值得庆幸的是，在Canvas中还提供了其他的方法可以帮助我们绘制复杂的曲线。那就是我们今天要说的贝塞尔曲线，在Canvas中提供了两个独立的方法：quadraticCurveTo()和bezierCurveTo()方法。这两个方法就是贝塞尔曲线。

### 4) [从Chrome源码看JS Object的实现](http://www.renfed.com/2017/04/04/chrome-object/)@会编程的银猪
Chrome自行开发了V8引擎，并被Node拿去当解析器。本文将通过V8的源码尝试分析Object的实现。



## 工具框架
### 1) [基于Docker、NodeJs实现高可用的服务发现](https://github.com/jasonGeng88/blog/blob/master/201704/service_discovery.md?hmsr=toutiao.io&utm_medium=toutiao.io&utm_source=toutiao.io) @jasonGeng88
关于服务发现的方式，主要分为两种方式：客户端发现与服务端发现。它们的主要区别为：前者是由调用者本身去调用服务，后者是将调用者请求统一指向类似服务网关的服务，由服务网关代为调用。

### 2) [15 个有趣的 JS 和 CSS 库](https://zhuanlan.zhihu.com/p/26317328?hmsr=toutiao.io&utm_medium=toutiao.io&utm_source=toutiao.io) @IT程序狮子烨
时光如白驹过隙， Tutorialzine 为我们带来了 2017 年 4 月份一些精心挑选的优秀 Web 开发资源。前端开发者们，让我们一起先睹为快吧！

### 3) [《GitHub 风格的 Markdown 正式规范》发布](https://linux.cn/article-8399-1.html?f=tt&hmsr=toutiao.io&utm_medium=toutiao.io&utm_source=toutiao.io) @GHLandy 
很庆幸，我们当初选择 Markdown 作为用户在 GitHub 上托管内容的标记语言，它为用户提供了强大且直接的方式 （不管是技术的还是非技术的） 来编写可以很好的渲染成 HTML 的纯文本文档。


## 前端视界
> pc端查看可直接点击链接，手机端查看请识别二维码
### 1) [web VR demo](https://yorkchan94.github.io/webvr-webpack2-boilerplate/dist/)@陈昱宏



