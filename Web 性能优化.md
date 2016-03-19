#一些疑问
是否应该将用于异步下载的行内脚本往前放，以便更早的开始下载脚本
异步脚本只是声明 `init` 方法，而不调用。
加载成功回调监听 DOMContentLoaded ，在那里调用 `init()`

#异步脚本
异步加载脚本，不阻塞页面渲染。
方法是 script Dom 和 `document.write` script
Chrome ff Safari 下用 script dom, ie 下用 `document.write`
`document.write` script 的缺点是阻止其他资源的下载，script dom 则是并发下载。可能要加上 `async` 标签？
加载成功的回调要放到 `scriptDOM.onload` 里面，ie8- 要用 `readystatechange`
异步脚本在一些浏览器中无法保证执行顺序，谁先来，谁先执行。
如果把异步脚本添加的代码放置在 `</body>` 之前，那么 `callback` 函数不必判定 `window.onload` 

#函数作用域
当函数创建时，当前执行函数作用域链和活动对象复制到函数作用域链
当函数执行时，创建当前函数的活动对象
2+次以上使用垮作用域变量，需要提出局部变量。
`with` 会创建新的作用域，当前函数所有作用域都变成了跨域的，故不推荐使用
**疑问** `eval` 使用上有啥需要注意的地方

#操作 DOM
不循环操作 DOM，循环计算，一次写入。
`innerHTML` 与 `document.createElement` `appendChild` 性能相差无几
`cloneNode` 会更加高效
`HTMLCollection` 是动态集合，最好放到数组里操作。
遍利 DOM 时使用 `nextSibling` 要快于 `childNodes`。
过滤文本和注释节点，使用 `children` `childElementCount` `firstElementChildren` `nextElementSibling`
`querySelectorAll` 返回的不是 `HTMLCollection`, 是静态的。`NodeList`
重排是布局渲染树的变更，重绘是布局或其他样式的改变导致的。
设置某些展示相关的属性后，如果马上获取，会发生即时重排重绘。比如 `offserTop` `getComputedStyle()`
使用 `.style.cssText` 批量修改样式，代替直接使用 `style.backgroundColor` 
频繁变动样式的场景，可以使用 `document.createDocumentFragment`
使动画元素脱离文档流 绝对定位 -> 动画 -> 恢复相对定位

#算法与流程控制
倒序遍历数组
    for (var i = length; i--; ) {  }
减少迭代次数，达夫设备，分割总迭代次数，倍数次执行处理函数，循环余数。应用于 1000 次以上的循环。
基于函数的迭代比基于循环的要慢一些，性能要求严格的地方不要使用。`Array.prototype.forEach`
`if else` 要把概率大放到前面来判断，给 `if else` 做嵌套分组
递归调用要考虑浏览器调用栈大小限制，大概为 1 万，故变递归为迭代是更好的实现方式
Memoization 工厂函数，用于包装函数，缓存函数计算结果

#字符串和正则表达式
`str = str + 'one' + 'two'` 性能好于 `str += 'one' + 'two'`
ie7- 连接大量字符，使用 `Array.prototype.join` 更好
######正则表达式原理
1. 编译 （赋值给一个变量，比每次都声明好，可减少此步）
2. 设置起始位置
3. 匹配每个字元，失败后回溯起始位置，尝试其他路径。
4. 匹配成功，没有匹配成功继续设置起始位置，重复第 2 步

一些字符是决策点，比如： `*` `,` `+?` 
贪婪匹配与非贪婪匹配的方向是不同的。
以简单、必需的字元开始 如 `^` `$`
具体化量词匹配模式 用 `[^1]*1` , 而不用 `.*?1`
尽可能少用分之 用 `[cb]at` 而不用 `cat|bat`
尽可能使用非捕获组 `(?:...)`
只捕获感兴趣的
只获取固定位置或一个字符的，不应使用正则，而应该使用 `charAt` `slice` `substr` `indexOf` `lastIndexOf`

#快速响应用户界面
运行时间长的脚本，可能会引发浏览器报错。5 - 10 秒
建议单个执行任务时间不超过 100 ms
使用定时器让出，让 UI 先执行（先刷界面）。 最小延迟建议 25 ms
使用定时器处理数组，每遍历一个执行，延迟一下， 前提是执行过程不必同步
使用定时器处理多任务，任务无同步要求的。
重复定时器最好间隔 1 秒以上
HTML5 `Worker`  `new Worker('xxx.js')` `onmessage` `event.data` `postMessage()` ie10+


#网页呈现关键路径
1. Parse Html -> DOM
2. Parse CSS -> CSSOM
3. Gen render tree
4. Layout
5. Render
