# 前端学习者需要有哪些装备
> 工欲善其事，必先利其器。前端的入门门槛可以说很低，任意的文本编辑器，加上每台计算机必备的浏览器就能将hello world跑起来，可以说零配置。但是为了能在后续的学习工作中无往而不利，还是建议初学者在一开始就把自己武装起来，扩大自己的格局

## 编辑器
很多同学喜欢使用webstorm，这是一个优秀的IDE，有很多语法提示，功能强大，但是不得不说，这是一种重武器，跑起来会比较耗内存，如果电脑不够强大，并且同时运行着很多其它软件（如PS），卡顿可能会变成见惯不怪的事情

相比之下sublime根本不能称之为IDE，它的轻便并不意味着功能不足，你可以使用它的插件系统，轻松的定制属于自己的开发工具，资源推荐：[如何优雅地使用Sublime Text3](http://www.jianshu.com/p/3cb5c6f2421c)
> 个人习惯使用sublime，该如何选择，还得看你的个人倾向

## 调试工具（chrome dev tools）
初学者一定要学会调试，遇到问题首先要尝试独立解决，提供自己解决问题的能力，这一点很重要，不要总等着别人喂饼，学习资源：[Google Chrome 浏览器 开发者工具 使用教程](http://devework.com/google-chrome-developer-tools-tutorial.html)

## 开通自己的博客账号
在学习的过程中，你需要踩很多坑，也会有不少收获，开通一个自己的博客账号，总结、沉淀、思考，不要认为自己能力尚浅，写博客总有班门弄斧之意，且不说你踩过的坑后来者也许同样会遇到，兴许正好就解决了别人的问题，至少对自己来说，能把知识通过自己语言、文字表达归纳，一定能掌握的更加深刻，就算一段时间之后忘记了，回头看看自己的笔记，就能轻易捡起来

无需搭建，有很多不错的社区可以注册自己的ID，这里推荐我自己在使用的[简书](http://www.jianshu.com/)

程序员的博客应该使用markdown语法，不要有负担，这对于程序员的你，实在是太简单了，学习资源：[ Markdown语法介绍](https://coding.net/help/doc/project/markdown.html)

如果编辑器你选择了sublime，那么就不用费心选择markdown编辑器了，安装两个插件即可：
- markdown editing（语法高亮）
- markdownPreview (浏览器预览)

## 使用github托管自己的代码
github是程序员的社交工具，初学者要养成代码版本管理的意识，github.io还支持发布静态页面，利于学习者将自己的学习成功在小伙伴之间“奔走相告”，这种炫耀“战利品”的行为，是一种正向反馈，这是艰苦的学习能够坚持下去的动力之一。
> 不瞒您说，如果github维护的好，对求职也是很有帮助的

首先你要对git有一定的了解，学习资源：[git-简易指南](http://www.bootcss.com/p/git-guide/)，要用起来，至少应该掌握如下几点：    
1. 仓库的概念（本地仓库、远程仓库）     
2. 分支的概念，创建分支、分支切换、分支合并等    
3. 克隆远程仓库到本地：git clone remote-url    
4. 更新代码：git pull    
5. 提交代码到本地：    
    a. 加入缓存区：git add fileName    
    b. 提交本地：git commit -m "注释信息"    
6. 提交到远程：git push   

然后你就可以在github上注册账号，建仓了：[用github来展示你的前端页面吧](http://www.cnblogs.com/luozhihao/p/6081842.html)

## node环境
你造么？     
前端已经从农耕时代，发展到工业时代了。    
也许现在你的工程只需要images、css、js和index.html，可是总有一天你的前端需要工程化，你需要使用webpack、sass/less、react/vue等等等，那时候node、npm/yarn将变得必不可少，所以我希望你能一开始把环境准备好    

node版本迭代太快，推荐使用nvm来对node进行安装、版本切换：[正确的安装和使用nvm(mac)](http://www.imooc.com/article/14617)

node默认使用npm来管理包，不过它有一些毛病，详情请见：[Yarn vs npm: 你需要知道的一切](http://web.jobbole.com/88459/)，推荐使用yarn:[安装](http://yarnpkg.top/Installation.html)

我在mac上安装的过程中，踩了一些坑，使用的：
```
    curl -o- -L https://yarnpkg.com/install.sh | bash
```
的方式安装，几分钟之后
```
    Yarn was installed, but doesn't seem to be working :(.
```
网上看了很多Issue都是说，需要降级安装，后面仔细看日志好像是.yarn目录内容创建失败，加上了一个sudo就好了，额，被系统权限坑了
```
    sudo curl -o- -L https://yarnpkg.com/install.sh | bash
```


然后再自己已有的项目中切换到yarn，运行`yarn install`
```
    An unexpected error occurred: "https://registry.yarnpkg.com/postcss-custom-media: read ETIMEDOUT".
```
看得出来，网络上出了问题，先查查issue，这次找到了解决办法，
```
    yarn install --network-concurrency 1
```

## 总结
初学者有这些装备就差不多了，后续有需求了再补充


