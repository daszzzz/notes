
## javascript

### js 里面有那些基本类型

js 的基本类型分为两种，原始类型和 `object`。

原始类型有：`number` 数字，`string` 字符串，`undefined`，`null`，`symbol`, `boolean`，以及 es6 新增的符号类型 `symbol`。

### js 中什么类型是引用传递, 什么类型是值传递? 如何将值类型的变量以引用的方式传递?

对于原始类型 js 是按值传递的。对于复杂类型是按地址值复制一份，然后按地址值传递。

### 类型判断

一般可以使用 `Object.prototype.call.toString` 判断，用 `instanceof` 和 `constructor` 都存在一个问题，就是跨 iframe 的时候，由于不同宿主环境内置对象不是同一个，所以通过 `instanceof` 和 `constructor` 判断时会出错。js 是弱类型语言，大型项目里面，可以使用 flow，typescript

### 作用域

js 是词法作用域，也就是静态作用域，


## 工程化

### 前端性能优化

前端性能主要包含两个方面：加载性能，和渲染性能。

加载性能，首先可以从减少需要加载的内容做起，不该放的可以不放，用 css3 代替图片，字体可以用点手段提取必要的字体，响应式图片，媒体查询css。

然后是减少资源的大小，可以将 HTML，CSS, JS 压缩成最小，然后开启GZIP压缩，HTTP2 压缩标头，图片可以压缩，使用 webp。

然后可以从关键渲染路径着手，优化加载顺序，第三方的js，可以 async， defer。js 放后面避免阻塞加载，css 放前面。可以使用 link preload，提升资源的优先级比如字体。一般情况下加载字体的优先级是很低的。 类似的还可以使用 preconnect 链接另外一个页面，提前处理 dns 查找和重定向的步骤。还有 prefetch，空闲时候链接。使用 HTTP2，优先加载重要资源。

缩短下载时间，可以使用 HTTP2 的服务器推送的技术。上 CDN，资源合并成一个文件，减少 http 请求，或者上 http2。

使用渐进式渲染，css，js 分模块，异步加载。使用 APP SHELL 模型，提供一个骨架页面，service worker 缓存。图片也是异步加载。异步渲染页面。

使用缓存，根据文件名的 hash 值判断过期，本地存储，indexDB，cache api。

还有渲染性能主要就是减少 js到样式渲染到布局到绘制到合成这一步骤。


提高加载的速度

