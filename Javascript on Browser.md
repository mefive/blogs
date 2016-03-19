#Window

`.screenLeft(.screenX FF)` `.screenTop(.scrreenY FF)` 窗口位置

`window.innerHeight || document.documentElement.clientHeight` 视口高度（viewport）

关闭窗口要用 `top.close();` 。`top` 是打开窗口的页面实例

`.navigator.userAgent` 用户代理字符串， 

######例如

    Mozilla/5.0 (Macintosh; Intel Mac OS X 10_11_1) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/49.0.2623.87                 Safari/537.36

location href path domain hash (ie9+)

能力检测

需要用 `typeof === 'function'`   'undefined' 'unknown'

html escape

xxs attack

`.frames` 页面中的所有 iframe 实例



#DOM

#####继承关系

document `HTMLDocument` -> `Document` -> `Node`

documentElement `HTMLxxxElement` -> `HTMLElement` -> `Element` -> `Node`

#####Document document

`DOMContentLoaded` ie9+

`readystatechange` ie8- `document.readyState === 'interactive'`

`getElementById(string)` `createElement(string)` `createTextNode` 

`domain`

#####Node

`childNodes` 子节点 `children` element 子节点

`appendChild` 追加子元素

`attributes` `hasAttribute()` `attributes[xxx].specified` (ie8-)

#####HTMLElement

`dataset`  `style`

#####Element  

`innerHTML`  `normalize`  将文本节点合并成一个

#####Text 

`nodeValue` 值



#操作 DOM

`script.onload` 先执行 再触发

`<link rel="stylesheet" type="text/css" href="xxx.css" />`

`<script src="xxx.js" />`

`<img src="xxx.jpg" />`

`<a href="xxx">xxx</a>`

`document.findXXXBy` 返回的 NodeList 是动态的， 而 jQuery find 确不是

NodeList slice (ie 不支持, 需要循环遍历 push)

innerText (textContent firefox) 插入文本

`.style` 访问元素的样式 特例：`cssFloat` `styleFloat`(ie)

`.style.removeProperty(string name)` (IE 11+) 删除指定样式

`window.getComputedStyle` `htmlElement.style.currentStyle` ie 获取计算后的样式

`document.styleSheet[0].insertRule` `.addRule` 操作样式表

`.offsetHeight` 算上边框的高度 `.offsetTop` 上边框到包含元素内边框的距离

`.clientHeight` 包含内边距的高度

`document.body.clientHeight` 文档高度 

`window.open` 如果没有在用户操作的 handler 里，会被拦截



#Event

`document.implementation.hasFeature('xxx', 'version')`  搜寻一下所有的 xxx 和 version，不常用

HTML 事件处理程序扩展作用域 event 全局对象 (js 处理函数里，event 并不注入 firefox)

`<button onClick="console.log(event);console.log(clientX)">Click</button>`

DOM0 事件 `dom.onXXX = function(event)` ie8- 没有参数，需要用window.event 获取

DOM 事件流顺序 捕获 -> 目标 -> 冒泡 ie8- 只有冒泡

`event.eventPhase` 1: 捕获阶段 2: 目标阶段 3: 冒泡阶段

`addEventListener` `removeEventListener`

 `attachEvent('onXXX', func)` `detachEvent` ie8-

`event.preventDefault` `event.returnValue = false` ie8-

`event.stopPropagation` `event.cancelBubble = true` ie8-

`event.isTrusted` 是否是用户触发的

`event.target` `srcElement` ie8-  触发事件的真实元素

`event.currentTarget` handler 处理的元素 === this, 但是 ie8- 的 this === window

`img` 一定要先 append 到文档中再监听 onload 事件 ， ie8 bug

发生在 `window` 上的事件，`event.target` 都是 `document`，**这个并不是啊**

#####UIEvent

`onload`  `onunload` 销毁页面

`onresize` 

`onscroll` 滚动事件，用 `dom.scrollTop scrollLeft` 获取偏移

`onfocus` `onblur` 不会冒泡

`onfocusin` `onfocusout` 会冒泡

支持焦点事件的有 `<input>` `<textarea>`  `<a>`  `<select>`  `<button>`

##### Mouse Event

`onmouseenter`  `onmouseleave` 不冒泡 后代元素不会触发

`onmouseover` `onmouseout` 冒泡 进入后代也会触发 

`event.relatedTarget` 相关元素  `fromElement` `toElement` ie8-

`onmousehwheel` 鼠标滚动事件 `DOMMouseScroll` firefox 老版本

`event.clientX` `event.clientY` 距离视口 viewport 边缘的距离

`event.pageX` `event.pageY` 距离 document 边缘的距离

`onmousedown` `onmouseup`

`event.button` 0: 鼠标左键 1: 鼠标滚轮按钮 2: 鼠标右键 MouseEvent 2.0 (1 左键 2 右键 ie8-)

`event.offsetX` `event.offsetY`  对于目标元素的偏移 （需重构 delight-ui Draggable 的 mouseOffset）

`onmousewheel` `event.wheelDelta` 

`dom.addEventListener('DOMMouseScroll', func)`  `-event.detail * 40`  firefox

##### Keyboard Event

`onkeydown` 任意键

`onkeypress` 字符键 按住会重复发

`onkeyup` 松开

`event.keyCode` 按键字符编码 `esc 27`  `enter 13`

`event.charCode` ie9 + ascii 编码  

