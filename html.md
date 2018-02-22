### What does a doctype do?

`DOCTYPE` 告诉浏览器要通过哪一种规范解析文档。如果没有给出合法的 `DOCTYPE` 声明，浏览器将以怪异模式（Quirks mode）渲染页面。怪异模式将使用更宽松的方式渲染页面。使用 HTML5 推荐的声明方式 `<!DOCTYPE html>` 可以让包括 IE6 在内的浏览器都启用标准模式渲染页面。

* [DOCTYPE 的作用](http://harttle.land/2016/01/22/doctype.html)
* [MDN: 怪异模式和标准模式](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Quirks_Mode_and_Standards_Mode)
* [W3: DOCTYPE](https://www.w3.org/QA/Tips/Doctype)

### What's the difference between HTML and XHTML?

`XML` 是可扩展标记语言，可以用来存储数据。`HTML`是超文本标记语言，用来展示数据。`XHTML` 是 `XML` 和 `HTML` 的结合，有着比较严格的语法规则，随着 html5 标准的发展，xhtml 已经渐渐被淘汰了。

*  [MDN: XML](https://developer.mozilla.org/zh-CN/docs/XML_%E4%BB%8B%E7%BB%8D)
*  [MDN: HTML](https://developer.mozilla.org/zh-CN/docs/Web/HTML)
*  [MDN: XHTML](https://developer.mozilla.org/zh-CN/docs/XHTML)
*  [知乎: XML,HTML,XHTML 之间的关系](https://www.zhihu.com/question/19818208)

### How do you serve a page with content in multiple languages?

浏览器会自动设置请求头 `Accept-Language` 告诉服务器需要的自然语言。一般来说可以通过指定的 url 获取特定的语言版本。对于前端来说，vue、angular、react 之类的框架，或者一些模版引擎，都有一些工具库能帮助我们实现国际化。

* [w3: language](https://www.w3.org/International/getting-started/language)
* [MDN: accept-language](https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Headers/Accept-Language)
* [Angular: i18n](https://angular.io/guide/i18n)
* [知乎: lang](https://www.zhihu.com/question/20797118)

### What are data- attributes good for?

html5 将标签的自定义属性标准化，通过增加 `data-` 前缀表示这里存储了额外的信息。在 js 中可以通过这个节点的`dataset` 属性可以访问到里面的数据。在各种框架中，一般都不会加上 `data` 前缀。

* [MDN: 使用 `data` 属性](https://developer.mozilla.org/zh-CN/docs/Web/Guide/HTML/Using_data_attributes)
* [html5-custom-data-attributes](http://html5doctor.com/html5-custom-data-attributes/)

### Consider HTML5 as an open web platform. What are the building blocks of HTML5?

`HTML5` 即是指新一代的 `HTML` 语言标准，也是指一系列的技术的合集。它的特点是: 

    * 语义化：`HTML` 新增加一些语义化的标签，便于搜索引擎和开发人员理解。
    * 连通性： 使用 `websocket` `webRTC` 等技术，能让客户端和服务端更好的通信。
    * 离线 & 存储: 离线存储增加客户端的离线访问功能。
    * 多媒体: `video` `audio`, 直接在网页中嵌入视频和音频。
    * 3D, 图像 & 效果: `canvas` `svg` 可以绘制图像。
    * 性能 & 集成: `webworker` 让网站有更好的性能。
    * 设备访问: 触控事件，地理位置api。
    * 样式: css3

*  [MDN: HTML5](https://developer.mozilla.org/zh-CN/docs/Web/Guide/HTML/HTML5)

### Describe the difference between a cookie, sessionStorage and localStorage.

它们都可以存储数据，`cookie` 容量小，可以通过 `http` 请求发送和设置，可以跨域发送，可以设置过期时间。 `localStorage` 容量大，不会随请求发送，永久储存。 `sessionStorage` 在标签页关闭后清除，不可以跨标签。

* [MDN: http cookie](https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Cookies)
* [MDN: storage](https://developer.mozilla.org/zh-CN/docs/Web/API/Storage)

### Describe the difference between <script>, <script async> and <script defer>.

    * `<script>` 会暂停 html 解析，script 被下载并且立即执行，所以一般放在 html 文件末尾。
    * `<script async>` 表示脚本可以异步执行，在 script 下载的时候 html 解析不会被暂停，适用于没有依赖关系的独立文件。（使用 document.createElement 创建的 script 默认是异步的）
    * `<script defer>` 表示脚本需要延迟执行，会被放在 html 完全解析后执行。通常将 script 放在末尾也能达到同样的效果。 

* [Asynchronous vs Deferred JavaScript](https://bitsofco.de/async-vs-defer/)
* [async vs defer attributes](http://www.growingwiththeweb.com/2014/02/async-vs-defer-attributes.html)
* [浏览器的渲染：过程与原理](https://zhuanlan.zhihu.com/p/29418126)

### Why is it generally a good idea to position CSS <link>s between <head></head> and JS <script>s just before </body>? Do you know any exceptions?

`<link>` 放在 `<head>` 里面是 html 的规范。大概是因为 html 在解析的时候，需要样式表。`<script>` 标签放在`</body>` 前面是因为 `<script>` 将会停止 html 解析，直到 script 执行完毕。

* [浏览器工作原理](https://www.html5rocks.com/zh/tutorials/internals/howbrowserswork/#The_order_of_processing_scripts_and_style_sheets)
* [性能优化建议](https://developer.yahoo.com/performance/rules.html)
* [从 chrome 源码，查看浏览器渲染进程](https://zhuanlan.zhihu.com/p/30558018)
