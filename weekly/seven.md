# 金融壹账通前端H5技术周报(第七期)
> **本期导读**: 原创专题带来掌雄在微信小程序中的canvas绘图实践，和昱宏对three.js事件绑定的封装，以及我对redux的一小段源码解析。语言基础中的函数式编程部分似乎并没有那么基础，fetch能不能取代XMLHttpRequest也是一个值得思考的问题。工具框架篇带来virtual-dom的“拆盒”实践、饿了么在PWA上“尝鲜”实践和google的新型jpeg压缩算法。文末为近期开发的公司实习生招聘页，欢迎大家赏鉴分享

![](./images/seven/banner.jpeg)

## 原创专题
### 1）[微信小程序canvas手绘雷达图](http://www.jianshu.com/p/17eb83a04185)@吴掌雄
微信小程序已经发布了两个多月了，没有想象中那么火。但是一些拥有多用户量的APP应用也会抽出主业务流程做微信小程序版本。做过小程序开发的小伙伴们都知道微信小程序缺少类似echart.js的图形库，然而业内echart.js等主流的h5图形库并不能在小程序上运行，所以遇到绘制图形需求的时候我们只能用canvas绘画。本文为大家分享的是以自定义组件的形式绘制雷达图。
### 2）[由redux 异步数据流引发的血案](http://www.jianshu.com/p/a347c11417dc)@曾文富
redux是一个管理web应用数据状态（state）的javascript库，其使用单项数据流的模式试图让应用状态变得可控
### 3）[three.js事件绑定插件--onEvent](http://www.jianshu.com/p/61ba1906f9a7)
Three.js是构建web3d场景非常流行的框架，利用three.js我们可以更优雅地创建出三维场景和三维动画。最近在使用three.js开发Web3d的时候，想要给我的3d物体添加onclick事件，查遍了three的官方文档发现，three.js的mesh（3d网格）没有类似HTML里dom的addEventListener的绑定事件...

## 语言基础
### 1）[我眼中的 JavaScript 函数式编程](http://taobaofed.org/blog/2017/03/16/javascript-functional-programing/?hmsr=toutiao.io&utm_medium=toutiao.io&utm_source=toutiao.io)@化辰
JavaScript 函数式编程是一个存在了很久的话题，但似乎从 2016 年开始，它变得越来越火热。这可能是因为 ES6 语法对于函数式编程更为友好，也可能是因为诸如 RxJS (ReactiveX) 等函数式框架的流行
### 2）[fetch 没有你想象的那么美](https://undefinedblog.com/about/)@undefined
前端工程中发送 HTTP 请求从来都不是一件容易的事，前有骇人的 ActiveXObject，后有 API 设计十分别扭的 XMLHttpRequest，甚至这些原生 API 的用法至今仍是很多大公司前端校招的考点之一。
### 3）[CSS 自定义属性 — 基础篇](https://zhuanlan.zhihu.com/p/25714131)@kmokidd
这是 CSS 自定义属性系列文章的第一篇，在这篇文章中我将快速介绍什么是自定义属性以及它们的语法，并在后续文章中详尽地分析 CSS 自定义属性，各位可以持续关注。

## 工具框架
### 1）[对 virtual-dom 的一些理解](https://zhuanlan.zhihu.com/p/25630842)@喻争
Vue 2.x 、React 都引入了 Virtual Dom 的概念，来更加高效地更新 dom 节点，提升渲染性能。为了能更深入地了解 Virtual Dom 的相关细节，决定将 Matt-Esch/virtual-dom 作为学习对象。这个项目很纯粹，也很清晰地展示了如何利用虚拟节点来更新视图的整个过程
### 2）[PWA 在饿了么的实践经验](https://zhuanlan.zhihu.com/p/25800461)@王亦斯
PWA （ Progressive Web Apps，渐进式网页应用）是由谷歌提出的新一代 Web 应用概念，旨在提供可靠、快速、类似 Native 应用的服务方案。
### 3）[Google开源新算法，可将JPEG文件缩小35%](http://36kr.com/p/5067258.html?hmsr=toutiao.io&utm_medium=toutiao.io&utm_source=toutiao.io)@boxi
一图胜千言。Web与过去冷冰冰的互联网最大的区别就在于多了丰富的图片。而web上面最流行的静态图片格式非JPEG莫属。JPEG文件的多寡往往会影响页面的加载速度。为此，Google开发了一种新的JPEG算法，可将文件大小减少35%，这无疑会提高网站的加载性能；此外新算法还可以在保持大小不变的情况下显著改善图片质量。更重要的是，Google的这种JPEG格式跟WebP、WebM等图像压缩办法不同，它可以完全与现有的浏览器、设备、图片编辑应用以及JPEG标准兼容。而且，Google还把它给开源出来了。
### 4）[移动端H5图片压缩上传](https://github.com/CommanderXL/imgResize/blob/master/README.md?hmsr=toutiao.io&utm_medium=toutiao.io&utm_source=toutiao.io)@CommanderXL
利用FileReader,读取blob对象,或者是file对象，将图片转化为data uri的形式。
使用canvas,在页面上新建一个画布,利用canvas提供的API,将图片画入这个画布当中。
利用canvas.toDataURL()，进行图片的压缩，得到图片的data uri的值
上传文件。
## 前端视界
### 1）实习生招聘
![](./images/seven/qrcode.png)


