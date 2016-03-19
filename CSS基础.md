####现代 HTML 模板

    <!DOCTYPE html>

    <html>

        <head>

            <meta chartset="utf-8" />

            <!--[if lt IE 8]-->

            <!--[endif]-->

        </head>

        <body>

        </body>

    </html>

####HTML 实体

`&;`

####引入样式文件的方式

    <link href="xxx.css" rel="stylesheet" type="text/css" />

    @import "xxx.css";

    <style></style>

###浏览器厂商前缀

-webkit-

-moz-

###盒模型

`box-sizing: border-box;` 尺寸包含 padding border

外边距叠加，多个垂直比邻（没有 border padding）块元素。行内、浮动、绝对定位不叠加。

块元素：`div` `p` `h1`

行内元素：设置垂直 `margin` 无效，行高只会影响行内元素外的容器

inline-block 与 inline 元素彼此之间有默认 space ，需要去掉 html 之间的空格和换行

浮动如果不够宽，就向下沿浮动方向浮动，直到有位置，便被卡住。

利用 `overflow:hidden` 触发 BFC ，用于清除浮动，双栏布局。

触发 BFC 的另外充分条件是 `float` 不为 `none` 、`display` 是 `inline-block`, `position` 是 `absolute` 或 `fixed`

BFC 计算规则 不与 float box 重叠，计算高度包括 float box 部分

###背景图

`background-position` 像素代表图像左上角对于容器的偏移 百分比代表图像的百分比放置在容器的百分比上

`last-child` ie8+

`<col>` `<colgroup>` 用于整列样式

`fieldset` `legend` `label for`

###布局

流式布局、弹性布局

多栏对齐高度，用大 `padding` 和相近负`margin` 解决

####媒体查询

    

####HTML5 新标签

`<aside>` `<header>` `<nav>` `<article>` `<footer>` `<nav>`

####HTML 标签分类

**块级标签：** `<h1>-<h6>` `<p>` `<ol>` `<li>` `<blockquote>`

**行内标签：** `<a>` `<img>` `<em>` `<strong>` `<cite>` `<q>`

####选择符

`~` 一般同胞选择符，例如 `h1 ~ a { color: red; }`

####伪类

`:focus` `:target` 

####层叠规则

1. id > class

2. inline > stylesheet

####字体

`font-family: times, serif;` 

默认下，`body` 的字体大小是其他元素的基准

`rem` 是以 `html` 元素的 `font-size` 为基准

`normal` 恢复默认

只用 `bold` 和 `normal` 这两个值

`text-intend: 2em;` `letter-spacing: 1em;`  `word-spacing`

####三栏滑动布局

三栏容器与两栏容器。给两栏容器以负 `margin-right` 和 `width: 100%;float:left` 

`display: table-cell` ie8+

####响应式布局

`<meta name="viewport" content="width=device-width;maximumscale=1.0" />`
