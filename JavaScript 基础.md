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

`global.parseInt()` 专门处理字符串。空字符串是 `NaN`。会忽略掉字符串中的非数字部分及其以后。第二个参数是必须的，因为 es3 和 es5 对于八进制处理有冲突。

`global.parseFloat()` 只解析十进制字符串，十六进制的始终为 `0`

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

`var now = new Date()`

`Date.parse(string)` 兼容性差 `Date.UTC(year, month -1, day, hour, minute, second)` GMT 时间 这俩都返回 ms 数

`new Date(与UTC相同的至少两个参数)` 解析 GMT 时间

`valueOf()` 返回 ms 数

一系列 set get 方法，比如 `getFullYear()` `getMonth()` 唯一要注意的是  month 是 0 - 11 的



#RegExp

`/.../g` 全局。`/.../i` 忽略大小写

`[ab]` a或b。 `[^ab]` 非a且非b

`()` 分组。 `(?:)` 分组不捕获

`{1, 2}` 重复次数。`*` 任意次。`?` 零次或一次。`+` 一次或多次。`*?` `??` `+?` 贪婪匹配，取最长

`^` 以开头。`$` 以结尾

`|` 或

`\d` 数字，`\D` 非数字

`\s` 空格，`\S` 非空格

`\w` 字母和数字，`\W` 非字母和数字

`.` 任意非换行回车

`\1` 反向引用前面的分组

这些字符串匹配需要转义 `(` `)` `[` `]` `{` `}` `\` `^` `$` `|` `?` `*` `.` `+`  

在 `new RegExp(exp, flag)` 中，这些需要双重转义 `\\`

es5 规定字面量与构造函数每次都返回新实例，但 ie8- 的字面量却不是

`.source` 是字符串表达式

`exec(string)` 捕获组的数组，但再设置了 `g` 全局时，每次返回一次匹配，游标移动。返回数组的 `index` 保存本次匹配的起始点

`test(string)` 测试字符串是否匹配，返回布尔值。设置 `g` 时，每次返回一次匹配



#Function

函数声明提升，函数表达式赋值不提升

`arguments.callee` 函数本身

'length' 命名参数的数量

`apply(context, array)` `call(context, arg1, arg2 ... )`



#基本包装类型

`new String(xxx)` 传统对象。 `String(xxx)` 仅在执行时包装对象，之后销毁



#Number

`toFixed(小数位数)` 返回字符串 四舍五入 ，ie8 下传入 0 不能正确四舍五入。因此取整应该用 `Math.round`。



#String

`charAt(index)` 获取字符，`charCodeAt()` ascii 码， ie8+ 可以是用 `[index]`

`concat(string)` 拼接字符串

`slice(start, end)` `substring(start, end)` `substr(start, length)`

`slice` 负参数与长度相加。`substring` 负参数都转化为 `0`。`substr` 负参数第一个与长度相加，第二个转化为 `0`

`indexOf(char)` `lastIndexOf(char)` `toUpperCase()` `toLowerCase()`

`match(exp)` 与 `exp.exec(string)` 用法相同。`search(exp)` 返回 index

`replace(exp, string)` `$n` 第 n 个捕获组  `$&` 整个匹配的子字符串

`split(exp, length)` 分割字符串为数组

`String.fromCharCode(code, code1, code2...)`  ascii 转化字符串



#Global 对象

`encodeURI(string)` 不会对特殊字符编码 `:` `/` `?` `#`，对空格编码

`encodeURIComponent` 对任何特殊字符编码 用于参数的 `key` 与 `value` 编码

`eval(code)` 严格模式下 代码外部访问不到 `eval`  内部的变量



#Math

`E` `PI`

`.ceil()` 向上舍入。 `.floor()` 向下舍入。`.round()` 四舍五入

`random()` 返回 0 ~ 1 的随机数。`Math.floor(Math.random() * big + small)` 获取介于 small 和 big 之间的数



#对象

#####属性

对象属性分为 **数据属性** 与 **访问器属性** es5

数据属性描述 `configurable` `enumerable` `writable` 默认都是 `true`，`value`。 

ie9+ 可以通过 `Object.defineProperty()` 设置， 一但设置且不配置，`configurable` `enumerable` `writable` 默认都是 `false`

`configurable` 为 `false` 后，不可再改回 `true`，不可被 `delete`，并且不可通过 `defineProperty` 修改除 `writable` 以外的描述

访问器属性就是通过 `defineProperty` 设置 `set` `get` 函数 严格模式下 若定义了一个 也要定义另外一个

`Object.definedProperties` 定义多个属性



#####创建对象

######工厂模式

一个函数返回组装好的对象

######构造函数模式

简单的将属性附加到实例上，缺点是实例之前未共享方法属性，或缺乏封装性

######原型模式

把属性都附加到构造函数的原型上

`Object.getPrototypeOf(obj)` 获取对象上的原型对象

`for in` 会遍历出原型链上线的属性，需要用 `hasOwnProperty()` 过滤掉

es5 中的 `Object.keys(obj)` 返回实例可枚举属性名数组。`Object.getOwnPropertyNames(obj)` 获取实例所有属性数组

原型模式的缺陷是，共享了引用类型的属性

######组合使用构造函数模式和原型模式

构造函数用于实例属性赋值，尤其是引用类型的属性，原型负责函数类型和基本类型



#继承

#####原型链组合构造函数

    function Sub() {

        Super.call(this, arguments);

        ...

    }

    Sub.prototype = new Super();

#####原型式继承

没有构造函数，利用已有的对象创造新对象

###### 

    var F = function () {};

    F.prototype = super;

    return new F();

等价于 es5 中的 `Object.create()`

#####原型寄生组合构造函数

    function Sub() {

        Super.call(this, arguments);

        ...

    }

    Sub.prototype = Object.create(Super.prototype);



#函数表达式

`name` 函数名

递归函数一定要是具名函数，或非严格模式下用 `arguments.callee`

#####闭包

函数创建时，保存了当前运行函数的活动对象和作用域链保存到 `[[scope]]` 里

函数执行时，创建**活动对象**和包含外围活动对象的作用域链（从 `[[scope]]` 复制过来）

IE DOM 元素的 GC 是基于引用计数的，所以会被闭包引用，即便把函数置 `null` 也不会减少引用次数。所以要在不用时吧 dom 变量清空

匿名立即执行函数模拟块级作用域
