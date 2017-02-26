# 买了阿里云之后
>终于战胜拖延症，备案好了域名，下狠心买了一个阿里云（低配打了折的还得好几十一个月，宝宝心里苦~）。苦归苦，web环境（主要是为了node应用服务）还是要搭建起来的，开车了，请坐好扶稳！！！

![](./images/aly/baby.jpg)
## 一、前戏
除了购买之前需要先买一个域名以及备案，购买的过程中也有事情需要注意。

阿里云实际上可以看做一台计算机，在买计算机之前，了解配置是必不可少的一步，此前我也咨询过朋友，然而没有实践经验，难以真正理解。反正从无到有，反正阿里云的配置可以弹性变更，莫不如听信阿里的谗言，选一个个人入门型的。

![](./images/aly/xin.jpg)

其它的配置都帮勾选好了，唯独操作系统是需要自己动手的，在windows和linux之间，请不要犹豫，放弃windows，因为这是服务器，即使习惯了windows，也应该跳出自己的思维舒适区。然而，linux系统也还有好几种，这个时候该干嘛？没错，谷歌（或者度娘）。网上有各种优劣对比，走到了这个阶段也应该知道自己的侧重点了。我选了一个Ubuntu 14.04 64位，Ubuntu和Debian都使用的apt-get的方式安装软件，这是我更熟悉的一种方式，并且Ubuntu基于Debian开发，有比Debian更加激进的软件更新策略，嗯，年轻就应该多尝试。
> 自己折腾、实践，选错了也没多大点事，因为系统是可以重装的

## 二、连接
拿到阿里云实例之后，第一要务就是能够远程连接，我发现我在管理界面中点击远程连接按钮进入命令行连接的时候我是不知道root密码的，好吧，重置密码吧，**重置密码之后一定要记得重启**，否则密码是无效的

拿到root密码，ip，其实就可以把管理后台搁在一边了，可以使用你习惯的终端（这里我mac shell），以ssh的方式远程登录，以sftp的方式来上传下载文件，服务器上编辑文件使用vi
> 这里全程使用命令行的方式操作，木有图形界面，请试着接受，习惯之后，你会发现，这个逼完全是可以装的，没有想象中复杂，却比想象中迅捷

![](./images/aly/can.jpg)

连接命令：
```
    //ssh连接
    # ssh root@yourip
    # your root pass

    //sftp连接
    # sftp root@youip
    # you root pass

```
命令很多，不是本文的重点，网上教程可以搜索到很多，可以找来看看，不需要每个命令都记住，有印象即可，用到可以去查，常用的自然会记住

## 三、尝试python启动最简单的web服务
使用购买好的域名解析到实例对应的公网ip。

使用ssh命令连接之后，需要确定一个保存web文件的目录，在`/home`目录下创建一个`WWW`以及`WWW/static`。使用sftp连接，上传一个`index.html`，内容嘛as you wish，主要是用来测试的
```
    //ssh
    #cd /home
    #mkdir WWW
    #cd /WWW
    #mkdir static
    //sftp
    # cd /home/WWW/static
    # lcd dir(本地index.html所在目录)
    # put index.html
```
Ubuntu默认已经安装了python，直接输入`python`命令如果能进入python命令行就可以证明此言不虚了，一个命令就可以启动一个最简单的web服务，在浏览器输入：`http://youdomain/index.html`，如果访问正常，那么第一步就成了
```
    # python -m SimpleHTTPServer 80 
```

![](./images/aly/qu.jpg)
## 四、安装git
git无疑已经是最流行的代码管理工具，而github这个基于git进行版本控制的源代码托管服务也是最流行。我的应用代码也托管在github上面，安装git之后，我可以方便的从github更新最新的代码，这一点很重要。另外Ubuntu的一些软件也可以基于git安装
```
    //安装
    # apt-get install git-core
    //使用
    # cd /home/WWW
    # git clone https://github.com/zengwenfu/h5-creator.git
    # your github username  
    # your github password
```

