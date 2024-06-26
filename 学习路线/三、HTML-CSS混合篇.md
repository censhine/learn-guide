# 三、HTML-CSS混合篇

# 1. HTML5、CSS3 里面都新增了那些新特性？
#### HTML5

**新的语义标签**
- article 独立的内容。
- aside 侧边栏。
- header 头部。
- nav 导航。
- section 文档中的节。
- footer 页脚。
- 画布(Canvas) API
- 地理(Geolocation) API
- 本地离线存储 localStorage 长期存储数据，浏览器关闭后数据不丢失；
- sessionStorage 的数据在浏览器关闭后自动删除
- 新的技术webworker, websocket, Geolocation
- 拖拽释放(Drag and drop) API
- 音频、视频API(audio,video)
- 表单控件，calendar、date、time、email、url、searc

#### CSS3

**2d，3d变换**
- Transition, animation
- 媒体查询
- 新的单位（rem, vw，vh 等）
- 圆角（border-radius），阴影（box-shadow），对文字加特效（text-shadow），线性渐变（gradient），旋转（transform）transform:rotate(9deg) scale(0.85,0.90) translate(0px,-30px) skew(-9deg,0deg);//旋转,缩放,定位,倾斜
- rgba
# 2. BFC 是什么？
- BFC 即 Block Formatting Contexts (块级格式化上下文)，它属于普通流，即：元素按照其在 HTML 中的先后位置至上而下布局，在这个过程中，行内元素水平排列，直到当行被占满然后换行，块级元素则会被渲染为完整的一个新行，除非另外指定，否则所有元素默认都是普通流定位，也可以说，普通流中元素的位置由该元素在 HTML 文档中的位置决定。
- 可以把 BFC 理解为一个封闭的大箱子，箱子内部的元素无论如何翻江倒海，都不会影响到外部。
- 只要元素满足下面任一条件即可触发 BFC 特性

**body 根元素**
- 浮动元素：float 除 none 以外的值
- 绝对定位元素：position (absolute、fixed)
- display 为 inline-block、table-cells、flex
- overflow 除了 visible 以外的值 (hidden、auto、scroll)

# 3. 常见兼容性问题？
- 浏览器默认的margin和padding不同。解决方案是加一个全局的*{margin:0;padding:0;}来统一。
- Chrome 中文界面下默认会将小于 12px 的文本强制按照 12px 显示,
- 可通过加入 CSS 属性 -webkit-text-size-adjust: none; 解决.

---
