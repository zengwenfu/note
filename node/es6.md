# es6速记
## let和const命令 --- 块级作用域
- 不存在变量提升，必须先声明后使用
- 暂时性死区，块级作用域内使用了let/const命令的变量，绑定了这个块，不再受外部同名变量的干扰，立即执行匿名函数（IIFE）不再必要了
- 不允许重复声明
- let和const的区别在于，const声明的是只读的常量，一旦声明，就不能改变，所以必须声明的时候赋值（对于符合类型的变量，const只保证地址不变，不保证数据不变）

特点：增加了块级作用域，变量的声明使用更加严格，可在编译/解释阶段报错，以免带来不可预知的错误

## 变量的解构赋值 --- 模式匹配
- 数组
```
    let [x, y] = [1, 2, 3];
    x // 1
    y // 2

    //交换
    [y, x] = [x, y]
```
- 对象属性赋值
```
    let { id, status, data: number } = jsonData;
```
- 函数参数、返回值 --- 参数默认值，函数返回多值
```
    //参数默认值
    jQuery.ajax = function (url, {
      async = true,
      beforeSend = function () {},
      cache = true,
      complete = function () {},
      crossDomain = false,
      global = true,
      // ... more config
    }) {
      // ... do stuff
    };

    //函数返回多值
    function example() {
      return {
        foo: 1,
        bar: 2
      };
    }
    var { foo, bar } = example();
```

特点：语法糖，在很多地方提供了方便，运用广泛
