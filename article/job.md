# 前端面试概要
## CSS
### 布局
> 参考网址：    
> [史上最全Html和CSS布局技巧](http://www.imooc.com/article/2235)     
> [Flex 布局教程：语法篇](http://www.ruanyifeng.com/blog/2015/07/flex-grammar.html)     
> [Flex 布局教程：实例篇](http://www.ruanyifeng.com/blog/2015/07/flex-examples.html)

**1）居中：**
```
    /**************水平居中****************/

    //已知宽度 margin:auto
    .child {
        width: 200px;
        margin: 0 auto;
    }

    //使用inline-block 和 text-align
    .parent {
        text-align: center;
    }
    .child {
        display: inlick-block;
    }

    /****************垂直居中**********************/

    //vertical-align:table-cell
    .parent {
        display: table-cell;
        vertical-align: middle;
        height: 200px;
    }

    //vertical-align: inline-block
    .parent {
        display: inline-block;
        vertical-align: middle;
        line-height: 20px;
    }

    /******************水平垂直居中*******************/

    // vertical-align, text-align, inline-block
    .parent {
        display: table-cell;
        vertical-align: middle;
        text-align: center;
    }
    .child {
        display: inline-block;
    }

    // 绝对定位：已知自身高宽
    .child {
        position: absolute;
        top: 50%;
        left: 50%;
        width: 100px;
        height: 100px;
        margin-left: -50px;
        margin-top: -50px;
    }

    // 绝对定位：未知自身高宽（需要浏览器支持transform）
    .child {
        position: absolute;
        top: 50%;
        left: 50%;
        transform: translate(-50%, -50%);
    }

    //flex 以下详细说

```
**2）多列布局：**
```
    //定宽+自适应 float + margin
    .parent{
        background:red;
        height:100px;
        margin:0 auto;
    } 
    .left{
        background:green;
        margin-right:-100px;
        width:100%;
        float:left;
    } 
    .right{
        float:right;
        width:100px;
        background:blue;
    }
```
**3) flex布局：**
```
    // 容器
    .box {
        display: -webkit-flex;
        display: flex；
        flex-direction: row;// row|row-reverse|column|column-reverse
        flex-wrap: nowrap;//nowrap|wrap|wrap-reverse
        //flex-flow: row wrap; //上面两个属性的合集
        justify-content: center;//主轴：flex-start|flex-end|center|space-between|space-round
        align-items: center; //交叉轴//flex-start|flex-end|center|baseline|stretch;
        align-content: center; 有多轴时候（wrap）
    }

    //项目
    .item {
        order: 1;
        flex-grow: 0; //默认0
        flex-shrink: 1; //默认1
        flex-basis: auto;//默认auto
        align-self: auto;//默认继承父元素align-items
    }
```

### 适配
**1) 等比适配：**flexible、[viewport](http://www.jianshu.com/p/b880b48fa028)      
**2) 流式布局**      
**3) 响应式布局**      
### 转换、过渡、[动画](http://www.zhangxinxu.com/wordpress/2012/09/css3-3d-transform-perspective-animate-transition/)
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
### [css设计模式](http://div.io/topic/1806)
## JS
### BOM、DOM
> BOM浏览器扩展的js接口  
> DOM网页文档接口