## 五、安装nvm、node
我这里需要部署的是基于node的web应用，所以需要安装node，为了能在多个node版本中切换如流，需要安装一个node的版本管理工具nvm
```
    //前面我们已经按照了git，所以可以使用git
    # git clone https://github.com/creationix/nvm.git ~/.nvm && cd ~/.nvm && git checkout `git describe --abbrev=0 --tags`  
    
    //编辑环境变量文件
    # cd
    # vim .bashrc
    //增加
    source ~/.nvm/nvm.sh   
    // 添加到系统
    # source .bashrc
```
如此nvm便安装成功了，可以使用nvm来方便的安装node了，
```
    //查看可用的node版本
    # nvm ls-remote
    //安装指定版本，默认已经安装了npm了
    # nvm install 5.8.0
```
进入上一步中在github中下载的代码，安装依赖包，执行启动命令，不过好像出了点错误
```
    # cd /home/WWW/h5-creator
    # npm install
    # npm start
```
![](./images/aly/cai.jpg)
## 六、安装mongodb
上一步报的错误是因为h5-creator使用了mongodb，然而服务器上没有安装所致，所以mongodb也得安装上
```
    //添加mongodb签名到APT
    # apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv EA312927
    //创建/etc/apt/sources.list.d/mongodb-org-3.2.list文件并写入命令
    # echo "deb http://repo.mongodb.org/apt/ubuntu precise/mongodb-org/3.2 multiverse" | sudo tee /etc/apt/sources.list.d/mongodb-org-3.2.list
    //更新软件源列表
    # apt-get update
    //安装mongodb（默认是安装稳定版）
    # apt-get install -y mongodb-org=3.2.9 mongodb-org-server=3.2.9 mongodb-org-shell=3.2.9 mongodb-org-mongos=3.2.9 mongodb-org-tools=3.2.9
```
安装成功之后，默认已经自启动，重新到`/home/WWW/h5-creator`中运行`npm start`即可正常运行，由于这个node服务默认使用了3000这个端口号，得输入域名加端口才可以访问，当然可以改为监听80端口，便可以直接输入域名访问应用。然而，倘需要在服务器中部署多个node应用监听不同的端口，则必有占不到80端口的应用，如何在访问网站的时候省去端口号呢，这需要nginx的反向代理，详情请往下读

在此之前还有一个问题，启动了node服务之后，终端界面停留在了node服务日志的输出界面中，退出终端，则服务也跟着被中断了，所以还需要一个管理node进程的pm2。当然pm2解决的问题不单是退出终端界面不中断服务，众所周知，node是单线程的，倘若应用出现了未捕获的异常，那么进程将中断，服务也就中断了，线上产品如此，那是灾难性的，使用pm2管理node进程，可以在出错的时候重启。
> 类似的还有基于python的supervisor

## 七、安装pm2
pm2是基于node的模块，使用npm全局安装即可，不过一定要全局安装，安装成功使用pm2代替node启动node服务
```
    //安装
    # npm install pm2 -g
    //进入h5-creator
    # cd /home/WWW/h5-creator
    //启动服务
    # pm2 start server.js

    //pm2 其它常用命令
    //查看node进程列表
    # pm2 list
    //显示特定进程详情
    # pm2 show id
    //重启
    # pm2 restart id
    //停止
    # pm2 stop id
```
如此启动之后，终端不会停留在node应用日志界面，你可以安安静静的离开了~
![](./images/aly/mei.jpeg)
## 八、安装nginx
使用nginx的反向代理，可以将同一台服务器上监听不同端口的服务，都能以80端口作为代理入口，定向到特定的服务
```
    //安装
    # apt-get install nginx
```
nginx的配置文件在`/etc/nginx`目录，查看nginx.conf发现如下一句
```
    include /etc/nginx/conf.d/*.conf;
```
所以的配置文件加入conf.d目录即可，具体的配置规则，三言两语也说不清楚，需要找点资料稍微系统的看下，这里只挑我的配置中的关键部分进行说明
```
     listen       80;
     server_name  h5.facemagic888.com; //域名绑定
     server_tokens off; ## Don't show the nginx version number, a security best practice

     root   /home/WWW/h5-creator;
     index  index.html index.htm;

     .......

     location / {
        ...
        proxy_pass http://localhost:3000; //代理定向到localhost:3000
     }
```
我注册的域名是facemagic888.com，可以解析www.facemagic888.com这个一级域名，还可以解析诸如h5.facemagic888.com的二级域名，由于一级域名有别的用途（个人网站，开发中），所以这个h5在线生成工具给了一个二级域名h5.facemagic888.com。这个域名解析到服务器的ip，通过80端口访问服务器（默认无需输入）的时候，nginx会转发到服务器的3000端口应用进行处理

至此，阿里云的部署配置算是告一段落了，其它的什么问题，运行的过程中再观察了，抄小路，去访问一下部署好的网站吧：http://h5.facemagic888.com/

## 总结
说起来完成整个过程只有8步，但是涉及到的知识点还是蛮多的，一步一步慢慢尝试慢慢品，会有很多收获，just do it

[菲麦前端专题，汇聚前端好文，邀您关注！](http://www.jianshu.com/c/4f96d8bcb372)



