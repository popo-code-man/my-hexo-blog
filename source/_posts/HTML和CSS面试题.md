---
title: HTML和CSS面试题
date: 2023-03-10 22:22:28
tags: React
categories: 面试题
cover: csslogo.png
top_img: csslogo.png
---

#### 怎么让一个不定宽高的 DIV，垂直水平居中？

```css
/*
* flex 方法
*/
display: flex;
align-items: center;
justify-cotent: center;
/*
* 知道盒子宽高 margin负值配合定位
*/
.son1 {
	width: 200px;
	height: 200px;
	position: absolute;
	top: 50%;
	left: 50%;
	margin-top: -100px;
	margin-left: -100px;
}
.son2 {
	width: 200px;
	height: 200px;
	position: absolute;
	top: 0;
	left: 0;
	right: 0;
	bottom: 0;
	margin: auto;
}
/*
* CSS3 transform
*/
position: absolute;
top: 50%;
left: 50%;
transform: translate(-50%, -50%);
/*
*使用display:table-cell方法
*/
.parent {
	display: table-cell;
	text-align: center;
	vertical-align: middle;
}
.son {
	display: inline-block;
	vertical-align: middle;
}
```

#### position 几个属性的作用？

```css
static -- 默认值 没有定位
fixed  -- 绝对定位 相对于浏览器窗口
absolute -- 绝对定位 相对于 static 定位以外的第一个父元素进行定位。
relative -- 相对定位 相对于其正常位置进行定位。
inherit -- 规定应该从父元素继承 position 属性的值。
```

#### px，em，rem 的区别？

- px 像素（Pixel）。相对长度单位。像素 px 是相对于显示器屏幕分辨率而言的。

  1.  IE 无法调整那些使用 px 作为单位的字体大小；
  2.  国外的大部分网站能够调整的原因在于其使用了 em 或 rem 作为字体单位；
  3.  Firefox 能够调整 px 和 em，rem，但是 96%以上的中国网民使用 IE 浏览器(或内核)。

- em 是相对长度单位。相对于当前对象内文本的字体尺寸。如当前对行内文本的字体尺寸未被人为设置，则相对于浏览器的默认字体尺寸。

  1. em 的值并不是固定的；
  2. em 会继承父级元素的字体大小。

- rem 是 CSS3 新增的一个相对单位（root em，根 em），使用 rem 为元素设定字体大小时，仍然是相对大小，但相对的只是 HTML 根元素。

  > rem 一般可以经过动态设置根元素大小来实现适配各种分辨率屏幕

#### 什么是 BFC？

