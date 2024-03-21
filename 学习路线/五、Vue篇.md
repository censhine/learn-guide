# 五、Vue篇

## 1 谈谈你对MVVM开发模式的理解？
- MVVM分为Model、View、ViewModel三者。
- Model 代表数据模型，数据和业务逻辑都在Model层中定义；
- View 代表UI视图，负责数据的展示；
- ViewModel 负责监听 Model 中数据的改变并且控制视图的更新，处理用户交互操作；
- Model 和 View 并无直接关联，而是通过 ViewModel 来进行联系的，Model 和 ViewModel 之间有着双向数据绑定的联系。因此当 Model 中的数据改变时会触发 View 层的刷新，View 中由于用户交互操作而改变的数据也会在 Model 中同步。
- 这种模式实现了 Model 和 View 的数据自动同步，因此开发者只需要专注对数据的维护操作即可，而不需要自己操作 dom。

## 2 v-if 和 v-show 有什么区别？
- v-if 是真正的条件渲染，会控制这个 DOM 节点的存在与否。因为它会确保在切换过程中条件块内的事件监听器和子组件适当地被销毁和重建；也是惰性的：如果在初始渲染时条件为假，则什么也不做——直到条件第一次变为真时，才会开始渲染条件块。
- v-show 就简单得多——不管初始条件是什么，元素总是会被渲染，并且只是简单地基于 CSS 的 “display” 属性进行切换。
- 当我们需要经常切换某个元素的显示/隐藏时，使用v-show会更加节省性能上的开销；当只需要一次显示或隐藏时，使用v-if更加合理。
## 3 你使用过 Vuex 吗？
Vuex 是一个专为 Vue.js 应用程序开发的状态管理模式。每一个 Vuex 应用的核心就是 store（仓库）。“store” 基本上就是一个容器，它包含着你的应用中大部分的状态 ( state )。

- （1）Vuex 的状态存储是响应式的。当 Vue 组件从 store 中读取状态的时候，若 store 中的状态发生变化，那么相应的组件也会相应地得到高效更新。
- （2）改变 store 中的状态的唯一途径就是显式地提交 (commit) mutation。这样使得我们可以方便地跟踪每一个状态的变化。
主要包括以下几个模块：

- State => 基本数据，定义了应用状态的数据结构，可以在这里设置默认的初始状态。
- Getter => 从基本数据派生的数据，允许组件从 Store 中获取数据，mapGetters 辅助函数仅仅是将 store 中的 getter 映射到局部计算属性。
- Mutation => 是唯一更改 store 中状态的方法，且必

须是同步函数。
Action => 像一个装饰器，包裹mutations，使之可以异步。用于提交 mutation，而不是直接变更状态，可以包含任意异步操作。
Module => 模块化Vuex，允许将单一的 Store 拆分为多个 store 且同时保存在单一的状态树中。
## 4 说说你对 SPA 单页面的理解，它的优缺点分别是什么？
- SPA（ single-page application ）仅在 Web 页面初始化时加载相应的 HTML、JavaScript 和 CSS。一旦页> 面加载完成，SPA 不会因为用户的操作而进行页面的重新加载或跳转；取而代之的是利用路由机制实现 > HTML 内容的变换，UI 与用户的交互，避免页面的重新加载。

- 优点：
用户体验好、快，内容的改变不需要重新加载整个页面，避免了不必要的跳转和重复渲染；
基于上面一点，SPA 相对对服务器压力小；
前后端职责分离，架构清晰，前端进行交互逻辑，后端负责数据处理；
- 缺点：
初次加载耗时多：为实现单页 Web 应用功能及显示效果，需要在加载页面的时候将 JavaScript、CSS 统一> 加载，部分页面按需加载；
- 前进后退路由管理：由于单页应用在一个页面中显示所有的内容，所以不能使用浏览器的前进后退功能，所> 有的页面切换需要自己建立堆栈管理；
- SEO 难度较大：由于所有的内容都在一个页面中动态替换显示，所以在 SEO 上其有着天然的弱势。
## 5 Class 与 Style 如何动态绑定？
Class 可以通过对象语法和数组语法进行动态绑定：


