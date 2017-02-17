# 移动端兼容性问题整理
## 一、点击穿透
## 二、软键盘遮挡输入框的问题
android处理：
```
// .container 设置了 overflow 属性, 导致 Android 手机下输入框获取焦点时, 输入法挡住输入框的 bug
    // 相关 issue: https://github.com/weui/weui/issues/15
    // 解决方法:
    // 0. .container 去掉 overflow 属性, 但此 demo 下会引发别的问题
    // 1. 参考 http://stackoverflow.com/questions/23757345/android-does-not-correctly-scroll-on-input-focus-if-not-body-element
    //    Android 手机下, input 或 textarea 元素聚焦时, 主动滚一把
    if (/Android/gi.test(navigator.userAgent)) {
        window.addEventListener('resize', function () {
            if (document.activeElement.tagName == 'INPUT' || document.activeElement.tagName == 'TEXTAREA') {
                window.setTimeout(function () {
                    document.activeElement.scrollIntoViewIfNeeded();
                }, 0);
            }
        })
    }
```
ios处理：
```
     $("#mobile").focus(function(){
         setTimeout(function() {
             $('body').scrollTop(100);
         }, 500);
     });
```
## 三、不支持fixed的问题
## 四、cors的问题
1. 在测试环境中（域名：http://202.69.27.140:13080/），我们通过safari的隐私设置，将“Cookie 和网站数据”选项设置为“始终允许”（默认设置为允许来自我访问的网站），就可以在请求的时候带上cors第三方的cookie，选项设置的相关说明如下：
    a) 始终阻止：Safari 将不允许任何网站、第三方或广告商将 Cookie 和其他数据储存在您的 Mac 上。这可能会使得某些网站无法正常工作。
    b) 仅允许来自当前的网站：Safari 仅接受您当前访问的网站的 Cookie 和网站数据。网站通常具有其他来源的嵌入式内容。Safari 不允许此类第三方储存或访问 Cookie 或其他数据。
    c) 允许来自我访问的网站：Safari 仅接受您所访问的网站的 Cookie 和网站数据。Safari 使用现有 Cookie 确定您之前是否访问过网站。选择此选项有助于防止具有您浏览的其他网站中的嵌入式内容的网站将 Cookie 和数据储存在您的 Mac 上。
    d) 始终允许：Safari 将允许所有网站、第三方和广告商将 Cookie 和其他数据储存在您的 Mac 上。
2. 额使用生产环境的地址（域名：http://ff-app-cms.pingan.com.cn/），则不需要修改safari的隐私设置就能正常传递cors的第三方cookie

这个实验结果跟在手机上的效果是一致的，在部分手机微信上，测试环境的地址无法完成注册，但是生产环境的地址可以完成注册，所以我大胆猜想，部分高版本的浏览器对不标准的域名地址（如http://202.69.27.140:13080/这种带ip和端口的）的cors第三方cookie进行了限制，但是对标准的域名访问地址无限制
这个猜想目前尚未查阅到权威资料印证，也没有想到别的什么更好的测试方法，比较遗憾！！！
## 五、zepto.js tap触发两次
