# webpack源码分析（一）— *Tapable插件架构*
> 在前面的文章[webpack不适合多页面应用？你写的插件还不够多](webpack-plugin.md)中提到过，webpack核心使用了Tapable实现事件的发布订阅处理的插件架构([Tapable中文文档](tapable.md))，今天就具体来分析下webpack基于Tapable的插件架构

## 找到代码入口
- 想必你已经使用过`npm install webpack`命令下载过webpack，那么在你的node_modules目录下找到webpack。
- npm模块的入口文件可以通过package.json中的`"main": "lib/webpack.js"`找到，当你通过reqire引用模块的时候，其实定位到的就是这个文件。一般情况下，我们会在命令行直接使用webpack命令去执行打包，这个时候执行的就是`bin/webpack.js`了，这个命令只是在调用`lib/webpack.js`之前处理一些命令行参数，殊途同归。
- 打开lib/webpack.js。webpack.js除了使用exportPlugins导出很多插件类（方便外部调用），最重要的事情就是创建compiler对象(如果options是数组的话，每个元素创建一个)
```
    //创建compiler对象
    compiler = new Compiler();
    //后面这几句代码，得看了compiler再回来看看了
    compiler.options = options;
    compiler.options = new WebpackOptionsApply().process(options, compiler);
    new NodeEnvironmentPlugin().apply(compiler);
    compiler.applyPlugins("environment");
    compiler.applyPlugins("after-environment");
```
这个时候我们的视线得转移到compiler上了

## 植入Tapable
打开lib/Compiler.js
```
    function Compiler() {

        //传入作用域，调用Tapable的构造函数
        Tapable.call(this);

        this.outputPath = "";
        this.outputFileSystem = null;
        this.inputFileSystem = null;

        this.recordsInputPath = null;
        this.recordsOutputPath = null;
        this.records = {};

        this.fileTimestamps = {};
        this.contextTimestamps = {};

        this.resolvers = {
            normal: new Resolver(null),
            loader: new Resolver(null),
            context: new Resolver(null)
        };
        this.parser = new Parser();

        this.options = {};
    }
    module.exports = Compiler;

    //复制一份Tapable的原型
    Compiler.prototype = Object.create(Tapable.prototype);
    Compiler.prototype.constructor = Compiler;
```
如果你阅读过[Tapable中文文档](tapable.md)，你应该对这个mix的方式不会陌生，tapable的原理其实也不复杂
> 声明一个全局的变量`this._plugins = {}`，插件中使用`plugin(name, fn)`方法给事件`name`注册处理方法`fn`，多次注册形成了事件`name`的监听链，当事件`name`触发的时候，执行这些处理方法。处理方法的执行顺序和执行方式依据事件`name`的触发方式的不同而不同

这个时候compiler已经具备Tapable的所有属性和方法了，我们再回到lib/webpack.js来看看创建了Compiler对象后的几行代码
>说实话不太欣赏这种在对象外面初始化的设计模式，读代码的时候你得跳来跳去，我更倾向于通过构造函数传入options，在对象内进行初始化工作。（仅代表个人的想法）

```
    //给对象参数赋值
    compiler.options = options;
    //传入options和compiler执行WebpackOptionsApply的process想法
    //这个方法对参数进行了处理，并且注入了大量的插件
    compiler.options = new WebpackOptionsApply().process(options, compiler);
    //注册nodeEveironmentPlugin插件
    new NodeEnvironmentPlugin().apply(compiler);
    //触发environment和after-environment事件
    compiler.applyPlugins("environment");
    compiler.applyPlugins("after-environment");
```

webpack很多核心功能本身就是以插件的形式开发的，打开lib/WebpackOptionsApply就会发现，在这个方法中，除了处理参数，就是把一个个插件注册到compiler中

`compiler.applyPlugins("environment")`以一种最简单的并行处理的方式去去触发事件`environment事件`，所有注册的处理方法并行执行，相互独立互不干扰，并且不需要给处理方法传入参数。

而有些事件的触发方式要复杂一些，例如complier触发`emit`的方式
```
    this.applyPluginsAsync("emit", compilation, function(err) {
        if(err) return callback(err);
        outputPath = compilation.getPath(this.outputPath);
        this.outputFileSystem.mkdirp(outputPath, emitFiles.bind(this));
    }.bind(this));
```
这段代码：
触发事件`emit`，传入参数compilation对象，串行的调用注册在事件`emit`上的处理函数（先入先出），倘若某一个处理函数报错，则执行传入的`function(err)`，后续的处理函数将不被执行，否则最后一个处理函数调用`function()`。插件注册此类事件，处理函数需要调用callback，这样才能保证监听链的正确执行。所以为了在写自定义插件的时候能正确的监听事件，非常有必要仔细读[Tapable中文文档](tapable.md)（虽然本文已经多次提到这个文档，但是还是有必要再进行一次提醒）

**webpack中另外一个重要的对象compilation使用了同样的方式植入了tapable**

## 总结
咱们分析webpack源码主要有两个原因：一是为了学习优秀的代码的设计方法，二是为了编写webpack自定义插件的时候能够游刃有余。不管从哪一点来说，Tapable面向切面的插件思想，都是值得我们琢磨的（在我的一个项目中还真的从webpack把Tapable借鉴过来了）