```html
对象语法：
<div v-bind:class="{ active: isActive, 'text-danger': hasError }"></div>
data: {
	isActive: true,
  	hasError: false
}

数组语法：
<div v-bind:class="[isActive ? activeClass : '', errorClass]"></div>
data: {
  activeClass: 'active',
  errorClass: 'text-danger'
}

Style 也可以通过对象语法和数组语法进行动态绑定：

对象语法：
<div v-bind:style="{ color: activeColor, fontSize: fontSize + 'px' }"></div>
data: {
  activeColor: 'red',
  fontSize: 30
}

数组语法：
<div v-bind:style="[styleColor, styleSize]"></div>
data: {
  styleColor: {
     color: 'red'
   },
  styleSize:{
     fontSize:'23px'
  }
}
```

## 6 怎样理解 Vue 的单向数据流？
- 所有的 prop 都使得其父子 prop 之间形成了一个单向下行绑定：父级 prop 的更新会向下流动到子组件中，但是反过来则不行。
- 这样会防止从子组件意外改变父级组件的状态，从而导致你的应用的数据流向难以理解。
额外的，每次父级组件发生更新时，子组件中所有的 prop 都将会刷新为最新的值。
这意味着你不应该在一个子组件内部改变 prop。如果你这样做了，Vue 会在浏览器的控制台中发出警告。
子组件想修改时，只能通过 $emit 派发一个自定义事件，父组件接收到后，由父组件修改。

## 7 computed 和 watch 的区别和运用的场景？
- computed： 是计算属性，依赖其它属性值，并且 computed 的值有缓存，只有它依赖的属性值发生改变，下一次获取 computed 的值时才会重新计算 computed 的值；
- watch： 更多的是「观察」的作用，类似于某些数据的监听回调 ，每当监听的数据变化时都会执行回调进行后续操作；

**运用场景：**
- 当我们需要进行数值计算，并且依赖于其它数据时，应该使用 computed，因为可以利用 computed 的缓存特性，避免每次获取值时，都要重新计算；
- 当我们需要在数据变化时执行异步或开销较大的操作时，应该使用 watch，使用 watch 选项允许我们执行异步操作 ( 访问一个 API )，限制我们执行该操作的频率，并在我们得到最终结果前，设置中间状态。这些都是计算属性无法做到的。
## 8 直接给一个数组项赋值，Vue 能检测到变化吗？
- 由于 JavaScript 的限制，Vue 不能检测到以下数组的变动：

- 当你利用索引直接设置一个数组项时，例如：vm.items[indexOfItem] = newValue
- 当你修改数组的长度时，例如：vm.items.length = newLength
- 为了解决第一个问题，Vue 提供了以下操作方法：
```js
// Vue.set
Vue.set(vm.items, indexOfItem, newValue)
// vm.$set，Vue.set的一个别名
vm.$set(vm.items, indexOfItem, newValue)
// Array.prototype.splice
vm.items.splice(indexOfItem, 1, newValue)

// 为了解决第二个问题，Vue 提供了以下操作方法：
// Array.prototype.splice
vm.items.splice(newLength)
```

## 9 谈谈你对 Vue 生命周期的理解？

- Vue 实例有一个完整的生命周期，也就是从开始创建、初始化数据、编译模版、挂载 Dom -> 渲染、更新 -> 渲染、卸载等一系列过程，我们称这是 Vue 的生命周期。

- 我们阅读以上源码可知，vm.$set 的实现原理是：

- 如果目标是数组，直接使用数组的 splice 方法触发相应式；
- 如果目标是对象，会先判读属性是否存在、对象是否是响应式，最终如果要对属性进行响应式处理，则是通过调用 defineReactive 方法进行响应式处理（ defineReactive 方法就是 Vue 在初始化对象时，给对象属性采用 Object.defineProperty 动态添加 getter 和 setter 的功能所调用的方法）
## 22 虚拟 DOM 的优缺点？
**优点：**

