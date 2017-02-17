# 移动端开发速成知识体系

## 一、基础知识
1. 移动端等比适配方案：
    a) [viewport方式](http://www.jianshu.com/p/b880b48fa028): 最为简单，低端机有兼容性风险
    b) [Flexible](https://github.com/amfe/article/issues/17): 来自阿里，rem这个单位要重点读
2. 布局：flex
3. 事件：
    a) 手势事件:touchstart, touchmove, touchend, touchcancel
    b) 触摸事件:gesturestart, gesturechange, gestureend
    c) 屏幕事件:onorientationchange
    d) 常见问题：点击延迟、点击穿透
4. css3动画
5. 性能优化：[前端性能优化的三个维度](http://www.jianshu.com/p/a5d9938ed60f)
6. es6语法
7. 混合编程：[Native App、Web App与Hybrid App的比较](http://www.jianshu.com/p/cf956e7f2054)

## 二、前端工程化
1. 模块化思想：
    a) [Javascript模块化编程-阮一峰系列](http://www.ruanyifeng.com/blog/2012/10/javascript_module.html)
    b) AMD、CMD思想
    c) webpack
2. 打包工具，gulp、webpack(node要有基本的了解)
3. css中间语言：less、sass
4. view层（mvc、mvvm框架，任选其一，触类旁通，首推react）：react、vue、angular
5. node express/aop框架（前后端同构，接口合并，服务器端渲染）
