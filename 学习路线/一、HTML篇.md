# 一、HTML篇

## 1 简述一下你对 HTML 语义化的理解？
>- 用正确的标签做正确的事情。
>- html 语义化让页面的内容结构化，结构更清晰，便于对浏览器、搜索引擎解析；即使在没有样式 CSS 情况下也以一种文档格式显示，并且是容易阅读的;
>- 搜索引擎的爬虫也依赖于 HTML 标记来确定上下文和各个关键字的权重，利于 SEO;
>- 使阅读源代码的人对网站更容易将网站分块，便于阅读维护理解。

## 2 标签上 title 与 alt 属性的区别是什么？
>- alt 是给搜索引擎识别，在图像无法显示时的替代文本；
>- title 是关于元素的注释信息，主要是给用户解读。
>- 当鼠标放到文字或是图片上时有 title 文字显示。（因为 IE 不标准）在 IE 浏览器中 alt 起到了 title 的作用，变成文字提示。
>- 在定义 img 对象时，将 alt 和 title 属性写全，可以保证在各种浏览器中都能正常使用。

## 3 iframe的优缺点？
>#### 优点：
>- 解决加载缓慢的第三方内容如图标和广告等的加载问题
>- Security sandbox
>- 并行加载脚本
>#### 缺点：
>- iframe会阻塞主页面的Onload事件
>- 即时内容为空，加载也需要时间
>- 没有语意

## 4 href 与 src？
>#### 含义
>- href (Hypertext Reference)指定网络资源的位置，从而在当前元素或者当前文档和由当前属性定义的需要的锚点或资源之间定义一个链接或者关系。（目的不是为了引用资源，而是为了建立联系，让当前标签能够链接到目标地址。）
>- src source（缩写），指向外部资源的位置，指向的内容将会应用到文档中当前标签所在位置。
>#### href与src的区别
>- 1、请求资源类型不同：href 指向网络资源所在位置，建立和当前元素（锚点）或当前文档（链接）之间的联系。在请求 src 资源时会将其指向的资源下载并应用到文档中，比如 JavaScript 脚本，img 图片；
>- 2、作用结果不同：href 用于在当前文档和引用资源之间确立联系；src 用于替换当前内容；
>- 3、浏览器解析方式不同：当浏览器解析到src ，会暂停其他资源的下载和处理，直到将该资源加载、编译、执行完毕，图片和框架等也如此，类似于将所指向资源应用到当前内容。这也是为什么建议把 js 脚本放在底部而不是头部的原因。

---



