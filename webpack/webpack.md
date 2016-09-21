#webpack源码走读
1. webpack的核心是插件机制，使用Tapable实现
2. webpack和gulp的区别，gulp数据流串行结构，webpack在串行的主线程中有很多事件注册点，可以触发插件执行（Tapable）
3. webpack继承Tapable的方式，调用构造函数，复制原型，在原型链上并没有指向Tapble
```
    //调用Tapable的构造函数
    function Compiler() {
        Tapable.call(this);
        ...........
    }
    //复制Tapable的属性
    Compiler.prototype = Object.create(Tapable.prototype);
    Compiler.prototype.constructor = Compiler;
```
4. WebpackOptionsApply.js注入了所有用户插件，以及webpack内置插件，并且compiler的参数也是在webpack外部赋值，而不是传入赋值的。compiler内部的参数this.resolvers（解析器）也是在WebpackOptionsApply中注入的
```
    //其实不太习惯这种模式，compiler内部参数的赋值在外部设置而不是通过参数传入在内部设置
    compiler = new Compiler();
    compiler.options = options;
    compiler.options = new WebpackOptionsApply().process(options, compiler);

    //如果是我写，我宁愿
    compiler = new Compiler(options);
    function Compiler(options) {
        this.options = options;
    }
```
5. webpack事件点（可以通过监控Tapable方法，监听webpack注册的事件点）
`environment->after-environment->run->compile->make->after-compile`
6. compile.createChildCompiler可以创建一个子编译器，可以像父编译器一样有一整套的编译系统
7. normalModuleFactory:normalModule对象工厂，当调用它的create方法的时候，会依次触发，基于插件的模式真的很丧心病狂啊
 a. 触发factory，返回方法factory，构造normalModule对象
 b. factory方法触发resolver方法
 c. resolver触发after-resolver
 d. after-resolver创建module
    触发create-module 和 module
8. module是核心，normalModule继承自module，创建normalModule的时候，会调用NormalModuleMixin，NormalModuleMixin又会执行normalModule的fillLoaderContext方法：
`this.fillLoaderContext(loaderContext, options, moduleContext);`
这个方法是干嘛使的，用来填充loaderContext的，除了方法本身填充工作，它还触发normal-module-loader，让插件继续执行loaderContext的填充工作（终于明白extract-text-webpack-plugin是干什么的了）





