## HTML

### What does a doctype do?

`DOCTYPE` 告诉浏览器要通过哪一种规范解析文档。如果没有给出合法的 `DOCTYPE` 声明，浏览器将以怪异模式（Quirks mode）渲染页面。怪异模式将使用更宽松的方式渲染页面。使用 HTML5 推荐的声明方式 `<!DOCTYPE html>` 可以让包括 IE6 在内的浏览器都启用标准模式渲染页面。

* [DOCTYPE 的作用](http://harttle.land/2016/01/22/doctype.html)
* [MDN: 怪异模式和标准模式](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Quirks_Mode_and_Standards_Mode)
* [W3: DOCTYPE](https://www.w3.org/QA/Tips/Doctype)

### What's the difference between HTML and XHTML?

`XML` 是可扩展标记语言，可以用来存储数据。`HTML`是超文本标记语言，用来展示数据。`XHTML` 是 `XML` 和 `HTML` 的结合，有着比较严格的语法规则，随着 html5 标准的发展，xhtml 已经渐渐被淘汰了。

* [MDN: XML](https://developer.mozilla.org/zh-CN/docs/XML_介绍)
* [MDN: HTML](https://developer.mozilla.org/zh-CN/docs/Web/HTML)
* [MDN: XHTML](https://developer.mozilla.org/zh-CN/docs/XHTML)
* [知乎: XML,HTML,XHTML 之间的关系](https://www.zhihu.com/question/19818208)

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

* [MDN: HTML5](https://developer.mozilla.org/zh-CN/docs/Web/Guide/HTML/HTML5)

### Describe the difference between a cookie, sessionStorage and localStorage.

它们都可以存储数据，`cookie` 容量小，可以通过 `http` 请求发送和设置，可以跨域发送，可以设置过期时间。 `localStorage` 容量大，不会随请求发送，永久储存。 `sessionStorage` 在标签页关闭后清除，不可以跨标签。

* [MDN: http cookie](https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Cookies)
* [MDN: storage](https://developer.mozilla.org/zh-CN/docs/Web/API/Storage)

### Describe the difference between `<script>`, `<script async>` and `<script defer>`.

* `<script>` 会暂停 html 解析，script 被下载并且立即执行，所以一般放在 html 文件末尾。
* `<script async>` 表示脚本可以异步执行，在 script 下载的时候 html 解析不会被暂停，适用于没有依赖关系的独立文件。（使用 document.createElement 创建的 script 默认是异步的）
* `<script defer>` 表示脚本需要延迟执行，会被放在 html 完全解析后执行。通常将 script 放在末尾也能达到同样的效果。

* [Asynchronous vs Deferred JavaScript](https://bitsofco.de/async-vs-defer/)
* [async vs defer attributes](http://www.growingwiththeweb.com/2014/02/async-vs-defer-attributes.html)
* [浏览器的渲染：过程与原理](https://zhuanlan.zhihu.com/p/29418126)

### Why is it generally a good idea to position CSS `<link>s` between `<head></head>` and JS `<script>s` just before `</body>`? Do you know any exceptions?

`<link>` 放在 `<head>` 里面是 html 的规范。大概是因为 html 在解析的时候，需要样式表。`<script>` 标签放在`</body>` 前面是因为 `<script>` 将会停止 html 解析，直到 script 执行完毕。

* [浏览器工作原理](https://www.html5rocks.com/zh/tutorials/internals/howbrowserswork/#The_order_of_processing_scripts_and_style_sheets)
* [性能优化建议](https://developer.yahoo.com/performance/rules.html)
* [从 chrome 源码，查看浏览器渲染进程](https://zhuanlan.zhihu.com/p/30558018)

### Why you would use a srcset attribute in an image tag? Explain the process the browser uses when evaluating the content of this attribute.

srcset 可以使 img 标签，在不同的分辨率或者不同尺寸的屏幕下，提供与之相适应的图片。而如果通过 css 或者 js 实现会有个预加载的过程，体验并不好。（sizes 媒体查询）

* [怎样创建自适应的图片](https://developer.mozilla.org/zh-CN/docs/Learn/HTML/Multimedia_and_embedding/Responsive_images)

### Have you used different HTML templating languages before?

pug，lodash template，Handlebars，artTemplate 等等。在 vue，angular，react 大行其道的今天，我们已经不太需要使用模版引擎了，简单使用的话，直接用 es6 的模版字符串代替了。

### 模版引擎实现原理

大概是用正则表达式替换，用 new Function 将字符串解析成函数

* [知乎：实现一个前端模板引擎](https://zhuanlan.zhihu.com/p/26269716)
* [只有20行Javascript代码！手把手教你写一个页面模板引擎](http://blog.jobbole.com/56689/)

### 如何实现浏览器内多个标签页之间的通信?

使用 `localStorage`，`localStorage` 改变时会触发一个 `storage` 事件，通过监听该事件可以实现多个标签之间的通信。github 就是采用这种方式，localStorage 里有一个值标记是否登录，然后当登录状态改变时，这个值会改变，然后触发 storage 事件，然后就可以进行操作了。源码是：

```
    window.addEventListener('storage', function(n) {
    if (n.storageArea === localStorage && 'logged-in' === n.key && n.newValue !== a) {
        a = n.newValue
        var r = (0, t.query)(document, '.js-stale-session-flash')
        r.classList.toggle('is-signed-in', 'true' === a),
        r.classList.toggle('is-signed-out', 'false' === a),
        r.classList.remove('d-none'),
        window.addEventListener('popstate', function(e) {
            null != e.state.container && location.reload()
        }),
        (0, e.on)('submit', 'form', function(e) {
            e.preventDefault()
        })
    }
    })
```

此外，也可以通过轮询cookie，或者 webSocket，SharedWorker。

* [MDN: 通过 StorageEvent 响应存储的变化](https://developer.mozilla.org/zh-CN/docs/Web/API/Web_Storage_API/Using_the_Web_Storage_API#通过_StorageEvent_响应存储的变化)
* [SharedWorker](https://developer.mozilla.org/zh-CN/docs/Web/API/SharedWorker)
* [编写 WebSocket 客户端应用](https://developer.mozilla.org/zh-CN/docs/Web/API/WebSockets_API/Writing_WebSocket_client_applications)
* [HTTP cookies](https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Cookies)

### 页面可见性（Page Visibility API） 可以有哪些用途？

可以用来检测是否在后台运行，然后进行优化，暂停更新之类的。

```
var doVisualUpdates = true;

document.addEventListener('visibilitychange', function(){
  doVisualUpdates = !document.hidden;
});

function update() {
  if (!doVisualUpdates) {
    return;
  }
  doStuff();
}
```

* [Background Tabs in Chrome 57](https://developers.google.cn/web/updates/2017/03/background_tabs?hl=pt-br)

### HTML5的离线储存

使用 ServiceWorker 和 Cache Storage 缓存页面

* [google: 第一个pwa](https://codelabs.developers.google.com/codelabs/your-first-pwapp/#8)
* [github: 使用 service worker 离线访问](https://github.com/facebook/create-react-app)
* [MDN: Progressive Web Apps\(PWA\)](https://developer.mozilla.org/zh-CN/Apps/Progressive)

### What is progressive rendering?

渐进式渲染是一系列用于提高用户对页面加载的感知的技术。关键在于逐步呈现内容，让用户看到屏幕上的东西正在不停的增量加载，而不是给个白屏。可以用以下技术进行优化：

* 延迟图像的加载
* 将可见的内容分模块，按优先级加载
* 异步插入 html
* 提供一个骨架页面
* 使用 service worker 缓存页面

* [Async Fragments: Rediscovering Progressive HTML Rendering with Marko](https://www.ebayinc.com/stories/blogs/tech/async-fragments-rediscovering-progressive-html-rendering-with-marko/)
* [淘宝首页性能优化实践](https://github.com/wagnlinzh/wagnlinzh.github.io/wiki/淘宝首页性能优化实践)
* [饿了么的 PWA 升级实践](https://huangxuan.me/2017/07/12/upgrading-eleme-to-pwa/)
* [Reactive Web Design: The secret to building web apps that feel amazing](https://medium.com/@owencm/reactive-web-design-the-secret-to-building-web-apps-that-feel-amazing-b5cbfe9b7c50)
* [Progressive Rendering: A killer \(and under appreciated?\) feature of the Web](https://medium.com/ben-and-dion/progressive-rendering-a-killer-and-under-appreciated-feature-of-the-web-97c789b608c1)
* [google: PWA 入门](https://developers.google.cn/web/updates/2015/12/getting-started-pwa)
* [google: APP Shell](https://developers.google.cn/web/fundamentals/architecture/app-shell?hl=zh-cn)
* [google: Web App manifest](https://developers.google.cn/web/fundamentals/web-app-manifest/?hl=zh-cn)

### 介绍一下你对浏览器内核的理解？

浏览器内核主要是指浏览器的渲染引擎，负责解析 HTML 和 CSS 内容，并将解析后的内容显示在屏幕上。现在的渲染引擎主要有：webkit，blink，事实标准。

* [浏览器的工作原理](https://www.html5rocks.com/zh/tutorials/internals/howbrowserswork/#The_browser_high_level_structure)
* [browser refarch](http://grosskurth.ca/papers/browser-refarch.pdf)

### html 标签

在 `HTML4` 中只有 inline 和 block 的区别，在 `HTML5` 标准中没有这种说法了，HTML5 中元素大致被分为七大类：

* Metadata，如：link, meta, script, style
* Flow，除了少数 metadata 元素以外的大部分元素都是 metadata
* Sectioning，如：article, aside, nav, section
* Heading，标题元素，h1，h2，h3...
* Phrasing，\(if it can be inside a sentence, it's phrasing content.\)，可以理解为行内元素，如 span, img, i
* Embedded，嵌入外部资源的元素，audio, video, img, canvas, svg, iframe
* Interactive，所有与用户交互有关的元素，包括a, input, textarea, select

根据以上分类， HTML5 还规定了每个元素的内容模型\(content model\)，就是指对于该元素来说合法的子元素类型。

* [MDN: content categories](https://developer.mozilla.org/zh-CN/docs/Web/Guide/HTML/Content_categories)
* [元素分类与内容模型](http://blog.shaochuancs.com/w3c-html5-content-model/)
* [知乎：a 标签为什么能够包含块级元素？](https://www.zhihu.com/question/34952563)
* [stackoverflow：What is the difference between phrasing content and flow content?](https://stackoverflow.com/questions/30233447/what-is-the-difference-between-phrasing-content-and-flow-content)
* [HTML5 标准：kinds of content](https://html.spec.whatwg.org/multipage/dom.html#kinds-of-content)

### 简述一下你对HTML语义化的理解?

语义化的核心在于让机器能够理解内容。html 语义化让内容用更合理的语义表述出来，减少了机器处理的难度。带来的好处是，利于seo，便于开发。

* [如何理解 Web 语义化？](https://www.zhihu.com/question/20455165)



# CSS

* [What is the difference between classes and ID's in CSS?](#what-is-the-difference-between-classes-and-ids-in-css)
* [What's the difference between "resetting" and "normalizing" CSS? Which would you choose, and why?](#whats-the-difference-between-resetting-and-normalizing-css-which-would-you-choose-and-why)
* [CSS 选择器有那些](#CSS-选择器有那些)
* [What is CSS selector specificity and how does it work?](#what-is-css-selector-specificity-and-how-does-it-work)
* [层叠规则](#层叠规则)
* [浮动](#浮动)
* [外边距折叠](#外边距折叠)
* [BFC](#BFC)
* [外边距折叠](#外边距折叠)
* [IFC](#IFC)
* [Explain your understanding of the box model and how you would tell the browser in CSS to render your layout in different box models.](#explain-your-understanding-of-the-box-model-and-how-you-would-tell-the-browser-in-css-to-render-your-layout-in-different-box-models)
* [包含块](#包含块)
* [position](#position)
* [z-index](#z-index)
* [层叠上下文](#层叠上下文)
* [Relationships between display, position, and float](#relationships-between-display-position-and-float)
* [display](#display)
* [inline-block](#inline-block)
* [雪碧图](#雪碧图)
* [如何解决不同浏览器的样式兼容性问题？](#如何解决不同浏览器的样式兼容性问题？)
* [你使用过栅格系统吗？偏爱哪一个](#你使用过栅格系统吗？偏爱哪一个)
* [媒体查询](#媒体查询)
* [CSS 打印](#CSS-打印)
* [编写高效的 CSS 应该注意什么](#编写高效的-CSS-应该注意什么？)
* [使用 CSS 预处理的优缺点分别是什么？](#使用-CSS-预处理的优缺点分别是什么？)
* [解释浏览器如何确定哪些元素与 CSS 选择器匹配](#解释浏览器如何确定哪些元素与-CSS-选择器匹配)
* [伪元素和伪类](#伪元素和伪类)
* [你有没有使用过视网膜分辨率的图形？当中使用什么技术？](#你有没有使用过视网膜分辨率的图形？当中使用什么技术？)
* [什么情况下，用translate\(\)而不用绝对定位？什么时候，情况相反。](#什么情况下，用translate而不用绝对定位？什么时候，情况相反。)
* [li与li之间有看不见的空白间隔是什么原因引起的？有什么解决办法？](#li与li之间有看不见的空白间隔是什么原因引起的？有什么解决办法？)
* [postcss](#postcss)
* [@import 和 link 的区别](#import-和-link-的区别)
* [png、jpg、gif 这些图片格式解释一下，分别什么时候用。有没有了解过 webp？](#png、jpg、gif-这些图片格式解释一下，分别什么时候用。有没有了解过-webp？)

## TODO:

* css 的值和单位

## What is the difference between classes and ID's in CSS?

ID：唯一性、设置锚点、特异性差别、DOM 方法。

---

ID 具有唯一性，每个元素只能有一个id，每个页面只能有一个有该 ID 的元素。class 不是唯一的，可以在同一个元素上使用多个类，也可以在多个元素上使用相同的类。对于 CSS 来说 ID 和 class 只有权重的区别。对于 html 来说，ID 可以用来设置锚点。 JS 有专门获取特定 ID 元素的方法。

---

> [CSS Trick: The Difference Between ID and Class](https://css-tricks.com/the-difference-between-id-and-class/)

## What's the difference between "resetting" and "normalizing" CSS? Which would you choose, and why?

reset 删除所有的默认样式；是为了删除所有浏览器默认的样式，normalizing 目的是为了让所有浏览器样式保持一致，并且会修复某些浏览器 BUG

---

虽然使用 normalize css 更科学，更温和。但是实际开发的情况是需要根据设计稿和原型来的，normalize css 定义的 css 几乎都是没用的，反而还会造成困扰和多余麻烦。

---

> [What is the difference between Normalize.css and Reset CSS?](https://stackoverflow.com/questions/6887336/what-is-the-difference-between-normalize-css-and-reset-css/6896881#6896881)

## CSS 选择器有那些

基本选择器：

* 通配符选择器（Universal Selectors）：\*
* **命名空间选择器（Namespaces in Elemental Selectors）：ns\|E**
* ID 选择器（ID selector）: \#id
* 属性选择器（Attribute selectors）：\[att=val\]
* 类选择器（Class Selectors）：等价于\[class~=identifier\]
* 伪类选择器（pseudo-class）：E:hover，E:not\(s1, s2\)，E:checked
* 类型选择器（Tag Selectors）：div，p，span
* 伪元素选择器

复合选择器有：

* 后代选择器：E F
* 子选择器：E &gt; F
* 相邻兄弟选择器：E + F
* 一般兄弟选择器：E ~ F
* 网格选择器：F \|\| E，E:nth-col\(n\)

---

> [W3C: selector](https://www.w3.org/TR/selectors-4/#structure)  
> [MDN: CSS selectors](https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_Selectors)

## What is CSS selector specificity and how does it work?

计算规则是：

* style 的优先级（specificity）最高
* 计算 ID 选择器的个数
* 计算类选择器，属性选择器，伪类选择器的个数
* 计算类型选择器和伪元素选择器的个数
* 忽略通用选择器

选择器器的优先级会用来计算层叠值

---

!important 层叠值来源和重要程度的规则。

---

> [W3C: specificity rules](https://www.w3.org/TR/selectors-4/#specificity-rules)  
> [W3C: style 的规则](https://www.w3.org/TR/CSS21/cascade.html#specificity)  
> [MDN: 优先级](https://developer.mozilla.org/zh-CN/docs/Web/CSS/Specificity)

## 层叠规则

层叠是CSS的一个基本特征，它定义了如何合并来自多个源的属性值的算法。一个元素的其中一个属性的实际值的计算规则是：

* 首先会计算层叠规则产生的值（cascaded value），层叠值是由来源和是否是important，作用域（scope），特异性（specificity），定义顺序来决定的。来源的优先级如下：
  * Transition declarations
  * Important user agent declarations
  * Important user declarations
  * Important override declarations
  * Important author declarations
  * Animation declarations
  * Normal override declarations
  * Normal author declarations
  * Normal user declarations
  * Normal user agent declarations
* 然后得到指定值（specified value），如果层叠值存在则是层叠值，否则是继承过来值，如果都没有则是默认的值。
* 然后得到计算值（computed Value），计算值主要是用于继承的值，通常是绝对值。（float 会改变 display 的计算值为 block）
* 然后得到应用值（used value），应用值是完成所有计算后最终使用的值，如 width: auto。是布局的理论值。
* 然后得到实际布局的值（actual value），浏览器实际渲染出来的值。

---

> [W3C：Cascading](https://www.w3.org/TR/css3-cascade/#cascading)

## 浮动

* 在 CSS2.1 中，浮动属于 3 种定位方案中的一种。（常规流（normal flow）和绝对定位）
* 设置浮动效果时，元素会向左或者向右移动，直到碰到包含块的边框，或者另外一个浮动元素为止。
* 清除浮动有两种方案：一种是使用clear，通常的做法是添加一个 有 clear 属性的`after` 伪元素。第二种方案是创建一个块级格式化上下文（BFC），隔离浮动带来的影响，这种做法有很多，设置 overflow，浮动父元素，设置 display: flow-root 之类的，具体情况具体分析。
* 浮动会使改变display的计算值为block，（绝对定位也有这种特性）。
* 浮动会缩短行框（line boxes），如果宽度不足以容下行框，行框会下移直到没有遇到浮动元素为止。

---

> [MDN: float](https://developer.mozilla.org/zh-CN/docs/CSS/float)  
> [MDN: 视觉格式化模型](https://developer.mozilla.org/zh-CN/docs/Web/Guide/CSS/Visual_formatting_model)  
> [W3C: intro to floats](https://drafts.csswg.org/css-box-3/#intro-to-floats)

## BFC

* float、overflow、绝对定位、表格单元格、FLEX 的子元素，都能生成 BFC。还可以显式的设置 display: flow-root
* 在 CSS2.1 中，一个在常规流中的框，要么属于 BFC，要么属于 IFC。
* 块级框参与块级格式化上下文。块级框会从包含块的顶部开始一个一个垂直的向下摆放，在同一个BFC里面，相邻的块级框会发生外边距折叠。
* 创建 BFC 的框叫做 flow root，初始包含块就是初始流的 flow root。一个框可以直接设置 display 属性为 flow-root，为这个框的子元素生成了一个块级格式化上下文。
* 属于不同 BFC 的元素，是互不影响的。flow root 框的高度计算会包括它里面浮动的子元素（所以可以清除浮动）。外边距叠加在不同的 BFC 里面是不会发生的。

---

> [W3C: FLOW](https://drafts.csswg.org/css-box-3/#flows)  
> [W3C: block formatting](https://www.w3.org/html/ig/zh/wiki/CSS2/visuren#block-formatting)  
> [MDN: 块格式化上下文](https://developer.mozilla.org/zh-CN/docs/Web/Guide/CSS/Block_formatting_context)  
> [Understanding Block Formatting Contexts in CSS](https://www.sitepoint.com/understanding-block-formatting-contexts-in-css/)

## 外边距折叠

外边距折叠条件：

* 处于同一个[块级格式化上下文](#BFC)
* 同属于常规流
* 垂直方向上相邻的两个或以上的块级框

满足这些条件的外边距会折叠成值最大的那个。

---

这些条件意味着

* BFC 内部元素不会和外部元素发生折叠，因为它们没有处在同一块级格式化上下文\]。 Flex 内部元素不会折叠，因为 Flex 不属于块级格式化上下文
* float 和 absolute 不会折叠，因为不属于常规流
* inline-block 不会折叠，因为它也不属于 flow

---

> [W3C: collapsing margins](https://www.w3.org/html/ig/zh/wiki/CSS2/box#collapsing-margins)

## IFC

* 在 CSS2.1 中，IFC 和 BFC 一样是常规流的两种基本布局方式。
* 框会从包含块的顶部开始，一个接一个地水平摆放，它们在水平方向上的外边距、边框、内边距会被保留。
* 行内级框参与行内格式化上下文。垂直方向上默认通过基线对齐。行内级框分为行内框和原子行内级框。行内框的高度就是 line-height，原子行内框是高度是自身的高度加上边距。
* 浏览器会自动生成行框，包裹 IFC 的一行。行框的高度就是一行的高度。是行内级盒根据 vertical-align 对齐之后撑开的。所以至少也是 line-height。基线对齐时，不同的行内级框会有错位的情况，导致行框变高。使用 vertical-align: top, bootom 可以修复。

---

> [MDN：line-height](https://developer.mozilla.org/zh-CN/docs/Web/CSS/line-height)  
> [W3C：行高计算](https://www.w3.org/html/ig/zh/wiki/CSS2/visudet#line-height)  
> [W3C：行内格式化上下文](https://www.w3.org/html/ig/zh/wiki/CSS2/visuren#inline-formatting)  
> [w3cplus：深入了解CSS字体度量，行高和vertical-align](https://www.w3cplus.com/css/css-font-metrics-line-height-and-vertical-align.html)

## Explain your understanding of the box model and how you would tell the browser in CSS to render your layout in different box models.

每一个元素都是一个矩形框。类型大致有：

* 块级框（block-level box），参与块格式化上下文的元素
* 块容器框（block container box），只包含其他块级盒，或创建一个行内格式化上下文。
* 块框（block boxes），同时是块级框和块容器框。
* 匿名块框（Anonymous block boxes），块格式化上下文中浏览器自动生成的框。
* 行内级框（inline-level boxes），参与行内格式化上下文的元素。
* 行内框\(inline boxes\)，display inline 的非替换元素。
* 原子行内级盒（atomic inline-level boxes），可替换行内元素，inline-block。
* 匿名行内框（Anonymous inline boxes），自动生成的。
* 行框（Line boxes），行内格式化上下文产生的，用来包裹一行。

框的特性：

* 每个框都有一个内容，padding，border，margin区域。处在同一块级格式化化上下文中的框有可能会发生外边距折叠。
* box-sizing 可以设置计算框宽高的方式，content-box 不包含 padding 和 border。padding-box 包含。
* 很多框的尺寸和位置都取决[包含块](包含块)。
* CSS2 中，框有3种定位体系，常规流，浮动和绝对定位。

---

> [MDN：视觉格式化模型](https://developer.mozilla.org/zh-CN/docs/Web/Guide/CSS/Visual_formatting_model)  
> [W3C：视觉格式化模型](https://www.w3.org/html/ig/zh/wiki/CSS2/visuren#box-gen)  
> [W3C：宽高计算](https://www.w3.org/html/ig/zh/wiki/CSS2/visudet#Computing_widths_and_margins)  
> [W3C：框模型](https://www.w3.org/html/ig/zh/wiki/CSS2/box)  
> [W3C: box sizing](https://developer.mozilla.org/zh-CN/docs/Web/CSS/box-sizing)  
> [W3C: 框模型](https://developer.mozilla.org/zh-CN/docs/Web/CSS/CSS_Box_Model/Introduction_to_the_CSS_box_model)  
> [Understand the CSS Box Model](https://www.smashingmagazine.com/2010/06/the-principles-of-cross-browser-css-coding/#understand-the-css-box-model)

## 包含块

* 许多框的尺寸和位置都取决于包含块。
* 根元素存在的包含块，被叫做初始包含块。
* position 的值为 static 或 relative 的包含块是最近的是块容器盒的父元素的内容区的边界。
* position 的值为 fixed 的元素的包含块是 viewport 视口。
* position 的值为 absolute 的包含块是最近的 position 不为 static 的元素的 padding 的边界。
* **poistion fixed absolute 的包含块还有可能是设置了 transform 或 perspective，或者 will-change 的值是 transform 或 perspective 的最近父元素的 padding 的边界**

---

> [MDN：包含块](https://developer.mozilla.org/zh-CN/docs/Web/CSS/All_About_The_Containing_Block)  
> [W3C：包含块](https://www.w3.org/html/ig/zh/wiki/CSS2/visudet#containing-block-details)

## position

* position 分为两类，处于常规流的 static 和 relative，relative 可以设置相对原位置偏移。
* absolute 和 fixed 相对于[包含块](#包含块)定位
* sticky 没有超过设置的阈值时表现的像 relative，超过了像 fixed。

---

> [MDN：position](https://developer.mozilla.org/zh-CN/docs/Web/CSS/position)

## z-index

对于一个定位框，z-index 指定：

* 元素在当前层叠上下文中的层叠层级
* 元素是否创建一个新的本地堆叠上下文
* z-index 的值只是在同一个层叠上下文内比较才是有意义的

---

> [MDN：z-index](https://developer.mozilla.org/zh-CN/docs/Web/CSS/z-index)

## 层叠上下文

* 在 CSS2.1 中，一个框有三个维度的定位，水平，垂直和 z 轴。元素在 z 轴上的顺序就是层叠上下文。渲染树会层叠上下文的顺序，依次在屏幕上绘制元素。
* 在同一个层叠上下文的顺序是：
  * 背景和边框
  * 负的 z-index
  * 属于常规流的块级框
  * 浮动
  * 行内级框
  * z-index 0，或者不依赖 z-index 的层叠上下文
  * 正的 z-index
* 有些条件会创建一个新的层叠上下文
  * 根元素
  * z-index 不为 auto 的绝对/相对定位元素
  * opacity
  * transform
  * perspective
  * filter
  * will-change
  * flex 的 z-index 不为 auto 的子元素
* 不同的层叠上下文之间是独立的，相互不影响。z-index 的比较只在同一个层叠上下文中才有意义

---

> [MDN：层叠上下文](https://developer.mozilla.org/zh-CN/docs/Web/Guide/CSS/Understanding_z_index/The_stacking_context)  
> [W3C：分层显示](https://drafts.csswg.org/css-position-3/#layered-presentation)  
> [What No One Told You About Z-Index](https://philipwalton.com/articles/what-no-one-told-you-about-z-index/)

## Relationships between display, position, and float

* 首先，display 为 none，不生成框。position，float 不生效
* 定义了 position 和 float 的框是块状的。display 的计算值大部分情况是 block
* 定义了 position 的框，float 的计算值为 none。

---

> [W3C：Relationships between display, position, and float](https://www.w3.org/TR/css-position-3/#dis-pos-flo)

## display

有 inline block inline-block，list 相关 list-item 等， table 相关，flex，grid。

---

> [MDN：display](https://developer.mozilla.org/zh-CN/docs/Web/CSS/display)

## inline-block

inline-block 表现的像一个可替换元素。是块容器框也是原子行内级框。

---

> [MDN：display](https://developer.mozilla.org/zh-CN/docs/Web/CSS/display)

## 雪碧图

雪碧图是把多张图片整合到一张上的图片。原理是 background-position，**可以提前加载资源**，减少 HTTP 请求。使用 gulp webpack 工具自动生成。

---

> [css sprites](https://css-tricks.com/css-sprites/)

## 如何解决不同浏览器的样式兼容性问题？

* 使用 css 库
* 使用 sass less，postcss 解决前缀问题
* 使用 reset normalize
* 通过样式的层叠使用回退机制
* 特性检测，@supports 或者 modernizr

## 你使用过栅格系统吗？偏爱哪一个

使用 flex 实现，更规范方便使用

> [css tricks：flex](https://css-tricks.com/snippets/css/a-guide-to-flexbox/)  
> [MDN: flex](https://developer.mozilla.org/zh-CN/docs/Learn/CSS/CSS_layout/Flexbox)

## 媒体查询

* 媒体类型主要有 screen 和 print
* 媒体查询可以查询的特性主要有，宽，高，宽高比，横屏还是竖屏还有是否 retina 屏。
* link 标签里面 media 属性可以设置媒体查询条件，为 false 时，样式不会应用，但同样会被下载。

---

> [MDN：CSS 媒体查询](https://developer.mozilla.org/zh-CN/docs/Web/Guide/CSS/Media_queries)  
> [MDN：媒体查询](https://developer.mozilla.org/zh-CN/docs/Web/CSS/媒体查询)  
> [MDN：@media](https://developer.mozilla.org/zh-CN/docs/Web/CSS/@media)

## CSS 打印

media print，@page，page-break

---

> [Print —— 被埋没的Media Type](http://cdc.tencent.com/2014/08/19/print-被埋没的media-type/)

## 编写高效的 CSS 应该注意什么？

* **减少选择器的复杂度**：使用 BEM（ Block Element Modifier） 风格的命名法写 CSS。可以减少选择器的复杂度，减少嵌套。
* 渲染树绘制成像素有可能经过三个阶段，布局（layout）、绘制（paint）、合成（composite）。可以从这三个阶段入手优化性能：
  * 布局是浏览器计算各元素几何信息的过程。使用 Flex 布局，性能更好。先读取值，然后再应用样式。（避免强制布局和布局抖动）
  * 绘制是填充像素的过程。除 transform 或 opacity 属性之外，更改任何属性始终都会触发绘制。可以通过提升层级减少绘制的区域。
  * 合成是将页面的已绘制部分放在一起以在屏幕显示的过程。使用 transform 和 opacity 只触发合成。合成器有很多层级，每一都会有内存和gpu管理。

---

> [淘宝：无线性能优化](http://taobaofed.org/blog/2016/04/25/performance-composite/)  
> [google：渲染性能](https://developers.google.com/web/fundamentals/performance/rendering/)

## 使用 CSS 预处理的优缺点分别是什么？

优点：

* 提高 CSS 可维护性。
* 易于编写嵌套选择器。
* 引入变量，增添主题功能。可以在不同的项目中共享主题文件。
* 通过混合（Mixins）生成重复的 CSS。
* 模块化。不进行预处理的 CSS，虽然也可以分割成多个文件，但需要建立多个 HTTP 请求加载这些文件。

缺点：

* 需要预处理工具。
* 重新编译的时间可能会很慢。

原生的 CSS 已经可以实现变量，calc，color 等功能。具有动态性。

## 解释浏览器如何确定哪些元素与 CSS 选择器匹配

CSS 有 CSSOM 处理继承层叠问题。从右向左，向上遍历。

---

> [浏览器原理](https://www.html5rocks.com/zh/tutorials/internals/howbrowserswork/#Manipulating_the_rules_for_an_easy_match)  
> [Why do browsers match CSS selectors from right to left?](https://stackoverflow.com/questions/5797014/why-do-browsers-match-css-selectors-from-right-to-left)

## 伪元素和伪类

伪元素表现的像一个元素，伪类表现的像一个类。有没有创建一个文档树之外的元素

---

> [伪元素和伪类](http://www.alloyteam.com/2016/05/summary-of-pseudo-classes-and-pseudo-elements/)

## 你有没有使用过视网膜分辨率的图形？当中使用什么技术？

img srcset，媒体查询。

## 什么情况下，用translate\(\)而不用绝对定位？什么时候，情况相反。

transform 只触发合成，性能好。

---

> [坚持仅合成器的属性和管理层计数](https://developers.google.com/web/fundamentals/performance/rendering/stick-to-compositor-only-properties-and-manage-layer-count)

## li与li之间有看不见的空白间隔是什么原因引起的？有什么解决办法？

使用负 margin，使用 flex, font-size 0。压缩去除空格。

## 负margin

top 或者 left 会被拉。bottom, right 后面元素会被拉。如果没有设置宽度，左右拉，填充宽度。

> [The Definitive Guide to Using Negative Margins](https://www.smashingmagazine.com/2009/07/the-definitive-guide-to-using-negative-margins/)

## postcss

PostCSS 提供了一个解析器，它能够将 CSS 解析成抽象语法树

## @import 和 link 的区别

@import 导入的样式会在页面加载完再下载。 @import 和 link 属于不同的标准。

## png、jpg、gif 这些图片格式解释一下，分别什么时候用。有没有了解过 webp？

* png 无损的，效果比较好，比较大
* jpg 有损压缩，比较小，效果好
* gif 会动
* wbep 无损，效果好，会动。