- 保证性能下限： 框架的虚拟 DOM 需要适配任何上层 API 可能产生的操作，它的一些 DOM 操作的实现必须是普适的，所以它的性能并不是最优的；但是比起粗暴的 DOM 操作性能要好很多，因此框架的虚拟 DOM 至少可以保证在你不需要手动优化的情况下，依然可以提供还不错的性能，即保证性能的下限；
- 无需手动操作 DOM： 我们不再需要手动去操作 DOM，只需要写好 View-Model 的代码逻辑，框架会根据虚拟 DOM 和 数据双向绑定，帮我们以可预期的方式更新视图，极大提高我们的开发效率；
- 跨平台： 虚拟 DOM 本质上是 JavaScript 对象,而 DOM 与平台强相关，相比之下虚拟 DOM 可以进行更方便地跨平台操作，例如服务器渲染、weex 开发等等。

**缺点:**

无法进行极致优化： 虽然虚拟 DOM + 合理的优化，足以应对绝大部分应用的性能需求，但在一些性能要求极高的应用中虚拟 DOM 无法进行针对性的极致优化。
## 23 虚拟 DOM 实现原理？
虚拟 DOM 的实现原理主要包括以下 3 部分：

- 用 JavaScript 对象模拟真实 DOM 树，对真实 DOM 进行抽象；
- diff 算法 — 比较两棵虚拟 DOM 树的差异；
- pach 算法 — 将两个虚拟 DOM 对象的差异应用到真正的 DOM 树。

## 24 Vue 中的 key 有什么作用？
- key 是为 Vue 中 vnode 的唯一标记，通过这个 key，我们的 diff 操作可以更准确、更快速。
- Vue 的 diff 过程可以概括为：oldCh 和 newCh 各有两个头尾的变量 oldStartIndex、oldEndIndex 和 newStartIndex、newEndIndex，它们会新节点和旧节点会进行两两对比，即一共有4种比较方式：newStartIndex 和oldStartIndex 、newEndIndex 和 oldEndIndex 、newStartIndex 和 oldEndIndex 、newEndIndex 和 oldStartIndex，如果以上 4 种比较都没匹配，如果设置了key，就会用 key 再进行比较，在比较的过程中，遍历会往中间靠，一旦 StartIdx > EndIdx 表明 oldCh 和 newCh 至少有一个已经遍历完了，就会结束比较。
- 所以 Vue 中 key 的作用是：key 是为 Vue 中 vnode 的唯一标记，通过这个 key，我们的 diff 操作可以更准确、更快速!

- 更准确：因为带 key 就不是就地复用了，在 sameNode 函数 a.key === b.key 对比中可以避免就地复用的情况。所以会更加准确。
- 更快速：利用 key 的唯一性生成 map 对象来获取对应节点，比遍历方式更快，源码如下：
```javascript
function createKeyToOldIdx (children, beginIdx, endIdx) {
  let i, key
  const map = {}
  for (i = beginIdx; i <= endIdx; ++i) {
    key = children[i].key
    if (isDef(key)) map[key] = i
  }
  return map
}
```

## 25 你有对 Vue 项目进行哪些优化？
- **（1）代码层面的优化**

- v-if 和 v-show 区分使用场景
- computed 和 watch 区分使用场景
- v-for 遍历必须为 item 添加 key，且避免同时使用 v-if
- 长列表性能优化
- 事件的销毁
- 图片资源懒加载
- 路由懒加载
- 第三方插件的按需引入
- 优化无限列表性能
- 服务端渲染 SSR or 预渲染

- **（2）Webpack 层面的优化**

- Webpack 对图片进行压缩
- 减少 ES6 转为 ES5 的冗余代码
- 提取公共代码
- 模板预编译
- 提取组件的 CSS
- 优化 SourceMap
- 构建结果输出分析
- Vue 项目的编译优化
- **（3）基础的 Web 技术的优化**

