# http to https升级记
> 最近准备搞一个小程序玩玩，到配置服务器域名的时候发现只支持https协议，迫于无奈，我不得不再次跳出自己的思维舒适区，发起了一次http向https的冲击
> 在这方面我也了解的不深，写点文字，给自己做笔记看

## 一、获取证书
证书有很好几种类型，有免费的也有付费的，具体可以参考阮一峰老师的[HTTPS 升级指南](http://www.ruanyifeng.com/blog/2016/08/migrate-from-http-to-https.html)。于我而言(还不是因为穷~~）当然是选择最低级的**域名认证**以及免费的**Let's Encrypt**

既然如此，那就直奔**Let‘s Encrypt**这个环节，我的服务器是Ubuntu，所以又针对性的通过谷歌找到了[在Ubuntu上获取Let’s Encrypt免费证书](https://tsukkomi.org/post/get-the-lets-encrypt-certificate-on-ubuntu)（感谢作者qakcn)。

首先进行Cerbot的安装(我的系统版本好像只支持这种方式)：
```
    // 先进入你的安装目录，我进的是/etc
    wget https://dl.eff.org/certbot-auto
    chmod a+x certbot-auto
    ./certbot-auto
```

证书签发，可以通过如下命令
```
    // 进入certbot的安装目录
    ./cerbot-auto certonly --webroot -w /var/www -d example.com -d www.example.com -w /var/www/sub -d sub.example.com
```
关于多个域名生成在同一个证书下的过程有点曲折。我的服务器上部署了多个绑定不同端口的服务，通过nginx反向代理绑定到了不同的二级域名下，起初我将所有一级二级域名都生成在了一个证书当中，然后不管`https://www.facemagic888.com` 还是 `https://h5.facemagic888.com`都解析到了`https://www.facemagic888.com/index.html`这个页面中

一开始怀疑是，多个域名是不是需要单独生成，于是重新执行命令，给二级域名`h5.facemagic888.com`单独生成了一个证书，重新配置之后，情况还是一样

然后再次怀疑，难道是`let's encrypt`不支持二级域名么，可是查了半天也没看到这种说法啊，这恐怕缺乏依据，并且如果真不支持，那还是非常令人沮丧的
> 我不会告诉你，后面才发现是nginx配置的问题

## 二、nginx配置
起初对照着参考文章来进行配置：
```
    # node-ssl配置
    server {
        listen 443 ssl;
        server_name www.facemagic888.com h5.facemagic888.com;

        root /home/WWW/static;
        index index.html;

        ssl on;
        ssl_certificate /etc/letsencrypt/live/www.facemagic888.com/fullchain.pem;
        ssl_certificate_key /etc/letsencrypt/live/www.facemagic888.com/privkey.pem;

        location / {
            try_files $uri $uri/ =404;
        }
    }
```
这样配置之后，没错就是上面怀疑的开始！！！    
后面发现，虽然动态的接口不行，但是静态页面却无法访问，这就奇了怪了，那肯定不是不支持二级域名。 那就是代理配置得有问题洛，跟朋友在群里聊了聊发散了下，80端口既然配置了代理，443端口是不是应该也需要呢?来试一试：
```
    # node-ssl配置
    server {
        listen 443 ssl;
        server_name h5.facemagic888.com;

        root /home/WWW/h5-creator;
        index index.html;

        ssl on;
        ssl_certificate /etc/letsencrypt/live/www.facemagic888.com/fullchain.pem;
        ssl_certificate_key /etc/letsencrypt/live/www.facemagic888.com/privkey.pem;

        location / {
            ## If you use HTTPS make sure you disable gzip compression
            ## to be safe against BREACH attack.
            ## https://github.com/gitlabhq/gitlabhq/issues/694
            ## Some requests take more than 30 seconds.
            proxy_redirect off ;
            proxy_set_header Host $host:$server_port;
            proxy_set_header X-Real-IP $remote_addr;
            #proxy_set_header REMOTE-HOST $remote_addr;
            proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
            proxy_set_header X-Forwarded-Proto $scheme;
            proxy_set_header X-NginX-Proxy true;
            proxy_set_header Connection "";

            client_max_body_size 20m;
            client_body_buffer_size 256k;
            proxy_connect_timeout 30;
            proxy_send_timeout 30;
            proxy_read_timeout 60;
            proxy_buffer_size 256k;
            proxy_buffers 4 256k;
            proxy_busy_buffers_size 256k;
            proxy_temp_file_write_size 256k;
            proxy_next_upstream error timeout invalid_header http_500 http_503 http_404;
            proxy_max_temp_file_size 128m;

            proxy_http_version 1.1;
            #proxy_pass http://NODE_SERVER;
            proxy_pass http://localhost:3000;
          }

        location = /404.html {
            root   /usr/share/nginx/html;
        }
    }
```
还别说，这样还真就行了，果真还是对nginx还不够了解啊!!!

## 三、补充记忆
过来一段时间没折腾了，忘记如何重启nginx，我能说网上给的答案很多都太不直接了么，还是最欣赏这个办法
```
    service nginx restart
```

