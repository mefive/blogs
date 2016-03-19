#HTML 中使用 JavaScript

`<script type="text/javascript" src="xxx.js"></script>` 如果有 `src` , 行内代码将会被忽略

`defer` 脚本，保证顺序异步下载，DOM 解析完毕后执行。

`async` 脚本，不保证顺序异步下载，完成后立即执行。



#数据类型

5 种简单类型 `Undefined` `Null` `Boolean` `Number` `String`

1 种复杂类型 `Object`

`typeof` 6 种结果 `undefined` `boolean` `string` `number` `object` `function`

`typeof null === 'object'`

######`Undefined` 类型

一切没有被赋值过的变量的默认值。没有声明过的变量的 `typeof === 'undefined'`

######`Null` 类型

空对象引用。`undefined` 派生自 `null`。`undefined == null`

######`Boolean` 类型

`Boolean(xxx)` 可以转化其他类型到 `Boolean` 类型，`if (xxx)` 与之等价。

非空字符是 `true`，空字符是 `false`。非零数字是 `true`，零是 `false`。对象是 `true`，`null` 是 `false`。`undefined` 是 `false`

######`Number` 类型

八进制 `070`（严格模式下不能用）， 十六进制 `0x1f`

用 `e` 表示很大的值，10 的 xx 次方，例如 `2e2 === 200`

浮点数值最高精度是 17 位小数，计算精度有误差

数值边界 `Number.MIN_VALUE` 和 `Number.MAX_VALUE`

`NaN` 非数值 `NaN != NaN`

`Number()` 布尔值是 `0` 和 `1`。`null` 是 `0`。`undefined` 是 `NaN`。字符串八进制忽略，十六进制转换，空字符串是 `0`，其他是 `NaN`。对象先调用 `valueOf()` 再调用 `toString()`

`+` 一元操作符与 `Number()` 等效

`parseInt()` 专门处理字符串。空字符串是 `NaN`。会忽略掉字符串中的非数字部分及其以后。第二个参数是必须的，因为 es3 和 es5 对于八进制处理有冲突。

`parseFloat` 只解析十进制字符串，十六进制的始终为 `0`

`String` 类型 `length` 单字节字符长度 调用所有类型的 `toString()` 方法将其转换成字符串

数字的 `toString(进制)` 

`+` 加法二元运算符，优先考虑字符串，后转化成数字

######`Object` 类型

`isPrototypeOf(Obj)` `propertyIsEnumerable(propName)` 



#操作符

######一元操作符 

`++` `--` `+` `-` ，先把变量转化成数字，`Number()`

######位操作符（待补充）

######布尔操作符

`!` 转化成布尔型  `Boolean()`

`||` `&&` 不会转化，而是短路计算

######乘除操作符 

`*` `/` 转化为数字类型 `Number()` `Infinity * 0 === NaN` `Infinity * 2 = Infinity` 

######加操作符 

`+` 如果有一个是字符串，那么转化成字符串。不过都不是字符串，转化成数字 `Number()` `Infinity + -Infinity === NaN`

######减操作符 

`-` 转化成数字 `Number()`

######关系操作符 `<` `>` `>=` `<=` 

都是字符串的，比较字符串对应字符编码，大写字母小于小写字母

其中一个是数值，另一个转化成数值 `Number()`

如果是对象，则调用 `valueOf()` 和 `toString()`

与 `NaN` 比较，都是 `false`

######相等操作符 `==`

如果有一个是布尔型、字符串型，都转化成数值，`Number()`

如果有一个是对象，调用对象的 `valueOf`

`null == undefined` `null` 和 `undefined` 与其他类型比较时，都不相等（不转化）



#语句

######`if`

转化为布尔型 `Boolean()`

######循环

    do { ... } while (i++)

    while (i) { ..., i++ }

    for (var i = 0; i < 10; i++) { ... }

    for (var key in obj) { ... }

######`switch`

    switch (key) {

        case: expression

            ...

            break;

        default:

            ...

    }

######函数

`arguments` `Array.prototype.slice.call(arguments)` 转化成数组

参数是变量的值传递，而不是变量的引用



#变量

基本类型和引用类型

######基本类型

无法添加属性



#垃圾回收

大多数浏览器利用“标记清除”算法做内存回收。进函数、出函数标记变量可达的内存。GC遍历不可达内存，销毁之。

ie 中的 DOM 采用了引用计数方式，因此要避免循环引用



#Array

length 不是只读的，可以设置，新增 `undefined`,  或者删除末尾。

######方法

`push()` 末尾增加

`pop()` 末尾移出

`shift()` 首位移出

`unshift()` 首位移入

`sort()` -1 1 0

`reverse()` 翻转

`concat(array)` `slice(start, end)` `splice(start, length, insert...)`

`indexOf()` `lastIndexOf()` ie9+

`every()` `filter()` `forEach()` `map()` `some()` `reduce()`



#Date
