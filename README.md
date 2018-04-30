
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

### 对比 Vue.js React 和 Angular.js

按照我目前的理解，不管是在写 React，还是 Vue.js 还是 Angular.js 也好，感觉都差不多的，我都会遵循两个思想就是数据驱动和组件化。这两种思想是跟随着 React 发展起来的。数据驱动就是我们可以通过一个 state 然后经过一系列变换得到一个 UI 界面。这个 state 是响应式的，改变 state 的时候，UI 界面也会随之改变，这就是数据驱动。组件化的话，我的理解是可以把一个组件就是一个从数据到 UI 的一个映射。数据可以从父组件接受。这就有点函数式编程里面函数的味道。一系列组件放在一起经过一系列的变换就生成了完整的 UI。

React.js 和 Vue 比较的话，大体上是差不多的，都有虚拟 dom，都是组件化和响应式的。差别主要在于一些语法糖，比如 Vue.js 更推崇模版，而 React 更喜欢 jsx 的风格。性能上的话，vue 是自动追踪依赖的变化，判断是否需要渲染组件。react 可能还需要手动优化一下。Vue 还有个优势就是是渐进式的，比较轻量。

Angular.js 的话是元老了，特点是大而全，适合企业级开发。

### vue 数据绑定原理

首先会把模版代码解析为一个 token 序列。然后通过这个序列创建一个 AST 抽象语法树。然后将抽象语法树转为 vnode 树。在这个过程中，使用 with 绑定了当前的运行环境。使用 new Function 动态创建了一个渲染出vnode树的函数，最后将 vnode树 渲染成 dom 树。就完成了一个数据绑定的过程。

双向绑定的原理，主要还是依靠 ES5 object 新增的一个方法 defineProperty 实现的。vue 会遍历组件 data 下个的属性，通过 defineProperty 给他们加上 getter 和 setter。然后在组件渲染的时候，会有一个收集依赖的过程。具体是每个组件都有一个 watcher 实例，组件渲染时会触发属性的 getter，然后在 watcher 里面就会记录下这些依赖项，同时在依赖项里面也会记录上依赖它的 watcher。在设置一个属性值的时候，会调用依赖项的 setter，然后会通知 watcher。watcher 就会调用渲染函数。计算属性也是一个道理，会实例化一个 watcher。然后收集依赖，然后依赖项变化的时候，进行计算。

### 新增 vue 语法

- parse(html)，生成AST节点的时候，往节点附加信息;
- generate(ast)，生成VNode Render时候，加入代码控制运行时流程;
- render.call(vm)，生成VNode树时，提供对应的renderHelpersFunc函数，例如 _c, _v, _s 等;
- patch(vnode)，在真实的dom上处理UI渲染，事件监听等;




