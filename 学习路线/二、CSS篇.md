# 二、CSS篇

## 1 介绍一下 CSS 的盒子模型？
>- 有两种， IE 盒子模型、W3C 盒子模型；
>- 盒模型： 内容(content)、填充(padding)、边界(margin)、 边框(border)；
>- 区 别： IE 的 content 部分把 border 和 padding 计算了进去;

## 2 css 选择器优先级？
> !important > 行内样式（比重1000）> ID 选择器（比重100） > 类选择器（比重10） > 标签（比重1） > 通配符 > 继承 > 浏览器默认属性

## 3 垂直居中几种方式？
>- 单行文本: line-height = height
>- 图片: vertical-align: middle;
>- absolute 定位: top: 50%;left: 50%;transform: translate(-50%, -50%);
>- flex: display:flex;margin:auto

## 4 简明说一下 CSS link 与 @import 的区别和用法？
>- link 是 XHTML 标签，除了加载CSS外，还可以定义 RSS 等其他事务；@import 属于 CSS 范畴，只能加载 CSS。
>- link 引用 CSS 时，在页面载入时同时加载；@import 需要页面网页完全载入以后加载。
>- link 是 XHTML 标签，无兼容问题；@import 是在 CSS2.1 提出的，低版本的浏览器不支持。
>- link 支持使用 Javascript 控制 DOM 去改变样式；而@import不支持。

## 5 rgba和opacity的透明效果有什么不同？
> opacity 会继承父元素的 opacity 属性，而 RGBA 设置的元素的后代元素不会继承不透明属性。

## 6 display:none和visibility:hidden的区别？
>- display:none 隐藏对应的元素，在文档布局中不再给它分配空间，它各边的元素会合拢，就当他从来不存在。
>- visibility:hidden 隐藏对应的元素，但是在文档布局中仍保留原来的空间。

## 7 position的值， relative和absolute分别是相对于谁进行定位的？
>- relative:相对定位，相对于自己本身在正常文档流中的位置进行定位。
>- absolute:生成绝对定位，相对于最近一级定位不为static的父元素进行定位。
>- fixed: （老版本IE不支持）生成绝对定位，相对于浏览器窗口或者frame进行定位。
>- static:默认值，没有定位，元素出现在正常的文档流中。
>- sticky:生成粘性定位的元素，容器的位置根据正常文档流计算得出。

## 8 画一条0.5px的直线？
>#### 考查的是css3的transform
>- height: 1px;
>- transform: scale(0.5);

## 9 calc, support, media各自的含义及用法？
>- @support 主要是用于检测浏览器是否支持CSS的某个属性，其实就是条件判断，如果支持某个属性，你可以写一套样式，如果不支持某个属性，你也可以提供另外一套样式作为替补。
>- calc() 函数用于动态计算长度值。 calc()函数支持 “+”, “-”, “*”, “/” 运算；
>- @media 查询，你可以针对不同的媒体类型定义不同的样式。

## 10 1rem、1em、1vh、1px各自代表的含义？
>#### rem
>- rem是全部的长度都相对于根元素元素。通常做法是给html元素设置一个字体大小，然后其他元素的长度单位就为rem。
>#### em
>- 子元素字体大小的em是相对于父元素字体大小
>- 元素的width/height/padding/margin用em的话是相对于该元素的font-size
>#### vw/vh
>- 全称是 Viewport Width 和 Viewport Height，视窗的宽度和高度，相当于 屏幕宽度和高度的 1%，不过，处理宽度的时候%单位更合适，处理高度的 话 vh 单位更好。
>#### px
>- px像素（Pixel）。相对长度单位。像素px是相对于显示器屏幕分辨率而言的。
>- 一般电脑的分辨率有{19201024}等不同的分辨率
>- 19201024 前者是屏幕宽度总共有1920个像素,后者则是高度为1024个像素

## 11 画一个三角形？
这属于简单的css考查，平时在用组件库的同时，也别忘了原生的css
```css
.a {
    width: 0;
    height: 0;
    border-width: 100px;
    border-style: solid;
    border-color: transparent #0099CC transparent transparent;
    transform: rotate(90deg); /*顺时针旋转90°*/
}
<div class="a"></div>
```
---