
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

加载性能，主要可以从优化关键渲染路径入手。

优化加载的内容：首先是减少不必要的资源，不该放的可以不放，用 css3 代替图片，字体可以用点手段提取必要的字体，响应式图片，媒体查询css。其次是压缩，将 HTML，CSS, JS 压缩成最小，然后开启GZIP压缩，HTTP2 压缩标头，图片可以压缩，使用 webp。

提高加载的速度

