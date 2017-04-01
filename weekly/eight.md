# 金融壹账通前端H5技术周报(第八期)
> **本期导读**: 原创专题带来昱宏给大家分享的如何发布一个node模块到npm，以及我对rem等比适配的总结。语言基础专题来聊一聊http、http2和https那些事，并带来css设计模式的探讨。工具框架层增加了vue的篇幅，这个框架实在增速凶猛；另外，WebAssembly的出现，web端说不定又要经历一场变革，此时不追更待何时。文末又是昱宏，炫酷的3d粒子效果，欢迎赏鉴。

![](images/eight/banner.jpeg)
## 原创专题
### 1) [node插件开发与发布](http://www.jianshu.com/p/7c29e3e933b0) @陈昱宏
本文主要给各位分享如何快速创建node插件并发布到npm上。
npm是一个让JavaScript程序员分享和复用代码的工具，我们不仅可以install别人的插件，也可以publish自己的代码。
### 2) [利用rem实现网页的等比适配](http://www.jianshu.com/p/064671df0454) @曾文富
之前说过使用viewport来实现等比适配的例子，本文来讲讲等比适配的另一种方式


## 语言基础
### 1) [HTTP,HTTP2.0,SPDY,HTTPS你应该知道的一些事](http://www.alloyteam.com/2016/07/httphttp2-0spdyhttps-reading-this-is-enough/) @TAT.tennylv
作为一个经常和web打交道的程序员，了解这些协议是必须的，本文就向大家介绍一下这些协议的区别和基本概念，文中可能不局限于前端知识，还包括一些运维，协议方面的知识，希望能给读者带来一些收获，如有不对之处还请指出。

### 2) [没那么难，谈CSS的设计模式](http://div.io/topic/1806) @灵感
曾有人调侃，设计模式是工程师用于跟别人显摆的，显得高大上；也曾有人这么说，不是设计模式没用，是你还没有到能懂它，会用它的时候。

### 3）[全面解读Math对象及位运算](http://louiszhai.github.io/2016/07/01/Math/?utm_source=75teamweekly&utm_medium=referral)@louis
Math方法和位运算几乎是被忽略得最严重的知识点, 和正则一样, 不用不知道, 一用到处查. 为了告别这种低效的编程模式, 我特地总结此篇, 系统梳理了这两个知识点. 以此为册, 助你攻破它们.



## 工具框架
### 1) [如何写一手漂亮的 Vue](http://jeffjade.com/2017/03/11/120-how-to-write-vue-better/?hmsr=toutiao.io&utm_medium=toutiao.io&utm_source=toutiao.io) @晚晴幽草轩轩主
欲先利其器，必先利其器，这是此博客一大倡导；关于如何优雅地去写好 Vue，工具自是首当其冲要提及的，毕竟这非常重要；在你选择使用 Vue 来从事前端开发的那一刻，你已经同意的这一论点：毕竟 Vue 也是用原生 Js 写的，Js 则是用 C 语言写，而 C 又是汇编写的….. 这不再是刀耕火种的年代，而你也未用汇编或 C 来解决你的需求，So，你是同意的。既是赞同的，岂有不用好它的道理？那么来一起探讨下

### 2) [WebAssembly 为什么比 asm.js 快？](http://huziketang.com/blog/posts/detail?postId=58ce80d2a6d8a07e449fdd28&utm_source=75teamweekly&utm_medium=referral) @胡子大哈
WebAssembly 是为 Web 而设计的、可以生成浏览器可执行的二进制文件的编程语言。并且于2017 年 2 月 28 日，四个主要的浏览器一致同意宣布 WebAssembly 的 MVP 版本已经完成，即将推出一个浏览器可以搭载的稳定版本。WebAssembly 的一个主要目标就是变快。本文将给出一些它如何变快的技术细节

### 3) [解析vue2.0的diff算法](https://github.com/aooy/blog/issues/2) @aooy 
外刊君还在考虑在公司内做一些Node.js的尝试，正要撸起袖子写几行代码，就被这个漏洞给吓尿了，【漏洞分析】vue2.0加入了virtual dom，有向react靠拢的意思。vue的diff位于patch.js文件中，我的一个小框架aoy也同样使用此算法，该算法来源于snabbdom，复杂度为O(n)。


## 前端视界
> pc端查看可直接点击链接，手机端查看请识别二维码
### 1) [穿越](http://www.pinganh5.com/showcase/58bfb8d6f5b629dc9d4b700d)@陈昱宏
![](images/eight/qrcode.png)



