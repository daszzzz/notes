## CSS

### 垂直居中

垂直居中的话，首先需要分清楚该元素所处于的环境。

如果是在 flex 里面的话，很简单，只需要对元素设置 margin: auto 或者 align-items: center;

如果是处于表格中的话设置 vertical-align: middle; 即可垂直居中。

其他通用的情况可以将元素设置为绝对定位，然后 top 设置为 50%，然后 margin-top: 元素自身高度的一半。或者是使用 transform 将元素往上平移自身高度的 50%。如果是模态框居中的话，可以使用 vh 视口单位，然后往上移动自身高度的一半。

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

### JS 原生实现深拷贝

通常情况下可以通过解析为 json 字符串实现深拷贝，es6 内部其实已经实现了深拷贝方法，叫做结构化克隆算法，这个比 json 序列化能处理更多的问题。在我们使用 history api 和 indexDB  的时候，会自动调用到这种算法。其他情况的话，我会使用一层一层解构赋值实现深拷贝。更复杂的情况就应该写特定的函数了，涉及到原型链闭包的话，不是那么容易搞的。

## http

### HTTP 状态码

1XX 表示接收的请求正在处理，2XX 表示请求正常处理完毕比如200成功、204成功但是没有可以返回的信息，3XX 表示重定向比如301永久性重定向，302临时重定向，304未修改，4XX 表示客户端错误，比如400 错误的请求，403 没有权限，401 未授权，404 找不到资源，5XX 服务器错误，500 服务器错误。

### get 和 post 的区别

最大的区别还是语义上的区别，get 是获取资源，post 是资源进行处理。get 在URL里，可以被缓存，可以添加历史记录，前进后退。

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

## 框架

### 对比 Vue.js React 和 Angular.js

按照我目前的理解，不管是在写 React，还是 Vue.js 还是 Angular.js 也好，感觉都差不多的，我都会遵循两个思想就是数据驱动和组件化。这两种思想是跟随着 React 发展起来的。数据驱动就是我们可以通过一个 state 然后经过一系列变换得到一个 UI 界面。这个 state 是响应式的，改变 state 的时候，UI 界面也会随之改变，这就是数据驱动。组件化的话，我的理解是可以把一个组件就是一个从数据到 UI 的一个映射。数据可以从父组件接受。一个组件就是一个功能，这就有点函数式编程里面函数的味道。一系列组件放在一起经过一系列的变换就生成了完整的 UI。

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

### vuex 

因为 vue 是数据驱动或者说是状态驱动的，通过状态映射成 ui。vuex 就是集中管理状态的一个工具。特点是单向数据流，数据只能通过提交一个 mutation 改变。好处是可以解决组件间的通信问题。大型单页面应用的话，可以便于管理数据和开发维护。

### 虚拟 DOM

首先有一个 vnode 的类，这个类里面记录着一个 node 节点，它的标签名，子节点和一些属性的信息。虚拟 DOM 就是一个 vnode 组成的树。vnode 树可以被渲染成 DOM 树。由于 dom 创建一个元素的开销比较大，所以在将老的 vnode 树替换成新的 vnode 树的过程涉及到一个 diff 的过程，只更新修改部分的 dom。

这个 diff 过程的核心在于只比较同层的节点。比较同层的一组节点过程是互相比较它们的首尾指针看是否一致，然后移动指针。如果存在key的话，就会通过key来判断是否有改变。这样效率比较高。





