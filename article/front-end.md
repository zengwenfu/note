# 前端教练第一个两周计划
> **学习方式：**采取一对一教练的方式，教练负责提供针对性学习线路、发布学习任务（学习资源、作业）、检查学习状况、问题解答     

> **提问：**在小密圈“菲麦前端”上提问，为了提高提问质量，采取付费提问的方式（象征性的给一元提问费），所以一定要勤于思考，培养独立寻求问题解决方案的能力

> **输出：**作业实例、总结文章（写得好将会发布到菲麦前端微信公众号中）

> **答谢：**每一次两周的学习周期、找到工作，学员自行给教练发红包答谢，教练的付出也是应该得到一些正向反馈

## 一、CSS
### 布局(3天)
**学习资源：**     
1）[史上最全Html和CSS布局技巧](http://www.imooc.com/article/2235)       
2）[Flex 布局教程：语法篇](http://www.ruanyifeng.com/blog/2015/07/flex-grammar.html)    
3）[Flex 布局教程：实例篇](http://www.ruanyifeng.com/blog/2015/07/flex-examples.html)      
**作业：**          
1）使用flex布局这个网页：[菲麦首页](https://modao.cc/app/RUS5BBushucfHuXd9hqoIuyVwVXxr7O)     
2）在简书上发表一篇flex布局学习笔记

### 适配（3天）
1) 等比适配：flexible、[viewport](http://www.jianshu.com/p/b880b48fa028)     
2) 流式布局      
3) 响应式布局        
**作业：**   
1）使用flexible的方式制作移动端网页（等比适配各种机型）：[菲麦场景](http://h5.facemagic888.com/projects/58a02fbba5e0731851b677a4/view.html)     
2）在简书上发表一篇文章，适配采坑日记

### 转换、过渡、动画（3天）
```
    /******************2D转换******************************/
    //位置移动 translateX translateY
    .item {
        transform: translate(50px, 100px);
        -ms-transform: translate(50px, 100px);
        -webkit-transform: translate(50px, 100px);
        -o-transform: translate(50px, 100px);
        -moz-transform: translate(50px, 100px);
    }
    //旋转 顺时针 
    .item {
        transform: rotate(30deg);
    }
    //缩放 scaleX scaleY
    .item {
        transform: scale(2, 4);
    }
    //旋转 根据x轴y轴 skewX skewY
    .item {
        transform: skew(30deg, 30deg);
    }
    // 合集
    .item {
        transform: matrix(0.866,0.5,-0.5,0.866,0,0)
    }

    /*********************3D转换********************************/
    //位移 translateZ
    .item {
        transform: translate3d(30px, 50px, 100px)
    }
    //scale3d scaleZ, rotate3d rotateX rotateY rotateZ, perspective

    /**********************过渡***********************************/
    .item {
        transition: width 2s;
        -moz-transition: width 2s;  /* Firefox 4 */
        -webkit-transition: width 2s;   /* Safari 和 Chrome */
        -o-transition: width 2s;    /* Opera */
    }

    .item:hover {
        width:300px;
    }
```
### [设计模式](http://div.io/topic/1806)(1天)