> BFC(Block formatting context)直译为"块级格式化上下文"。它是一个独立的渲染区域，只有 Block-level box 参与， 它规定了内部的 Block-level Box 如何布局，并且与这个区域外部毫不相干。
>
> BFC 就是页面上的一个隔离的独立容器，容器里面的子元素不会影响到外面的元素。反之也如此。
>
> [更详细解释](https://blog.csdn.net/sinat_36422236/article/details/88763187)

#### CSS 引入的方式有哪些? link 和@import 的区别是?

- link 是 XHTML 标签，除了加载 CSS 外，还可以定义 RSS 等其他事务；@import 属于 CSS 范畴，只能加载 CSS。
- link 引用 CSS 时，在页面载入时同时加载；@import 需要页面网页完全载入以后加载。
- link 是 XHTML 标签，无兼容问题；@import 是在 CSS2.1 提出的，低版本的浏览器不支持。
- ink 支持使用 Javascript 控制 DOM 去改变样式；而@import 不支持。

#### 描述 css reset 的作用和用途？

> HTML 标签在浏览器中都有默认的样式，不同的浏览器的默认样式之间存在差别。例如 ul 默认带有缩进样式，在 IE 下，它的缩进是由 margin 实现的，而在 Firefox 下却是由 padding 实现的。开发时浏览器的默认样式可能会给我们带来多浏览器兼容性问题，影响开发效率。所以解决的方法就是一开始就将浏览器的默认样式全部去掉，更准确说就是通过重新定义标签样式。“覆盖”浏览器的 CSS 默认属性。最最简单的说法就是把浏览器提供的默认样式覆盖掉！这就是 CSS reset。
>
> [css-reset 文件地址](http://yui.yahooapis.com/3.18.1/build/cssreset/cssreset-min.css)

#### 解释 css sprites，如何使用？

> 精灵图：简单来说就是把一些图标汇集到一张 png 上 通过像素点来显示不同位置的图片

#### 清除浮动的几种方式？

1. **额外标签法**：给谁清除浮动，就在其后额外添加一个空白标签 。

   ```css
   .clear {
   	clear: both;
   }
   ```

2. **父级添加 overflow 方法**: 可以通过触发 BFC 的方式，实现清楚浮动效果。

   ```css
   .parent {
   	overflow: hidden;
   }
   ```

3. **使用 after 伪元素清除浮动**: ` :after`方式为空元素的升级版，好处是不用单独加标签了。（较常用）

   ```css
   .clearfix:after {
   	content: "";
   	display: block;
   	height: 0;
   	clear: both;
   	visibility: hidden;
   }
   .clearfix {
   	*zoom: 1;
   }
   ```

4. **使用 before 和 after 双伪元素清除浮动**: （较常用）

   ```css
   .clearfix:before,
   .clearfix:after {
   	content: "";
   	display: table;
   }
   .clearfix:after {
   	clear: both;
   }
   .clearfix {
   	*zoom: 1;
   }
   ```

#### 能否简述一下如何使一套设计方案，适应不同的分辨率，有哪些方法可以实现？

- 百分比布局
- flex 弹性盒子
- rem 适配
- 各种框架的布局系统 如：bootstrap 的栅格系统
- css 媒体查询实现不同相应分辨率显示相应效果
- ......

#### 你能描述一下渐进增强和优雅降级之间的不同吗？

> **渐进增强（Progressive Enhancement）**：一开始就针对低版本浏览器进行构建页面，完成基本的功能，然后再针对高级浏览器进行效果、交互、追加功能达到更好的体验。
>
> **优雅降级（Graceful Degradation）**：一开始就构建站点的完整功能，然后针对浏览器测试和修复。比如一开始使用 CSS3 的特性构建了一个应用，然后逐步针对各大浏览器进行 hack 使其可以在低版本浏览器上正常浏览。

#### 合理的页面布局中常听过结构与表现分离，那么结构是什么？表现是什么？

> 结构：HTML ( 骨架 )
>
> 表现：CSS

#### 简述对 Web 语义化的理解？

- 正确的标签做正确的事情
- 页面内容结构化
- 无 CSS 样子时也容易阅读，便于阅读维护和理解
- 便于浏览器、搜索引擎解析。 利于爬虫标记、利于 SEO

#### CSS 都有哪些选择器？CSS 选择器的优先级是怎么样定义的？

- **选择器**

  1. 标签名选择器
  2. 类选择器（class）
  3. id 选择器 （#box）
  4. 后代选择器（空格隔开）
  5. 群组选择器（逗号隔开）

- **优先级**

  ​ 行内 > id > 类 > 标签

#### display： none；与 visibility： hidden 的区别是什么？

- 如果给一个元素设置了 display: none，那么该元素以及它的所有后代元素都会隐藏，它是前端开发人员使用频率最高的一种隐藏方式。隐藏后的元素无法点击，无法使用屏幕阅读器等辅助设备访问，占据的空间消失。
- 给元素设置 visibility: hidden 也可以隐藏这个元素，但是隐藏元素仍需占用与未隐藏时一样的空间，也就是说虽然元素不可见了，但是仍然会影响页面布局

#### 用 CSS 定义 p 标签，要求实现以下效果：字体颜色在 IE6 下为黑色(#000000)；IE7 下为红色(#ff0000)；而其他浏览器下为绿色(#00ff00)

```css
p {
	color: green;
	*color: blue;
	_color: black;
}
```

#### HTML 与 XHTML——二者有什么区别

- XHTML 元素必须被正确地嵌套。

- XHTML 元素必须被关闭。

- 标签名必须用小写字母。

- 所有的 XHTML 元素必须被嵌套于 <html> 根元素中。

#### Doctype 作用? 严格模式与混杂模式-如何触发这两种模式，区分它们有何意义?

> - **Doctype**: `<!DOCTYPE>`声明叫做文件类型定义（DTD），声明的作用为了告诉浏览器该文件的类型。让浏览器解析器知道应该用哪个规范来解析文档。<!DOCTYPE>声明必须在 HTML 文档的第一行，这并不是一个 HTML 标签
>
> - **严格模式**:又称标准模式，是指浏览器按照 W3C 标准解析代码。
>
>   **混杂模式**:又称怪异模式或兼容模式，是指浏览器用自己的方式解析代码。
>
>   **如何区分**:浏览器解析时到底使用严格模式还是混杂模式，与网页中的 DTD 直接相关。

#### 盒模型：

> W3C 标准中，如果设置一个元素的宽度和高度，指的是元素内容的宽度和高度，而在 Quirks 模式下，IE 的宽度和高度还包含了 padding 和 border。

#### Css Hack？ie6,7,8 的 hack 分别是什么？

> 针对不同的浏览器写不同的 CSS code 的过程，就是 CSS hack。

```css
 background-color:blue;      /*firefox*/

background-color:red\9;      /*all ie*/

background-color:yellow;    /*ie8*/

+background-color:pink;        /*ie7*/

_background-color:orange;       /*ie6*/    }

:root #test { background-color:purple\9; }  /*ie9*/

@media all and (min-width:0px){ #test {background-color:black;} }  /*opera*/

@media screen and (-webkit-min-device-pixel-ratio:0){ #test {background-color:gray;} }       /*chrome and safari*/
```

#### 请用 div+css 写出左侧固定(width:200px;),右侧自适应页面宽度.

```html
<style>
	.container {
		padding: 10px;
		border: 1px solid #ffa200;
		margin-bottom: 40px;
	}
	.container .left {
		background-color: #4b83e2;
	}
	.container .right {
		background-color: #ff3b30;
	}
	/*左浮动固定宽度，右边盒子overflow:hidden触发bfc，使其不与浮动盒子区域重叠，因此会重新计算宽度。*/
	.container1 .left {
		float: left;
		width: 200px;
	}
	.container1 .right {
		overflow: hidden;
	}
	/*清除浮动*/
	.container1:after {
		content: "";
		height: 0;
		line-height: 0;
		display: block;
		visibility: hidden;
		clear: both;
	}
	/*左浮动固定宽度,右边margin-left*/
	.container2 .left {
		float: left;
		width: 200px;
	}
	.container2 .right {
		margin-left: 200px;
	}
	/*清除浮动*/
	.container2:after {
		content: "";
		height: 0;
		line-height: 0;
		display: block;
		visibility: hidden;
		clear: both;
	}
	/*左边绝对定位，右边设置margin-left，缺点：当左边高于右边时，左边会超出父元素，需要使用js补救。*/
	.container3 {
		position: relative;
	}
	.container3 .left {
		position: absolute;
		left: 10px;
		top: 10px;
		width: 200px;
	}
	.container3 .right {
		margin-left: 200px;
	}
	/*双display:inline-block*/
	.container4 {
		font-size: 0;
	}
	.container4 .left {
		width: 200px;
	}
	.container4 .left,
	.container4 .right {
		display: inline-block;
		font-size: 16px;
		vertical-align: top;
	}
	.container4 .right {
		width: calc(100% - 200px);
	}
	/*table*/
	.container5 {
		display: table;
	}
	.container5 .left,
	.container5 .right {
		display: table-cell;
	}
	/*flex*/
	.container6 {
		display: flex;
	}
	.container6 .right {
		flex-grow: 1;
	}
	/*grid*/
	.container7 {
		display: grid;
	}
	.container7 .left {
		grid-column: 1;
	}
	.container7 .right {
		grid-column: 2;
	}
</style>
<div class="container container1">
	<div class="left">左边左边左边左边左边左边左边左边左边左边</div>
	<div class="right">
		右边右边右边右边右边右边右边右边右边右边右边右边右边右边右边右边右边
	</div>
</div>
<div class="container container2">
	<div class="left">左边左边左边左边左边左边左边左边左边左边</div>
	<div class="right">
		右边右边右边右边右边右边右边右边右边右边右边右边右边右边右边右边右边
	</div>
</div>
<div class="container container3">
	<div class="left">左边左边左边左边左边左边左边左边左边左边</div>
	<div class="right">
		右边右边右边右边右边右边右边右边右边右边右边右边右边右边右边右边右边
	</div>
</div>
<div class="container container4">
	<div class="left">左边左边左边左边左边左边左边左边左边左边</div>
	<div class="right">
		右边右边右边右边右边右边右边右边右边右边右边右边右边右边右边右边右边
	</div>
</div>
<div class="container container5">
	<div class="left">左边左边左边左边左边左边左边左边左边左边</div>
	<div class="right">
		右边右边右边右边右边右边右边右边右边右边右边右边右边右边右边右边右边
	</div>
</div>
<div class="container container6">
	<div class="left">左边左边左边左边左边左边左边左边左边左边</div>
	<div class="right">
		右边右边右边右边右边右边右边右边右边右边右边右边右边右边右边右边右边
	</div>
</div>
<div class="container container7">
	<div class="left">左边左边左边左边左边左边左边左边左边左边</div>
	<div class="right">
		右边右边右边右边右边右边右边右边右边右边右边右边右边右边右边右边右边
	</div>
</div>
```

#### display：inline-block 什么时候会显示间隙？

> **间隙产生的原因是因为，换行或空格会占据一定的位置**

​ **解决**：夫元素设置：

```css
font-size: 0;
letter-spaceing: -4px;
```

#### overflow 有哪些属性值？

- **visible**: 默认值。内容不会被修剪，会呈现在元素框之外。
- **hidden**: 内容会被修剪，并且其余内容是不可见的。
- **scroll**: 内容会被修剪，但是浏览器会显示滚动条以便查看其余的内容。
- **auto**: 如果内容被修剪，则浏览器会显示滚动条以便查看其余的内容。
- **inherit**: 规定应该从父元素继承 overflow 属性的值。

#### css 去掉 iPhone、iPad 默认按钮样式

```css
input[type="button"],
input[type="submit"],
input[type="reset"] {
	-webkit-appearance: none;
	-moz-appearance: none;
	appearance: none;
}
```

#### CSS 样式初始化的目的

> - CSS 初始化是指重设浏览器的样式。不同的浏览器默认的样式可能不尽相同，所以开发时的第一件事可能就是如何把它们统一。如果没对 CSS 初始化往往会出现浏览器之间的页面差异。
>
> - 每次新开发网站或新网页时候通过初始化 CSS 样式的属性，为我们将用到的 CSS 或 html 标签更加方便准确，使得我们开发网页内容时更加方便简洁，同时减少 CSS 代码量，节约网页下载时间。
>
> - 初始化 CSS 为我们节约网页代码，节约网页下载时间；还会使得我们开发网页内容时更加方便简洁，不用考虑很多。
>
> - 如果不初始化，整个页面做完会很糟糕，重复的 css 样式很多。

#### 用 div+css 网站布局的好处

- div+css 布局比 table 布局节省页面代码，代码结构也更清晰明了.

- div+css 的页面对搜索引擎支持好，而且速度更快了,能够比 table 更加快速的显示网站内容.

- div+css 布局使网站版面布局修改变的更简单,因为版面代码都写在独立的 css 文件里修改起来方便多了,不象 table 要在页面中修改很多信息.

#### 用表格 table 对 seo 的影响

> 待补充。。。。。。

#### console 有哪些常用方法?（答出三种并说出它的用法即可，想考察你有没有工作经验）

- **console.log()**: 最常用的
- **console.dir()**: 将传入对象的属性，包括子对象的属性以列表形式输出
- **console.assert()**: 接收至少两个参数，第一个参数的值或返回值为`false`的时候，将会在控制台上输出后续参数的值。
- **console.count()**: 输出执行到该行的次数，可选参数 label 可以输出在次数之前
- **console.error()**:用于输出错误信息，用法和常见的`console.log`一样，不同点在于输出内容会标记为错误的样式，便于分辨。

#### 为什么利用多个域名来存储网站资源会更有效？

- CDN 缓存更方便

- 突破浏览器并发限制

- 节约 cookie 带宽

- 节约主域名的连接数，优化页面响应速度

- 防止不必要的安全问题

#### 网页的重绘与重排以及重构

- **重绘**: 浏览器加载文档

  > 浏览器从下载文档到显示页面的过程是个复杂的过程，这里包含了重绘和重排。各家浏览器引擎的工作原理略有差别，但也有一定规则。简单讲，通常在文档初次加载时，浏览器引擎会解析 HTML 文档来构建 DOM 树，之后根据 DOM 元素的几何属性构建一棵用于渲染的树。渲染树的每个节点都有大小和边距等属性，类似于盒子模型（由于隐藏元素不需要显示，渲染树中并不包含 DOM 树中隐藏的元素）。当渲染树构建完成后，浏览器就可以将元素放置到正确的位置了，再根据渲染树节点的样式属性绘制出页面。由于浏览器的流布局，对渲染树的计算通常只需要遍历一次就可以完成。但 table 及其内部元素除外，它可能需要多次计算才能确定好其在渲染树中节点的属性，通常要花 3 倍于同等元素的时间。这也是为什么我们要避免使用 table 做布局的一个原因。
  >
  > 重绘是一个 **元素外观 ** 的改变所触发的浏览器行为，例如改变 visibility、outline、背景色等属性。浏览器会根据元素的新属性重新绘制，使元素呈现新的外观。重绘不会带来重新布局，并不一定伴随重排。

- **重排（回流）**: 重排是更明显的一种改变，可以理解为渲染树需要重新计算。

  > - **DOM 元素的几何属性变化**
  >
  >   当 DOM 元素的几何属性变化时，渲染树中的相关节点就会失效，浏览器会根据 DOM 元素的变化重新构建渲染树中失效的节点.
  >   重排一定会引起浏览器的重绘，一个元素的重排通常会带来一系列的反应，甚至触发整个文档的重排和重绘，性能代价是高昂的。
  >
  > - **DOM 树的结构变化**
  >   当 DOM 树的结构变化时，例如节点的增减、移动等，也会触发重排。浏览器引擎布局的过程，类似于树的前序遍历，是一个从上到下从左到右的过程。通常在这个过程中，当前元素不会再影响其前面已经遍历过的元素。所以，如果在 body 最前面插入一个元素，会导致整个文档的重新渲染，而在其后插入一个元素，则不会影响到前面的元素。
  >
  > - **获取某些属性**
  >   浏览器引擎可能会针对重排做了优化。比如 Opera，它会等到有足够数量的变化发生，或者等到一定的时间，或者等一个线程结束，再一起处理，这样就只发生一次重排。但除了渲染树的直接变化，当获取一些属性时，浏览器为取得正确的值也会触发重排。这样就使得浏览器的优化失效了。这些属性包括：offsetTop、offsetLeft、 offsetWidth、offsetHeight、scrollTop、scrollLeft、scrollWidth、scrollHeight、clientTop、clientLeft、clientWidth、clientHeight、getComputedStyle() (currentStyle in IE)。所以，在多次使用这些值时应进行缓存。
  >
  > - **其他**
  >   改变浏览器窗口大小、改变一些元素的样式

- **重构**: 一般指项目重构，换框架等等

#### 谈谈以前端角度出发做好 SEO 需要考虑什么

- 经常更新网站内容，优质的原创内容越多，搜索引擎收录越多，权重越高。
- 优化 meta 标签的关键词，启用 Keep-Alive；为每个页面单独命名，要符合页面内容。
- 优化网站、代码结构，简洁，清晰，结构鲜明的代码容易被搜索引擎爬取。
- 确保每个页面都可以通过至少一个文本链接到达
- 重要的内容，应该能从首页或者网站结构中比较浅的层次访问到
- 使用文字而不是 flash、图片、Javascript 等来显示重要的内容或链接，为图片的 alt 添加文本。
-     ......

#### rgba()和 opacity 的透明效果有什么不同？

- `opacity` 是属性，`rgba()`是函数，计算之后是个属性值；
- `opacity` 作用于元素和元素的内容，内容会继承元素的透明度，取值 0-1；
- `rgba()` 一般作为背景色 `background-color` 或者颜色 `color` 的属性值，透明度由其中的 `alpha` 值生效，取值 0-1；

#### Sass、LESS 是什么？大家为什么要使用他们？

> CSS 预处理器。他是 CSS 上的一种抽象层。他们是一种特殊的语法/语言编译成 CSS。

- 结构清晰，便于扩展。

- 可以方便地屏蔽浏览器私有语法差异。这个不用多说，封装对浏览器语法差异的重复处理，减少无意义的机械劳动。

- 可以轻松实现多重继承。

- 完全兼容 CSS 代码，可以方便地应用到老项目中。LESS 只是在 CSS 语法上做了扩展，所以老的 CSS 代码也可以与 LESS 代码一同编译。

#### 行内元素有哪些？块级元素有哪些？空(void)元素有那些？样式之间的转换

- **行内元素**: a、b、span、img、input、strong、select、label、em、button、textarea
- **块级元素**:div、ul、li、dl、dt、dd、p、h1-h6
- **空元素**:即系没有内容的 HTML 元素，例如：br、meta、hr、link、input、img

> 强制转换成块元素
> display：block
> 强制转换成行内元素
> display：inline
> 强制转换成行内扩张元素
> display：inline-block

#### CSS3 新特性有哪些？

- **弹性布局 flex**
- **栅格布局 grid**
- **选择器**
- **过渡**
- **动画**
- **媒体查询**

#### CSS3 选择器有哪些？

- **属性选择器**
- **结构性伪类选择器—root**: 等同于`<html>`元素
- **结构性伪类选择器—not**: 可以选择除某个元素之外的所有元素
- **结构性伪类选择器—empty**:用来选择没有任何内容的元素
- **结构性伪类选择器—target**: 用来匹配文档(页面)的 url 的某个标志符的目标元素。
- **结构性伪类选择器—first-child**: 选择元素中的第一个子元素
- **结构性伪类选择器—last-child**:选择元素的最后一个子元素
- **结构性伪类选择器—nth-child(n)**:定位某个父元素的一个或多个特定的子元素
- **only-child 选择器**:选择父元素中只有一个子元素，而且只有唯一的一个子元素。
- ......

#### 移动端优先使用弹性布局（flex）来解决布局问题，请列出弹性布局的相关属性，并说明属性用途

- **flex-direction**

> flex-direction 属性决定主轴的方向（即项目的排列方向）。
>
> - `row`（默认值）：主轴为水平方向，起点在左端。
>
> - `row-reverse`：主轴为水平方向，起点在右端。
> - `column`：主轴为垂直方向，起点在上沿。
> - `column-reverse`：主轴为垂直方向，起点在下沿。

- **flex-wrap**

> flex-wrap 属性定义，如果一条轴线排不下，如何换行。
>
> - `nowrap`（默认）：不换行。
> - `wrap`：换行，第一行在上方。
> - `wrap-reverse`：换行，第一行在下方。

- **flex-flow**

> `flex-flow`属性是`flex-direction`属性和`flex-wrap`属性的简写形式，默认值为`row nowrap`。

- **justify-content**:

> `justify-content`属性定义了项目在主轴上的对齐方式。
>
> - `flex-start`（默认值）：左对齐
> - `flex-end`：右对齐
> - `center`： 居中
> - `space-between`：两端对齐，项目之间的间隔都相等。
> - `space-around`：每个项目两侧的间隔相等。所以，项目之间的间隔比项目与边框的间隔大一倍。

- **align-items**

> `align-items`属性定义项目在交叉轴上如何对齐。
>
> - `flex-start`：交叉轴的起点对齐。
> - `flex-end`：交叉轴的终点对齐。
> - `center`：交叉轴的中点对齐。
> - `baseline`: 项目的第一行文字的基线对齐。
> - `stretch`（默认值）：如果项目未设置高度或设为 auto，将占满整个容器的高度。

- **align-content**

> ​ `align-content`属性定义了多根轴线的对齐方式。如果项目只有一根轴线，该属性不起作用。
>
> - `flex-start`：与交叉轴的起点对齐。
> - `flex-end`：与交叉轴的终点对齐。
> - `center`：与交叉轴的中点对齐。
> - `space-between`：与交叉轴两端对齐，轴线之间的间隔平均分布。
> - `space-around`：每根轴线两侧的间隔都相等。所以，轴线之间的间隔比轴线与边框的间隔大一倍。
> - `stretch`（默认值）：轴线占满整个交叉轴。

#### CSS3 的兼容问题怎么处理？

```css
-moz-border-radius: 2px; /* Firefox */
-webkit-border-radius: 2px; /* Safari 和 Chrome */
border-radius: 2px; /* Opera 10.5+, 以及使用了IE-CSS3的IE浏览器 */
-o-border-radius: 2px;
-khtml-border-radius: 2px; /* 针对Konqueror浏览器 */
```

#### CSS3 动画和 JS 动画主要的不同点是什么？

- **CSS 动画**

> **优点**:
>
> 浏览器可以对动画进行优化。
>
> 浏览器使用与 requestAnimationFrame 类似的机制，requestAnimationFrame 比起 setTimeout，setInterval 设置动画的优势主要是:
>
> - requestAnimationFrame 会把每一帧中的所有 DOM 操作集中起来，在一次重绘或回流中就完成,并且重绘或回流的时间间隔紧紧跟随浏览器的刷新频率,一般来说,这个频率为每秒 60 帧。
> - 在隐藏或不可见的元素中 requestAnimationFrame 不会进行重绘或回流，这当然就意味着更少的的 cpu，gpu 和内存使用量。
>
> 强制使用硬件加速 （通过 GPU 来提高动画性能）
>
> **缺点**:
>
> - 运行过程控制较弱,无法附加事件绑定回调函数。CSS 动画只能暂停,不能在动画中寻找一个特定的时间点，不能在半路反转动画，不能变换时间尺度，不能在特定的位置添加回调函数或是绑定回放事件,无进度报告
> - 代码冗长。想用 CSS 实现稍微复杂一点动画,最后 CSS 代码都会变得非常笨重。

- **JS 动画**

> **优点**:
>
> - JavaScript 动画控制能力很强, 可以在动画播放过程中对动画进行控制：开始、暂停、回放、终止、取消都是可以做到的。
> - JS 动画的效果比 css3 动画丰富,有些动画效果，比如曲线运动,冲击闪烁,视差滚动效果，只有 JavaScript 动画才能完成
> - CSS3 有兼容性问题，而 JS 大多时候没有兼容性问题
>
> **缺点**:
>
> - JavaScript 在浏览器的主线程中运行，而主线程中还有其它需要运行的 JavaScript 脚本、样式计算、布局、绘制任务等,对其干扰导致线程可能出现阻塞，从而造成丢帧的情况。
> - JS 动画代码的复杂度高于 CSS 动画

#### 请用 Css 写一个简单的幻灯片效果页面

> .......

#### Rem 的使用方法

- 简易 JS

  ```javascript
  (function (doc, win) {
  	var docEl = doc.documentElement,
  		resizeEvt =
  			"orientationchange" in window ? "orientationchange" : "resize",
  		recalc = function () {
  			if (docEl.clientWidth > 750) {
  				docEl.style.fontSize = "100px";
  				doc.getElementById("app").style.width = "750px";
  			} else {
  				var width = docEl.clientWidth / 7.5;
  				docEl.style.fontSize = width + "px";
  				doc.getElementById("app").style.width = "auto";
  			}
  		};
  	if (!doc.addEventListener) return;
  	win.addEventListener(resizeEvt, recalc, false);
  	doc.addEventListener("DOMContentLoaded", recalc, false);
  })(document, window);
  ```

- postcss-px2rem

#### 用 css 画一个三角形，圆，椭圆？

> ......

#### html5 有哪些新特性、移除了那些元素？如何处理 HTML5 新标签的浏览器兼容问题？

**html5 新增**

- 语义化标签
- 增强型表单
- 新增视频 `<video>` 和音频 `<audio>` 标签
- Canvas 绘图
- SVG 绘图
- 地理定位
- 拖放 API
- Web Worker
- Web Storage
- WebSocket

**新元素**

- header
- footer
- nav
- section
- time
- aside
- ......

**移除的元素**

- 纯表现的元素：basefont，big，center，font, s，strike，tt，u；
- 对可用性产生负面影响的元素：frame，frameset，noframes；

#### HTML5 中新增的操作 DOM 的方法？

- document.querySelector(" ");　　 单个元素获取
- document.querySelectorAll(" "); 　　多个元素获取
- 加：

```
box.classList.add("active");
```

- 删：

```
box.classList.remove("active");
```

- 判断：

```
box.classList.contains("active")； >>>>返回值是一个布尔值，true or false
```

- 切换：

```
box.classList.toggle("active");
```

#### image 和 canvas 在处理图片的时候有什么区别？

> ......

#### HTML5 中的本地存储概念是什么？生命周期有多长？

> html5 中的 Web Storage 包括了两种存储方式：sessionStorage 和 localStorage。
>
> sessionStorage 用于本地存储一个会话中的数据，这些数据只有在同一个会话中的页面才能访问并且当会话结束后数据也随之销毁，因此 sessionStorage 不是一种持久化的本地存储，仅仅是会话级别的存储。
>
> 而 localStorage 用于持久化的本地存储，除非主动删除数据，否则数据是永远不会过期的。
>
> cookie 是网站为了标示用户身份而储存在用户本地终端上的数据（通常经过加密）。
