##onerror

window.onerror 捕获所有异常

document.onerror

image.onerror

script.onerror (如何确定 load 状态 onreadystatechange ?)

xhr.onerror(网络失败)

websocket.onerror



##各种onload, onerror, onreadystatechage

#####window

`window.onload` 全支持

`window.onerror` 捕获所有异常

#####document

`document.addEventListener('DOMContentLoaded', func)`

`document.onreadystatechange` `document.readyState === 'interactive' or 'complete'`

#####script

`script.onload` 非 ie

`script.onreadystatechange`  `script.readyState === 'loaded' or 'complete'` ie

没有 `onerror`，需要定时检测

#####image

`image.onload` `image.onerror` 全支持



## object.create 与 object.assign

## cdn prefetch 是什么
