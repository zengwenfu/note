# es6速记
> 要对es6有系统了解的同学还请移步**阮一峰**的[ECMAScript 6 入门](http://es6.ruanyifeng.com)
> 本文出于方便记忆的目的，对常用的点进行偏向于应用的整理。

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

## 字符串扩展
- 字符串遍历
```
  for (let codePoint of 'foo') {
    console.log(codePoint)
  }
```
- includes()（是否包含）、startsWith()（是否开始于）、endsWith()（是否结束于）：都返回boolean值，可接受两个参数，`str`要监测的子穿，`index`从哪开始监测，可以认为是indexOf()的分解动作吧
- repeat()：复制字符串，常用于数值补全指定位数
```
  '1'.padStart(10, '0') // "0000000001"
  '12'.padStart(10, '0') // "0000000012"
  '123456'.padStart(10, '0') // "0000123456"

  //提示字符串格式
  '12'.padStart(10, 'YYYY-MM-DD') // "YYYY-MM-12"
  '09-12'.padStart(10, 'YYYY-MM-DD') // "YYYY-09-12"
```
- 模板字符串：再也不用担心多行html字符串拼接的繁复了
```
  $('#result').append(
    'There are <b>' + basket.count + '</b> ' +
    'items in your basket, ' +
    '<em>' + basket.onSale +
    '</em> are on sale!'
  );

  //不需要再一行一行的增加单引号和加号了
  //使用trim的目的是去掉多余的缩进
  $('#result').append(`
    There are <b>${basket.count}</b> items
     in your basket, <em>${basket.onSale}</em>
    are on sale!
  `.trim());

```
- String.raw转义模板字符串

## 正则的扩展

## 数值的扩展
- 0b（或0B）和0o（或0O）可以分别表示二进制和八进制
- Number.isFinite监测数值是否有限
- Number.isNaN()监测数值是否为NaN
- ES6将全局方法parseInt()和parseFloat()，移植到Number对象上面，行为完全保持不变
- Number.isInteger()
```
  Number.isInteger(25) // true
  Number.isInteger(25.0) // true 整数和浮点数是同样的储存方法 所以25和25.0视为相同
  Number.isInteger(25.1) // false
  Number.isInteger("15") // false
  Number.isInteger(true) // false
```
- Number.EPSILON，一个极小的常量，可以用于限定误差范围
```
  5.551115123125783e-17 < Number.EPSILON
```
- Number.isSafeInteger()：判断数值是否落在js可以精确表达的安全范围内
- Math.trunc方法用于去除一个数的小数部分，返回整数部分
- Math.sign方法用来判断一个数到底是正数、负数、还是零
- Math.cbrt()方法用于计算一个数的立方根
- Math.clz32方法返回一个数的32位无符号整数形式有多少个前导0
- Math.fround方法返回一个数的单精度浮点数形式。
- Math.hypot方法返回所有参数的平方和的平方根。
- Math.expm1(x)返回ex - 1，即Math.exp(x) - 1。
- Math.log1p(x)方法返回1 + x的自然对数，即Math.log(1 + x)。如果x小于-1，返回NaN。
- Math.log10(x)返回以10为底的x的对数。如果x小于0，则返回NaN。
- Math.log2(x)返回以2为底的x的对数。如果x小于0，则返回NaN。
- Math.sinh(x) 返回x的双曲正弦（hyperbolic sine）
- Math.cosh(x) 返回x的双曲余弦（hyperbolic cosine）
- Math.tanh(x) 返回x的双曲正切（hyperbolic tangent）
- Math.asinh(x) 返回x的反双曲正弦（inverse hyperbolic sine）
- Math.acosh(x) 返回x的反双曲余弦（inverse hyperbolic cosine）
- Math.atanh(x) 返回x的反双曲正切（inverse hyperbolic tangent）
- ES7新增了一个指数运算符（**），目前Babel转码器已经支持
```
  2 ** 2 // 4
  2 ** 3 // 8

  let a = 2;
  a **= 2;
  // 等同于 a = a * a;

  let b = 3;
  b **= 3;
  // 等同于 b = b * b * b;
```

## 数组的扩展
- Array.from方法用于将两类对象转为真正的数组
```
  // NodeList对象
  let ps = document.querySelectorAll('p');
  Array.from(ps).forEach(function (p) {
    console.log(p);
  });

  // arguments对象
  function foo() {
    var args = Array.from(arguments);
    // ...
  }
```
Array.from()的另一个应用是，将字符串转为数组，然后返回字符串的长度。因为它能正确处理各种Unicode字符，可以避免JavaScript将大于\uFFFF的Unicode字符，算作两个字符的bug
```
  function countSymbols(string) {
    return Array.from(string).length;
  }
```
- Array.of方法用于将一组值，转换为数组，弥补数组构造函数Array()会因为参数个数的不同，导致Array()的行为有差异的问题
```
  Array.of(3, 11, 8) // [3,11,8]
  Array.of(3) // [3]
  Array.of(3).length // 1

  Array() // []
  Array(3) // [, , ,]
  Array(3, 11, 8) // [3, 11, 8]
```
- 数组实例的copyWithin方法，在当前数组内部，将指定位置的成员复制到其他位置（会覆盖原有成员），然后返回当前数组
- 数组实例的find方法，用于找出第一个符合条件的数组成员，它的参数是一个回调函数，所有数组成员依次执行该回调函数，直到找出第一个返回值为true的成员，然后返回该成员。如果没有符合条件的成员，则返回undefined。数组实例的findIndex方法的用法与find方法非常类似，返回第一个符合条件的数组成员的位置，如果所有成员都不符合条件，则返回-1
```
  [1, 5, 10, 15].find(function(value, index, arr) {
    return value > 9;
  }) // 10

  //弥补indexOf不能发现NaN的问题
  [NaN].indexOf(NaN)
  // -1

  [NaN].findIndex(y => Object.is(NaN, y))
  // 0
```
- fill方法使用给定值，填充一个数组
```
  ['a', 'b', 'c'].fill(7)
  // [7, 7, 7]

  new Array(3).fill(7)
  // [7, 7, 7]

  ['a', 'b', 'c'].fill(7, 1, 2)
  // ['a', 7, 'c']
```
- 数组实例的entries()，keys()和values()
```
  for (let index of ['a', 'b'].keys()) {
    console.log(index);
  }
  // 0
  // 1
  
  for (let elem of ['a', 'b'].values()) {
    console.log(elem);
  }
  // 'a'
  // 'b'
  
  for (let [index, elem] of ['a', 'b'].entries()) {
    console.log(index, elem);
  }
  // 0 "a"
  // 1 "b"

  let letter = ['a', 'b', 'c'];
  let entries = letter.entries();
  console.log(entries.next().value); // [0, 'a']
  console.log(entries.next().value); // [1, 'b']
  console.log(entries.next().value); // [2, 'c']
```

## 函数的扩展
- 参数默认值
```
  function Point(x = 0, y = 0) {
    this.x = x;
    this.y = y;
  }

  var p = new Point();
  p // { x: 0, y: 0 }
```