- 开启 gzip 压缩
- 浏览器缓存
- CDN 的使用
- 使用 Chrome Performance 查找性能瓶颈

## 26 对于 vue3.0 特性你有什么了解的吗？
Vue 3.0 的目标是让 Vue 核心变得更小、更快、更强大，因此 Vue 3.0 增加以下这些新特性：

- **（1）监测机制的改变**
- 3.0 将带来基于代理 Proxy 的 observer 实现，提供全语言覆盖的反应性跟踪。这消除了 Vue 2 当中基于 Object.defineProperty 的实现所存在的很多限制：

- 只能监测属性，不能监测对象
- 检测属性的添加和删除；
- 检测数组索引和长度的变更；
- 支持 Map、Set、WeakMap 和 WeakSet。
- 新的 observer 还提供了以下特性：

- 用于创建 observable 的公开 API。这为中小规模场景提供了简单轻量级的跨组件状态管理解决方案。
- 默认采用惰性观察。在 2.x 中，不管反应式数据有多大，都会在启动时被观察到。如果你的数据集很大，这可能会在应用启动时带来明显的开销。在 3.x 中，只观察用于渲染应用程序最初可见部分的数据。
- 更精确的变更通知。在 2.x 中，通过 Vue.set 强制添加新属性将导致依赖于该对象的 watcher 收到变更通知。在 3.x 中，只有依赖于特定属性的 watcher 才会收到通知。
- 不可变的 observable：我们可以创建值的“不可变”版本（即使是嵌套属性），除非系统在内部暂时将其“解禁”。这个机制可用于冻结 prop 传递或 Vuex 状态树以外的变化。
- 更好的调试功能：我们可以使用新的 renderTracked 和 renderTriggered 钩子精确地跟踪组件在什么时候以及为什么重新渲染。

- **（2）模板**
- 模板方面没有大的变更，只改了作用域插槽，2.x 的机制导致作用域插槽变了，父组件会重新渲染，而 3.0 把作用域插槽改成了函数的方式，这样只会影响子组件的重新渲染，提升了渲染的性能。
同时，对于 render 函数的方面，vue3.0 也会进行一系列更改来方便习惯直接使用 api 来生成 vdom 。

- **（3）对象式的组件声明方式**
- vue2.x 中的组件是通过声明的方式传入一系列 option，和 TypeScript 的结合需要通过一些装饰器的方式来做，虽然能实现功能，但是比较麻烦。
- 3.0 修改了组件的声明方式，改成了类式的写法，这样使得和 TypeScript 的结合变得很容易。
- 此外，vue 的源码也改用了 TypeScript 来写。其实当代码的功能复杂之后，必须有一个静态类型系统来做一些辅助管理。
- 现在 vue3.0 也全面改用 TypeScript 来重写了，更是使得对外暴露的 api 更容易结合 TypeScript。静态类型系统对于复杂代码的维护确实很有必要。

- **（4）其它方面的更改**
- vue3.0 的改变是全面的，上面只涉及到主要的 3 个方面，还有一些其他的更改：

- 支持自定义渲染器，从而使得 weex 可以通过自定义渲染器的方式来扩展，而不是直接 fork 源码来改的方式。
- 支持 Fragment（多个根节点）和 Protal（在 dom 其他部分渲染组建内容）组件，针对一些特殊的场景做了处理。
- 基于 treeshaking 优化，提供了更多的内置功能。

## 27 响应式原理（变化侦测）
- 使用发布订阅模式将数据劫持和模板编译结合，实现双向绑定

- 1、observer: 封装 Object.defineProperty 方法用来劫持对象属性的getter和setter，以此来追踪数据变化。

