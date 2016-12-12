# 立即执行函数形成的闭包
> 闭包是js中比较难以理解的概念，今天在敲立即执行函数的时候突然有感，稍作分析，聊表心意

## 闭包的概念简记
[阮一峰的一篇文章](http://www.ruanyifeng.com/blog/2009/08/learning_javascript_closures.html)讲到了一种很浅显易懂的理解：

> 闭包就是能够读取其他函数内部变量的函数

例如：
```
    function f1(){
　　　　var n=999;
　　　　function f2(){
　　　　　　alert(n);
　　　　}
　　　　return f2;
　　}
    
   n; //undefined
   var result = f1();
   result();//999
```

**当然这种说法必要但是不充分**，因为这种说法没有包括这样一种情况（作用域内）
```
    var obj = {
        a: 'a',
        showA: function() {
            console.log(this.a);
        }
    }

    obj.showA(); //'a'
```
所以更为确切的理解我觉得是：
> 闭包就是能够读取其他**作用域**内部变量的函数

## 立即执行函数内部形成的闭包
```
    (function(global) {
        var defaultOpts = {
            a: 'abc'
        };

        function Test() {
            this.options = defaultOpts;
        };

        Test.prototype = {
            showA: function() {
                console.log(this.options.a);
            }
        };

        global.Test = Test;

    })(this);

    defaultOpts; //undefined
    new Test().showA();//abc
```

defaultOpts作为立即执行函数中的局部变量，在外部直接访问是访问不到的，然而它并没有在立即执行函数执行完成之后就消失，因为它在全局函数Test中被使用到了，**它其实已经常驻内存了**

so，遇到这样的情况不要疑惑，因为这已经形成闭包了

## After
coding过程中突然的自我~~
继续搬砖去了