**BOM**   
1) 弹出新的浏览器窗口      
2) 移动、关闭浏览器窗口以及调整调整窗口大小       
3) 提供用户屏幕分辨率详细信息的屏幕对象      
4) 对cookie的支持    
5) IE扩展了BOM，加入ActiveXObject
```
    window.frames
    window.history
    window.location
    window.navigator
    window.screen
```
**BOM、DOM图示意**      
![](http://www.dreamdu.com/images/browser_objects.png)

### 原生ajax
```
    function Ajax(type, url, data, success, failed) {
        //创建ajax对象
        var xhr = null;
        if(window.XMLHttpRequest) {
            xhr = new XMLHttpRequest();
        } else {
            xhr = new ActiveXObject('Microsoft.XMLHTTP');
        }

        var type = type.toUpperCase();
        // 用于清除缓存
        var random = Math.random();

        if(typeof data == 'object'){
            var arr = [];
            for(var key in data){
                arr.push(key + '=' + data[key]);
            }
            data = arr.join('&');
        }

        xhr.onreadystatechange = function() {
            if(xhr.readystate === 4) {
                if(xhr.status >= 200 && xhr.status < 300) {
                    success && success(xhr.responseText, xhr.responseXML);
                } else {
                    failed && failed();
                }
            }
        }
    }
```

### cookie
```
   //设置cookie
　　document.cookie = "name=value;expires=date"
   
   //读取cookie
   document.cookie;
```

### js内置对象
> [javascript中字符串常用操作总结](http://riny.net/2012/the-summary-of-javascript-string/)    
> [JavaScript 数组常用方法介绍](http://www.imooc.com/article/3609)    
> [Javascript Math对象和Date对象常用方法详解](https://segmentfault.com/a/1190000006043519)
![](http://upload-images.jianshu.io/upload_images/2954145-0f44952642feefbd.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

**1) String:**
```
    var str = 'abcdefg';

    // charAt charCodeAt
    console.log(str.charAt(2)); //返回C
    console.log(str.charCodeAt(0));//返回97

    // indexOf
    console.log(str.indexOf('a')); //返回0

    // substring(start, end); 返回start到end-1 
    // slice(start, end); 跟substring类似，参数可以是负值
    // substr(start, length);
    console.log(str.substring(1, 4));    //返回bcd
    console.log(str.substr(1, 3))    //返回bcd
    console.log(str.slice(1, -1));    //返回bcdef
    
    // replace split toLowerCase toUpperCase

```

**2）Math:**
```
    // Math.floor：向下取整
    // Math.ceil：向上取整
    // Math.round：四舍五入
    Math.floor(1.6); //1
    Math.ceil(1.4); //2
    Math.round(1.6); //2
    Math.round(1.4); //1
```

### 事件
**1) eventUtil:**
```
    var EventUtil={

       addHandler:function(element,type,handler){ //添加事件
          if(element.addEventListener){ 
             element.addEventListener(type,handler,false);  //使用DOM2级方法添加事件
          }else if(element.attachEvent){                    //使用IE方法添加事件
             element.attachEvent("on"+type,handler);
          }else{
             element["on"+type]=handler;          //使用DOM0级方法添加事件
          }
       },  

       removeHandler:function(element,type,handler){  //取消事件
          if(element.removeEventListener){
             element.removeEventListener(type,handler,false);
          }else if(element.detachEvent){
             element.detachEvent("on"+type,handler);
          }else{
             element["on"+type]=null;
          }
       },

       getEvent:function(event){  //使用这个方法跨浏览器取得event对象
          return event?event:window.event;
       },
        
       getTarget:function(event){  //返回事件的实际目标
          return event.target||event.srcElement;
       },
        
       preventDefault:function(event){   //阻止事件的默认行为
          if(event.preventDefault){
             event.preventDefault(); 
          }else{
             event.returnValue=false;
          }
       },

       stopPropagation:function(event){  //立即停止事件在DOM中的传播
                                         //避免触发注册在document.body上面的事件处理程序
          if(event.stopPropagation){
             event.stopPropagation();
          }else{
             event.cancelBubble=true;
          }
       },
            
       getRelatedTarget:function(event){  //获取mouseover和mouseout相关元素
          if(event.relatedTarget){
             return event.relatedTarget;
          }else if(event.toElement){      //兼容IE8-
             return event.toElement;
          }else if(event.formElement){
             return event.formElement;
          }else{
             return null;
          }
       },
            
       getButton:function(event){    //获取mousedown或mouseup按下或释放的按钮是鼠标中的哪一个
          if(document.implementation.hasFeature("MouseEvents","2.0")){
             return event.button;
          }else{
             switch(event.button){   //将IE模型下的button属性映射为DOM模型下的button属性
                case 0:
                case 1:
                case 3:
                case 5:
                case 7:
                   return 0;  //按下的是鼠标主按钮（一般是左键）
                case 2:
                case 6:
                   return 2;  //按下的是中间的鼠标按钮
                case 4:
                   return 1;  //鼠标次按钮（一般是右键）
             }
          }
       },
            
       getWheelDelta:function(event){ //获取表示鼠标滚轮滚动方向的数值
          if(event.wheelDelta){
             return event.wheelDelta;
          }else{
             return -event.detail*40;
          }
       },
            
       getCharCode:function(event){   //以跨浏览器取得相同的字符编码，需在keypress事件中使用
          if(typeof event.charCode=="number"){
             return event.charCode;
          }else{
             return event.keyCode;
          }
       }
            
    };
```
**2) 跨浏览器DOMContentLoaded**
> [从onload和DOMContentLoaded谈起](http://www.cnblogs.com/hh54188/archive/2013/03/01/2939426.html)

```
    jQuery.ready.promise = function( obj ) {
        if ( !readyList ) {

            readyList = jQuery.Deferred();

            // Catch cases where $(document).ready() is called after the browser event has already occurred.
            // we once tried to use readyState "interactive" here, but it caused issues like the one
            // discovered by ChrisS here: http://bugs.jquery.com/ticket/12282#comment:15
            if ( document.readyState === "complete" ) {
                // Handle it asynchronously to allow scripts the opportunity to delay ready
                setTimeout( jQuery.ready );

            // Standards-based browsers support DOMContentLoaded
            } else if ( document.addEventListener ) {
                // Use the handy event callback
                document.addEventListener( "DOMContentLoaded", DOMContentLoaded, false );

                // A fallback to window.onload, that will always work
                window.addEventListener( "load", jQuery.ready, false );

            // If IE event model is used
            } else {
                // Ensure firing before onload, maybe late but safe also for iframes
                document.attachEvent( "onreadystatechange", DOMContentLoaded );

                // A fallback to window.onload, that will always work
                window.attachEvent( "onload", jQuery.ready );

                // If IE and not a frame
                // continually check to see if the document is ready
                var top = false;

                try {
                    top = window.frameElement == null && document.documentElement;
                } catch(e) {}

                if ( top && top.doScroll ) {
                    (function doScrollCheck() {
                        if ( !jQuery.isReady ) {

                            try {
                                // Use the trick by Diego Perini
                                // http://javascript.nwbox.com/IEContentLoaded/
                                top.doScroll("left");
                            } catch(e) {
                                return setTimeout( doScrollCheck, 50 );
                            }

                            // and execute any waiting functions
                            jQuery.ready();
                        }
                    })();
                }
            }
        }
        return readyList.promise( obj );
    };
```

### 面向对象
> [理解js面向对象的最佳姿势](http://www.jianshu.com/p/f68917175e2d)

### EventLoop
> [js运行机制深层剖析](http://www.jianshu.com/p/0983e69d58ec)

### 闭包

### 字符串编码
> [简单明了区分escape、encodeURI和encodeURIComponent](http://www.cnblogs.com/season-huang/p/3439277.html)

## HTTP2
> [HTTP,HTTP2.0,SPDY,HTTPS你应该知道的一些事](http://www.alloyteam.com/2016/07/httphttp2-0spdyhttps-reading-this-is-enough/)

1）新的二进制格式     
2）多路复用     
3）header压缩    
4）服务器端推送    

## 安全
### SQL注入攻击
> [如何从根本上防止 SQL 注入？](https://www.zhihu.com/question/22953267)

1）检查变量数据类型和格式
2）过滤特殊符号
```
  基本关键词： and、or、order
  增的关键词： insert、into
  删的关键词： delete
  改的关键词: replace、update
  查的关键词： union、select、
  文件处理的关键词： load_file、outfile

  引号使用 反斜杠转义
```
3）绑定变量使用预编译语句（例如使用query）(最佳方式)

### 跨站脚本攻击 - XSS
> [XSS攻击及防御](http://blog.csdn.net/ghsau/article/details/17027893)

1）不要在允许位置插入不可信数据        
2）html encode      

| 字符 | 编码字符 | 
| --- | --- | 
| less-than character (<) |   &lt; | 
| greater-than character (>) |  &gt; | 
| ampersand character (&) |  &amp; |
| double-quote character (") |  &quot; |
| space character( ) |  `&nbsp;` |
| Any ASCII code character whose code is greater-than or equal to 0x80 |  &#<number>, where <number> is the ASCII character value. |

### 跨站伪造请求攻击 - CSRF
> [CSRF 攻击的应对之道](https://www.ibm.com/developerworks/cn/web/1102_niugang_csrf/)

1) 验证 HTTP Referer 字段(低版本浏览器可能会被篡改，用户也可以通过浏览器设置不发送此字段)
2）token验证（通过native发请求，根据公钥生成token）(这个方法不错)
### 文件上传漏洞攻击
> [上传漏洞总结](http://byd.dropsec.xyz/2016/05/11/%E4%B8%8A%E4%BC%A0%E6%BC%8F%E6%B4%9E%E6%80%BB%E7%BB%93/)

### 分布式拒绝服务攻击 - DDOS
> [分布式拒绝服务攻击(DDoS)原理及防范](http://blog.jobbole.com/46846/)

**企业网管理员-主机设置：**   
1）关闭不必要的服务     
2）限制同时打开的Syn半连接数目     
3）缩短Syn半连接的time out时间    
4）及时更新系统补丁    
**企业网管理员-网络设备设置：**    
1）防火墙    
  a) 禁止对主机的非开放服务的访问    
  b) 限制同时打开的SYN最大连接数    
  c) 限定特定IP地址的访问    
  d) 启用防火墙的防DDos的属性    
  f) 严格限制对外开放服务器的向外访问（防止自己服务器被当做傀儡去害人）    
2）路由器       
  a) Cisco Express Forwarding（CEF）      
  b) 使用 unicast reverse-path    
  c) 访问控制列表（ACL）过滤         
  d) 设置SYN数据包流量速率     
  e) 升级版本过低的ISO     
  f) 为路由器建立log server    

### DNS劫持
> [浅谈dns劫持](http://www.9usb.net/201006/dns-jiechi.html)

1）使用安全可靠的DNS服务器管理自己的域名，并且注意跟进DNS的相关漏洞信息，更新最新补丁，加固服务器；       
2）保护自己的重要机密信息安全，避免域名管理权限被窃取；       
3）提高服务器安全级别，更新系统及第三方软件漏洞，避免遭受攻击；      
4）近期，企业和政府网站被挂马事件频繁，网管应及时监测并提高网页代码安全性；     
5）广大网民应尽快更新安全软件，以拦截各种网络攻击，避免成为僵尸网络成员。       

## ES6
> [前端开发者不得不知的ES6十大特性](http://www.alloyteam.com/2016/03/es6-front-end-developers-will-have-to-know-the-top-ten-properties/)

### Default Parameters(默认参数) in es6
```
//在es5中，我们不得不采取这种方式给参数设定默认值
//这原本也没什么问题，知道参数=0
var link = function (height, color, url) {
    var height = height || 50;
    var color = color || 'red';
    var url = url || 'http://azat.co';
    ...
}

// es6
var link = function(height = 50, color = 'red', url = 'http://azat.co') {
  ...
}
```
### Template Literals（模板对象） in ES6
```
  //es5 字符串拼接
  var name = 'Your name is ' + first + ' ' + last + '.';
  var url = 'http://localhost:3000/api/messages/' + id;

  //es6 模板字符串
  var name = `Your name is ${first} ${last}. `;
  var url = `http://localhost:3000/api/messages/${id}`;
```

### Multi-line Strings （多行字符串）in ES6
```
  //es5
  var roadPoem = 'Then took the other, as just as fair,nt'
    + 'And having perhaps the better claimnt'
    + 'Because it was grassy and wanted wear,nt'
    + 'Though as for that the passing therent'
    + 'Had worn them really about the same,nt';
  var fourAgreements = 'You have the right to be you.n
    You can only be you when you do your best.';

  //es6
  var roadPoem = `Then took the other, as just as fair,
    And having perhaps the better claim
    Because it was grassy and wanted wear,
    Though as for that the passing there
    Had worn them really about the same,`;
  var fourAgreements = `You have the right to be you.
    You can only be you when you do your best.`;
```
### Destructuring Assignment （解构赋值）in ES6
```
  //es5
  var data = $('body').data(), // data has properties house and mouse
   house = data.house,
   mouse = data.mouse;
  var jsonMiddleware = require('body-parser').jsonMiddleware ;
  var body = req.body, // body has username and password
       username = body.username,
       password = body.password;

  //es6
  var { house, mouse} = $('body').data(); // we'll get house and mouse variables
  var {jsonMiddleware} = require('body-parser');
  var {username, password} = req.body;

  var [col1, col2]  = $('.column'),
   [line1, line2, line3, , line5] = file.split('n'); 

```
### Arrow Functions in（箭头函数） ES6
### Promises in ES6
### Block-Scoped Constructs Let and Const（块作用域和构造let和const）
```
  //es5 没有块级作用域
  function calculateTotalAmount (vip) {
    var amount = 0;
    if (vip) {
      var amount = 1;
    }
    { // more crazy blocks!
      var amount = 100;
      {
        var amount = 1000;
      }
    }  
    return amount;
  }
  console.log(calculateTotalAmount(true));  //1000

  // es6 let 块级作用域  var函数作用域
  function calculateTotalAmount (vip) {
    var amount = 0; // probably should also be let, but you can mix var and let
    if (vip) {
      let amount = 1; // first amount is still 0
    } 
    { // more crazy blocks!
      let amount = 100; // first amount is still 0
      {
        let amount = 1000; // first amount is still 0
      }
    }  
    return amount;
  }
   
  console.log(calculateTotalAmount(true)); // 0
```
### Classes （类）in ES6
```
class baseModel {
  constructor(options, data) { // class constructor，node.js 5.6暂时不支持options = {}, data = []这样传参
    this.name = 'Base';
    this.url = 'http://azat.co/api';
    this.data = data;
    this.options = options;
   }
 
    getName() { // class method
        console.log(`Class name: ${this.name}`);
    }
}



class AccountModel extends baseModel {
    constructor(options, data) {
      super({private: true}, ['32113123123', '524214691']); //call the parent method with super
      this.name = 'Account Model';
      this.url +='/accounts/';
    }
}
```
### Modules （模块）in ES6
> [Node.js 常见面试题](http://www.liuzhixiang.com/2015/07/01/Node.js-Interview-Questions-and-Answers/)

## 算法

## node
> [Node.js 常见面试题](http://www.liuzhixiang.com/2015/07/01/Node.js-Interview-Questions-and-Answers/)

### 简述
1. 模块机制 commonjs
2. 异步I/O
3. 异步编程  eventLoop
4. 内存控制  新生代内存（一分为二，一半使用中，一半用于垃圾回收）、老生代内存 
5. buffer  v8堆外分配内存
6. 网络编程 
7. 进程 child_process
8. 测试
9. 调试 [node.js调试](http://www.cnblogs.com/dolphinX/p/3485345.html)
**原生控制台调试：**     
在语句面前增加debugger;
```
  var server=require('./server'),
  router=require('./router'),
  requestHandlers=require('./requestHandlers');
  debugger;
  var handle={};
  debugger;
  handle['/']=handle['/start']=requestHandlers.start;
  debugger;
  handle['/upload']=requestHandlers.upload;
  handle['/show']=requestHandlers.show;
  debugger;
  server.start(8080,router.route,handle);
```
启动服务时增加debug选项：
```
  node debug index.js
```
**使用node-inspector调试**

### 什么是 error-first callback ？
error-first callback 用来传递错误和数据。第一个参数永远是一个错误对象（error-object），回调函数必须检查它。余下的参数用不过来传递数据。
> 异步回调的编程方式，异步处理中的异常难以捕捉（try catch也捕捉不到），约定回调的第一个参数为错误对象，实为上策

### 如何避免回调函数嵌套？
模块化：将回调写成单独的函数
使用 Promises

### Node程序如何监听80端口？
在`*nix`中，监听80端口需要root权限，这不是一个好主意

你可以使Node监听1024以上的端口，然后在Node前面部署nginx反向代理

### 单元测试
> [Nodejs单元测试小结](https://segmentfault.com/a/1190000002921481) 

**TDD:**测试驱动开发    
**BDD:**行为驱动开发，有点像产品说明书了


## react
### 组件生命周期
**三个状态：**    
1. mounting 以插入真实dom
2. updating 正在被重新渲染
3. unmounting 已移出真实的dom
**生命周期方法：**
componentWillMount: 在渲染前调用（客户端和服务器端通用）      
componentDidMount: 在第一次渲染后调用(只客户端可用)     
componentWillReceiveProps: 组件接收到新的props     
shouldComponentUpdate: 是否需要更新组件 forceUpdate时该方法无用     
componentWillUpdate: 在组件接收到新的prop或者state时调用，初始化渲染不调用      
componentDidUpdate: 更新完成后调用     
componentWillUnmount: 在组件从dom移除的时候立刻被调用

## 性能优化
[前端性能优化的三个维度](http://www.jianshu.com/p/a5d9938ed60f)

## 前端工程化
1）开发规范    
2）模块化开发
3）组件化开发
4）组件仓库
5）性能优化
6）项目部署
7）开发流程

## 混合编程
[H5与Native交互之JSBridge技术](http://tech.youzan.com/jsbridge/)
## 兼容性问题
> [移动端web常见问题解决方案](https://segmentfault.com/a/1190000004263966)    
> [47种常见的浏览器兼容性问题大汇总](http://www.qdfuns.com/notes/18372/bf9885f9902262654cd4d12cd1b65a11.html)

## 项目中遇到的问题



