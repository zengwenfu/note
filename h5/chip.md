# 知识碎片

## npm run command 不完全等于直接在命令行输入command
```
    "scripts": {
        "start": "cross-env NODE_ENV=dev supervisor -w server,app.js app",
        "bs": "cross-env NODE_ENV=dev node app_browsersync",
        "build": "webpack --config webpack.production.config.js -p",
        "precommit": "eslint 'client/js/**/*.js'",
        "production": "gulp webpack",
        "public": "node app_public.js"
      }
```

> 在命令行输入npm run public 和直接输入node app_public.js都不会有问题，然而执行node run start正确的情况下，执行cross-env NODE_ENV=dev supervisor -w server,app.js app却会报错。原因是，npm run 能将 /node_modules/.bin 加到你的PATH中，gulp进行了全局安装所以public命令不管怎么执行都是可以的，然而coss-env和supervisor都未进行全局安装，直接在命令行执行是找不到命令的，而使用npm run, 在/node_modules/.bin 目录下找到了命令，所以可以正常的跑