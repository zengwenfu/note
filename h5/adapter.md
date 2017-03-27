# 利用rem实现网页的等比适配
> 在[可能是理解viewport最好的方式](http://www.jianshu.com/p/b880b48fa028)说过使用viewport来实现等比适配的例子，本文来讲讲等比适配的另一种方式

## 推导
拿到一个宽度为vWidth的视觉稿     
设设备屏幕宽度为dWidth     
在视觉稿上量得一个元素的宽度为eleVWidth    
那么要实现等比适配，在各种设备中元素的实际宽度X将满足公式
```
    //等比
    eleVWidth/vWidth = X/dWidth;

    //我们的目的是求X
    X = (eleVWidth/vWidth)dWidth;
```
拿到视觉稿之后，eleVWidth和vWidth都已经固定了，但是dWidth在不同的设备中确实不同的，而且需要实际运行的时候我们才能拿到dWidth，这个时候就要利用rem的特性了，**我们通过阻塞运行的js动态设置rem，使得`rem=dWdith/10`**，套入刚才的公式：
```

    X=(eleVWidth/vWidth)*10*rem

    //体现在css中
    .className {
        width: (eleVWidth/vWidth)*10 rem
    }

```
> 为什么设置是dWdith/10呢？方便计算而已，当然也可以除以别的基数，但是尽量不要让rem太小，有兼容性问题

## 动态设置rem
这段css需要放在body标签的开始位置，因为rem值要尽可能早的设置成功，避免无谓的重排重绘（有些设备中若元素样式已经生效，动态改变rem未必能起作用，所以这个动作更需要提前）
```
    <body>
        <script>
        (function() {
            var ua = window.navigator.userAgent;
            var docEl = document.documentElement;
            var html = document.querySelector('html');
            var isAndorid = /Android/i.test(ua);
            var dpr = window.devicePixelRatio || 1;
            var rem = docEl.clientWidth / 10;

            // 设置 rem 基准值
            html.style.fontSize = rem + 'px';

            // Nexus 5 上 rem 值不准，
            // 如：设置100px，getComputedStyle 中的值却为 85px，导致页面错乱
            // 这时需要检查设置的值和计算后的值是否一样，
            // 不一样的话重新设置正确的值
            var getCPTStyle = window.getComputedStyle;
            var fontSize = parseFloat(html.style.fontSize, 10);
            var computedFontSize = parseFloat(getCPTStyle(html)['font-size'], 10);
            if (getCPTStyle && Math.abs(fontSize - computedFontSize) >= 1) {
                html.style.fontSize = fontSize * (fontSize / computedFontSize) + 'px';
            }

            // 设置 data-dpr 属性，留作的 css hack 之用
            html.setAttribute('data-dpr', dpr);

            // 安卓平台额外加上标记类
            if (isAndorid) {
                html.setAttribute('data-platform', 'android');
            }
        })();
        </script>
        ...
    </body>
```

## css中应该怎么写
> 如果每在视觉稿上量出一个值，在写到样式文件之前都得通过那个公司计算一翻，那绝对不是一个好策略，我们希望量到啥就写啥

使用less，sass等css预处理器的函数
```
    //设计稿为640
    @function rem($val) {
        @return $val/64 * 1rem;;
    }

    //设计稿为750
    @function rem750($val) {
        @return $val/75 * 1rem;
    }

    //使用
    .className {
        width: @rem(100);
    }
```

也可以使用webpack-loader，[change-rem-loader](https://www.npmjs.com/package/change-rem-loader)，这个loader代码做的事也是上述的转化计算(写一个webpack loader并不复杂，你可以自己写一个符合自己情况的loader)
```
    'use strict';
    module.exports = function(source) {
        source = source.replace(/rem(\d*)\((.*?)\)/g, function(match, type, value) {
            var divVal;

            // 不做 try catch，及早发现错误以免造成故障
            switch (type) {
                // 1080宽度的设计稿，rem1080(value)
                case '1080':
                    divVal = 108;
                    break;
                    // 默认为750宽度的设计稿，rem(value)
                case '750':
                    divVal = 75;
                    break;
                default:
                    divVal = 64;
            }

            return (value / divVal).toFixed(6) + 'rem';
        });
        return source;
    }

```
这样之后，我们css同样可以这样写（如何让loader起作用不是本文的范围）
```
    .className {
        width: rem(100);
    }
```


> 也许你的工程技术栈里面，使用的不是webpack，也没有使用less、sass等预处理器，那你可以根据你的实际情况去寻找一种预处理方案，只要达到推导公式的效果就可以了。     
> 什么？没有合适的方案，那你是时候充充电了