- 2、读取数据时触发getter来收集依赖(Watcher)到Dep。
- 3、修改数据时触发setter，并遍历依赖列表，通知所有相关依赖（Watcher）
- 4、Dep 类为依赖找一个存储依赖的地方，用来收集和管理依赖，在getter中收集，在setter中通知。
- 5、Watcher 类就是收集的依赖，实际上是一个订阅器，Watcher会将自己的实例赋值给window.target（全局变量）上，然后去主动访问属性，触发属性的getter，getter中会将此Watcher收集到Dep中，Watcher的update方法会在Dep的通知方法中被调用，触发更新。
- 6、Observer 类用来将一个对象的所有属性和子属性都变成响应式的，通过递归调用defineReactive来实现。
- 7、由于无法侦测对象上新增/删除属性，所以提供 $set 和 $delete API5。

## 28 Object.defineProperty怎么用， 三个参数？，有什么作用啊？
- Object.defineProperty() 方法会直接在一个对象上定义一个新属性，或者修改一个对象的现有属性，并返回此对象。
```javascript
  obj：需要定义属性的对象
  prop：需要定义的属性
  {}：要定义或修改的属性描述符。
  value: "18",         // 设置默认值 （与 get() 互斥）
  enumerable: true,    //这一句控制属性可以枚举 enumerable 改为true 就可以参与遍历了   默认值false
  writable: true,      // 该属性是否可写   默认值false （与 set() 互斥）
  configurable: true,  // 该属性是否可被删除   默认值false
  get // 当有人读取 prop 的时候  get函数就会调用,并且返回就是 sss 的值
  set // 当有人修改 prop 的时候  set函数就会调用, 有个参数这个参数就是修改后的值
```

## 29 vue2和vue3的响应式原理都有什么区别呢？
- vue2 用的是 Object.defindProperty 但是vue3用的是Proxy

- Object.defindProperty 缺点：

- 一次只能对一个属性进行监听，需要遍历来对所有属性监听
- 对于对象的新增属性，需要手动监听
- 对于数组通过push、unshift方法增加的元素，也无法监听
- Proxy就没有这个问题，可以监听整个对象的数据变化，所以用vue3.0会用Proxy代替definedProperty。

## 30 Vue的patch diff 算法
- patch将新老VNode节点进行比对，然后将根据两者的比较结果进行最小单位地修改视图，而不是将整个视图根据新的VNode重绘。patch的核心在于diff算法，这套算法可以高效地比较virtual DOM的变更，得出变化以修改视图。

- diff算法核心是通过同层的树节点进行比较而非对树进行逐层搜索遍历的方式，所以时间复杂度只有O(n)，是一种相当高效的算法。

- 同层级比较（只比较同一层级，不跨级比较）
- tag 不相同，则直接删除重建，不在深度比较
- tag 和 key，两个都相同，则认为是相同节点，会进行深度比较
## 31 Vue 模板编译原理
- 模板字符串 转换成 element AST（解析器）
- Vue-loader 切割解析 .vue 文件（parseHTML按标签以出栈入栈形式切割（自闭合不入栈直接处理），出栈时维护父子关系）生成 AST（抽象语法树）

- 使用大量正则匹配开始结束标签，while指针定位解析位置，
- 对 AST 进行静态节点标记，主要用来做虚拟DOM的渲染优化（优化器）
- 在dom更新时不需 diff 静态节点。
- 使用 element AST 生成 render 函数代码字符串（代码生成器）
- Vue-template-compiler再解析成render（可执行函数字符串-with(this)=>{return _c(‘div’)}），new Function 生成函数，传递给组件的 render

- 在组件渲染的时候直接调用 render 即可

## 32 Vue原理总结
- 【模板编译】将template模板，经过编译系统后生成VNode，（模板字符串→AST→Render函数）

- 【渲染】然后再通过渲染系统来将VNode生成真实DOM（document.createElement && Mount挂载到真实DOM节点上）

- 【响应式】通过响应式系统对数据进行监听，当数据发生改变时，触发依赖项（组件）

- 【Diff & Patch】组件内收到通知后，会通过diff算法对比VNode的变化，尽可能复用代码，找出最小差异，保证性能消耗最小。

- 【渲染】拿到需要新增/删除/修改的VNode后，逐一去操作真实DOM进行修改（通过选择器选择到对应真实DOM节点进行修改）