`event.keyCode` ascii 编码 ie8-, 使用 `String.fromCharCode` 获取字符

`oninput`  ie9+ 尝试在 ie8 下模拟这个

##### HTML5 事件

`oncontextmenu` 右键菜单

`onbeforeunload` 不要用 `addEventListener` `attachEvent` 返回 string 和  赋值 `event.returnValue`

`window.onhashchange` `event.newURL` `event.oldURL'  ie9+

移动设备 `ontouchstart` `ontouchmove` `ontouchend`

##### 事件有关的内存优化

用 `innerHTML` 移除的 dom，需要手动移除 event handler

onunload 中手动移除 event handler

##### 模拟事件

document.createEvent('MouseEvents') // KeyboardEvent CustomEvent

document.createEventObject (ie8-)

bulr focus click 到底在什么地方可以手动触发

focus 只能用于元素 input



## 表单

`<form>`

attribute `action` `acceptCharset` 

`.name` `.reset()` `.submit()` `.target` url

`document.forms[formNameString]` 

`.elements` input 元素集合 HTMLCollection

`form.elements[fieldName]`

`input` 获得焦点回车就提交表单

`onsubmit` 提交表单时

`.submit()` 不触发 `submit` 事件

#####表单元素

`<input>`

attribute `disabled` `form` `name` `readOnly` `tabIndex`  `type` `value`

`<select>`  type 是只读的

attribute  `autofocus` ie10+

`onblur` `onchange` blur 时候触发  `onfocus`

`<input type="text">`  `.select()` 模拟触发

`.onselect` 鼠标释放触发, 但是 ie8- 鼠标未触发释放

`.selectionStart` `.selectionEnd` ie9+

`.setSelectionRange(number start, number end)` ie9+

######ie8-

    var range = textElement.createTextRange();

    range.collapse(true);

    range.moveStart(0);

    range.moveEnd(2);

    range.select();

`oncopy` 拷贝事件

`event.clipboardData` 

`window.clipboardData` ie8-

`clipboardData.getData('text')` `clipboardData.setData('text/plain', value)`

html5 校验 attribute `maxLength` `minLength` `max` `min` `pattern`

`.checkValidity()`

`<form>` attribute `novalidate`

`<input>` attribute `formnovalidate`

`<select>` `.value` `.selectedIndex` `.options`  HTMLCollection

`<option>` `.value` `.text` `index` `selected`



## 富文本编辑

contenteditable(attr) or iframe desigMode

execCommand 点击两次是 toggle 

常用 bold copy fontsize forecolor backcolor

####细化操作 ie9+

    var range = document.getSelection().getRangeAt(0);

    var p = document.createElement('span');

    p.style.backgroundColor = 'yellow';

    range.surroundContents(p);



## HTML5 脚本编程

XDM postMessage onmessagee

evet 参数 data source origin

dragstart drag(持续) dragend

dragenter dragover(持续) drageleave 

history pushState(stateObj, '', url) popState replaceState

onpopstate event.state === stateObj



##错误处理与调试

    try {        

    }

    catch(error) {

        console.log(error.message);

    }

    finally {

        // 防止 try catch 语句中有 return

    }

错误类型 Error EvalError RangeError ReferenceError SyntaxError TypeError URIError

window onerror 参数 message url line

需要关注的三种错误 类型转换错误 数据类型错误 通信错误

console log error info warn



## 其他心得

单例对象可以挂在 构造函数上 XXX.instance

单例对象也可以挂在工厂函数上 XXXfunc.instance



## Ajax

XMLHttpRequest

readyState 3 loading 4 完成

xhr.responseText 保存完成的返回结果

事件 load(ie 是否支持) progess error(network error) abort

setRequestHeader getResponseHeader getAllResponseHeaders

POST 提交表单

Content-Type application/x-www-from-urlencoded

表单数据是 name=value & 分割

HTML5 api

FormData timeout overrideMimeType

load 事件

xhr.upload.onprogress xhr.download.onprogress 事件 event.loaded total ie10+

跨域 ajax , Access-Control-Allow-Origin * or domain

ie 实现跨域，XDR 对象 XDomainRequest，不发 cookie 只支持 get post, 只能设置 Content-Type 头，不能访问 res 的 header 信息

EventSource 非 ie , event open message error , 数据在 event.data 中， Content-Type 是 text/event-stream

##web sockets

ws:// wss:// header Connection: upgrade

`var socket = new WebScoket(url);`

`socket.close();`

readyState 0 OPENING 1 OPEN 2 CLOSING 3 CLOSE (不需要关注)

event onopen onerror onmessage(evenr.data) onclose

##cookie 20-50个 4096

`document.cookie` 设置它并不会覆盖，除非已经有了字段

设置其他参数 `domain=.xxx.com; expires=time.toGMTString(); `

domain path expire secure

#web 存储 2.5M 限制

Storage clear getItem(name) key(index) removeItem(name) setItem(name, value)

sessionStorage  会话数据，浏览器关闭消失

localStorage

document storage 事件 event: domain key newValue oldValue



#file api 需要看



#跨域异步请求

GET 请求

    1.CORS (服务器配合)

    2.JSONP （服务器配合）



POST 请求

    1. CORS （服务器配合）

    2. 相同根域，不同子域，iframe 模拟，直接通信。

    3. 不同域，iframe 模拟，postMessage 通信。(ie8+)
