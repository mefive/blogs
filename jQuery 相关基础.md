**`->` 是对应原生 API**

#`$()` 构造函数

1. `$(selector)` 相当于 `document.querySelectorAll(selector)`

2. `$(function)` 相当于监听 `DOMContentLoaded`

3. `$(htmlString)` 相当于 `var dom = document.createDocumentFragment(); dom.innerHTML = htmlString`



#jQuery 工具函数

`each` 遍历对象或数组，遍历对象不会遍历原型链上的属性。回调函数返回 `false` 可以跳出循环。这点区别于 es5 的 `[].forEach`

`map`， `inArray` 相当于 `[].indexOf`

`extend` 复制对象 `extend({}, obj)` -> `Object.assign({}, obj)`，`extend(true, {}, obj)` 深度复制

`grep` -> `[].filter`

`inArray` -> `[].indexOf`

`isArray` `isFunction` `isPlainObject`

`makArray` 

`merge` -> `[].concat`

`parseJSON` -> `JSON.parse`

`proxy` -> `Function.prototype.bind`

`trim` -> `String.prototype.trim`



#jQuery 选择器与 `querySelector` 不同的地方

`[attr!=val]` 不为 val 的

`:animated` 正在执行 jQuery 动画的元素

`:button` 匹配 `<button>` 和 `<input type="button">`

`:input` `:checkbox` `:file` `:radio` `:image`

`:checked` `:select`

`:contains(text)` 匹配有 text 文本的元素

`:eq(n)` 第 n 个元素

`:even` 偶数序号的子元素，实际为奇数次序的，因为第一个是 `0`

`:odd` 偶数次序

`not(sel)` 不匹配的



#jQuery 对象方法和属性 

`toArray()`

`attr()` -> `getAttribute` `setAttribute`

`removeAttr()` -> `removeAttribute()`

`css()` 获取计算后的样式，设置行内 `style`

`addClass()` `removeClass()` `toggleClass()` 设置样式， `hasClass()`

`text()` -> `innerText`，`html()` -> `innerHTML`

`offset()` `.left` `.top` 元素与文档的距离

`offsetParent()` -> `offsetParent`

`position()` `.left` -> `offsetLeft`

`height()` 不含内边距

`innerHeight()` -> `clientHeight` 包含内边距

`outerHeight()` -> `offsetHeight` 包含边框

`data()` `removeData()`

`append()` -> `appendChild()`，`appendTo()`

`prepend()` ，`prependTo()`

`before()` `insertBefore()` , `after()` `insertAfter()`

`replaceWith()` , `replaceAll()` 替换自身

`clone()` -> 'cloneNode()'

`wrap()` 包装自身

`remove()` 移除元素，`detach()` 移除元素保留事件

`toggle(f, g)`  f g f g

#######进一步处理

`first()` `last()`

`not()` `filter()`

`prev()` `next()`

`siblings(sel)` 所有匹配的兄弟节点

`parents()` `closest()`



#jQuey 事件处理

处理函数返回 `false`  表示 `preventDefault(); stopPropagation()`

######`event` 属性

`metaKey` 

`pageX` `pageY` 相对文档的坐标

`clientX` `clientY` 相对 viewport 的坐标

`timeStamp`

`which` -> `charCode` 或 `keyCode`

######事件处理

`on` `one` `off`

#####事件触发

`trigger(event, data)`



#动画效果

`fadeIn(ms, completeCallback)` `fadeOut()`

`slideDown()` `slideUp()`

`animation(styleTo, options)` `options.duration` `options.complete`



#Ajax

    $.ajax({

        url: actionString,

        dataType: // script json jsonp xml html text

        async: boolean

        mimeType: string

        type: methodString // GET POST PUT DELETE 

    })

    .done(function (data, textStatus) {

        textStatus // success 200 notmodified 304

    })

    .fail(function (data, textStaus)) {

        textStatus // error timeout parsererror

    }



