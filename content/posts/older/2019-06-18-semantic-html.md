---
title: "HTML5语义化开发指南"

toc: true
date:  2019-06-18T22:11:00+08:00
description: ""
author: "gafish"
categories:
  - "编程开发"
keywords:
 - "HTML语义化"
url: "/older/semantic-html/"

---

## 为什么要做 HTML5 语义化

HTML5的主要进步之一是引入了一组标准化的语义元素。

”语义元素“是用于以更有意义的方式标记文档结构的元素，这种方式可以清楚地表明它们的用途和目的是什么。而且重要的是，由于它们是标准化的，定义文档的这些元素可以被每个人使用并理解，包括机器人。

在web无障碍开发领域，给视障用户使用的屏幕阅读器是视障群体访问网络的必备工具，合理的 HTML5 语义化元素，会让屏幕阅读器正确的理解网页的内容，从而以最为合适的方式朗读。

站在开发者的角度，写出符合 HTML5 语义化的结构，也是显示我们职业素养的一种方式，最为重要的是这样的代码自带翻译，比如下面的div结构，为了让开发者明白div的含义，我们必须在class命名上下功夫。

```
<div class="header">
    <h1>Super duper best blog ever</h1>
    ...
</div>
<div class="main">
    <h2>Why you should buy more cheeses than you currently do</h2>
    ...
</div>
<div class="footer">
    Contact us!
    <div class="contact-info">this.is.us@example.com</div>
</div>

```

而如果采用语义化元素，结构一目了然，不管是日后维护还是交接给他人，都是件轻松的事情。

```
<header>
    <h1>Super duper best blog ever</h1>
    ...
</header>
<main>
    <h2>Why you should buy more cheeses than you currently do</h2>
    ...
</main>
<footer>
    Contact us!
    <div class="contact-info">this.is.us@example.com</div>
</footer>

```

先来回顾一下 HTML5 有哪些元素（根据 MDN 资料整理）

## HTML5 元素大全

### 文档元素

- html: HTML 文档中最外层的元素，也可称为根元素。

### 文档元数据

- head: 表示文档的头部
- title: 用来定义文档的标题
- base: 为页面上的所有的相对链接规定默认 URL 或默认目标
- link: 定义文档与外部资源的关系
- meta: 提供了 HTML 文档的元数据
- style: 用于表示文档所使用的样式

### 区块

- body: 表示文档的内容
- article: 表示文档、页面、应用或网站中的独立结构
- section: 表示文档中的一个区域（或节）
- nav: 描绘一个含有多个超链接的导航栏区域
- aside: 表示一个和其余页面内容几乎无关的部分
- Heading_Elements: 标题(Heading)元素呈现了六个不同的级别的标题，`<h1>` 级别最高，而 `<h6>` 级别最低
- footer: 表示最近一个章节内容或者根节点（sectioning root ）元素的页脚
- header: 用于展示介绍性内容

### 内容分组

- p: 表示文本的一个段落
- address: 表示其中的内容提供了某个人或某个组织（等等）的联系信息
- hr: 表示段落级元素之间的主题转换
- pre: 表示预定义格式文本
- blockquote: 表示其中的文字是引用内容
- ol: 表示多个元素的有序列表
- ul: 表示多个元素的无序列表
- li: 表示列表里的条目
- dl: 表示一个包含术语定义以及描述的列表
- dt: 用于在一个定义列表中声明一个术语
- dd: 用来指明一个描述列表元素中一个术语的描述
- figure: 代表一段独立的内容
- figcaption: 与其相关联的图片的说明/标题
- main: 呈现了文档的 `<body>` 或应用的主体部分
- div: 通用型的流内容容器，它应该在没有任何其它语义元素可用时才使用

### 文本级语义

- a: 定义超链接，用于从一个页面链接到另一个页面
- em: 标记出需要用户着重阅读的内容
- strong: 表示文本十分重要
- small: 表示边注释和附属细则，包括版权和法律文本
- s: 表示不再相关，或者不再准确的事情
- cite: 表示一个作品的引用
- q: 表示一个封闭的并且是短的行内引用的文本
- dfn: 表示术语的一个定义
- abbr: 用于展示缩写
- ruby: 用来展示东亚文字注音或字符注释
- rb: 用于分隔
- ruby: 注释的基本文本组件
- rt: 包含字符的发音
- rtc:  包含 `<ruby>` 元素中文字的语义注解
- rp: 用于为那些不能使用 `<ruby>` 元素展示 ruby 注解的浏览器
- data: 将一个指定内容和机器可读的翻译联系在一起
- time: 用来表示24小时制时间或者公历日期
- code: 呈现一段计算机代码
- var: 表示变量的名称，或者由用户提供的值
- samp: 用于标识计算机程序输出
- kbd: 表示用户输入
- sub: 定义了一个下标文本区域
- sup: 定义了一个上标文本区域
- i: 用于表现因某些原因需要区分普通文本的一系列文本
- b: 用于吸引读者的注意到该元素的内容上
- u: 表示具有未标注的文本跨度，显示渲染，非文本注释
- mark: 用来表示上下文的关联性的而突出显示的文字
- bdi: 隔离可能以不同方向进行格式化的外部文本
- bdo: 用于覆盖当前文本的朝向
- span: 短语内容的通用行内容器，并没有任何特殊语义
- br: 在文本中生成一个换行（回车）符号
- wbr: 一个文本中的位置，其中浏览器可以选择来换行

### 修改记录

- ins: 定义已经被插入文档中的文本
- del: 表示一些被从文档中删除的文字内容

### 嵌入内容

- picture: 通过包含零或多个 `<source>` 元素和一个 `<img>` 元素来为不同的显示/设备场景提供图像版本
- source: 为 `<picture>`, `<audio>` 或者 `<video>` 元素指定多个媒体资源
- img: 代表文档中的一个图像
- iframe: 表示嵌套的浏览上下文，有效地将另一个HTML页面嵌入到当前页面中
- embed: 将外部内容嵌入文档中的指定位置。此内容由外部应用程序或其他交互式内容源（如浏览器插件）提供
- object: 表示引入一个外部资源，这个资源可能是一张图片，一个嵌入的浏览上下文，亦或是一个插件所使用的资源
- param: 为`<object>`元素定义参数
- video: 用于支持文档内的视频播放
- audio: 用于在文档中表示音频内容
- track: 指定计时字幕（或者基于时间的数据）
- map: 与 `<area>` 属性一起使用来定义一个图像映射(一个可点击的链接区域)
- area: 在图片上定义一个热点区域，可以关联一个超链接

### 表格数据

- table: 表示表格数据
- caption: 展示一个表格的标题
- colgroup: 用来定义表中的一组列表
- col: 定义表格中的列，并用于定义所有公共单元格上的公共语义
- tbody: 表示它们包含表的主体
- thead: 定义了一组定义表格的列头的行
- tfoot: 定义了一组表格中各列的汇总行
- tr: 定义表格中的行
- td: 定义包含数据的表格的单元格
- th: 定义表格内的表头单元格

### 表单

- form: 示了文档中的一个区域，这个区域包含有交互控制元件
- label: 表示用户界面中某个元素的说明
- input: 用于为基于Web的表单创建交互式控件，以便接受来自用户的数据
- button: 表示一个可点击的按钮
- select: 表示一个控件，提供一个选项菜单
- datalist: 包含了一组`<option>`元素，这些元素表示其它表单控件可选值
- optgroup: 创建包含在一个 `<select>` 元素中的一组选项
- option: 用于定义在`<select>`,  `<optgroup>` 或`<datalist>` 元素中包含的项
- textarea: 表示一个多行纯文本编辑控件
- output: 表示计算或用户操作的结果
- progress: 用来显示一项任务的完成进度
- meter: 用来显示已知范围的标量值或者分数值
- fieldset: 用来对表单中的控制元素进行分组
- legend: 用于表示它的父元素`<fieldset>`的内容的标题

### 交互元素

- details: 可创建一个挂件，仅在被切换成展开状态时，它才会显示内含的信息
- summary: 用作 一个`<details>`元素的一个内容的摘要，标题或图例
- dialog: 表示一个对话框或其他交互式组件

### 脚本元素

- script: 用于嵌入或引用可执行脚本
- noscript: 定义脚本未被执行时的替代内容
- template: 用于保存客户端内容机制，该内容在加载页面时不会呈现
- canvas: 用来通过脚本（通常是JavaScript）绘制图形
- slot: 是 Web Components 技术套件的一部分，是Web组件内的一个占位符

## 基本布局

```
<html>
    <head>
        <title>示例页面</title>
    </head>
    <body>
        <div>
            <header>
                <h1>我的网站</h1>
                <nav>
                    <a href="">首页</a>
                    <a href="">文章</a>
                    <a href="">留言</a>
                </nav>
                <aside>
                    <img src="<https://via.placeholder.com/30.png/09f/fff>" alt="用户头像">
                </aside>
            </header>
            <div>
                <main>
                    <article>
                        <section>
                            <h2>文章标题11111</h2>
                            <p>巴拉巴拉巴拉巴拉巴拉巴拉巴拉</p>
                        </section>
                        <section>
                            <h2>文章标题2222</h2>
                            <p>巴拉巴拉巴拉巴拉巴拉巴拉巴拉</p>
                        </section>
                        <section>
                            <h2>文章标题3333</h2>
                            <p>巴拉巴拉巴拉巴拉巴拉巴拉巴拉</p>
                        </section>
                    </article>
                    <ul>
                        <a href="" title="第1页">1</a>
                        <a href="" title="第2页">2</a>
                        <a href="" title="第3页">3</a>
                    </ul>
                </main>
                <aside>
                    <section>
                        <h2>作者介绍</h2>
                        <p>巴拉巴拉巴拉巴拉巴拉巴拉巴拉</p>
                    </section>
                    <nav>
                        <a href="">HTML</a>
                        <a href="">JS</a>
                        <a href="">CSS</a>
                    </nav>
                </aside>
            </div>
        </div>
        <footer>
            <address>
                xxxx@xxx.com <br />
                <a href=""><https://twitter.com/home></a>
            </address>
        </footer>
    </body>
</html>

```

## article 、 section 、 div 的用法区别

- 如果元素内容可以分为几个部分的话，应该使用 `<article>` 而不是 `<section>`。
- 如果内容中的几个部分是互相独立的，应该使用 `<article>` 嵌套，几个部分的内容之间是关联的应该使用 `<section>`。
- 不要把 `<section>` 元素作为一个普通的容器来使用，这是本应该是`<div>`的用法（特别是当片段仅仅是为了美化样式的时候）。

    *MacOs VoiceOver 读屏软件对3个元素的朗读方式没有区别，都是直接读取内部的内容。*

## section 、 figure 的用法区别

section 和 figure 有相似的地方，都可以表示一个区域，结构上也相似，都可以有标题和内容，但两个元素的用法是完全不一样的。

- section 的内容跟上下文结构存在关联关系，figure 的内容是独立存在的一部分，把 figure 移除不影响主体内容的表达；
- section 中存在标题只能在开始的位置，figure 中的标题可以在开头也可以在结尾；

    *MacOs VoiceOver 读屏软件会把 section 的标题说成“标题”，但对 figure 的标题会说成“文本”。*

## header 、footer 不止表示页头页尾

通常的用法都是把一个页面的页头用header，页尾用footer来表示，但这并不是它们的唯一用法，根据元素的定义，它们表示的是章节或区块的头和尾，严格来说一个`<article>` 元素的头部需要用 header 来表示，如：

```
<article>
    <header>
        <h2>我们是相亲相爱的一家人</h2>
    </header>
    <p>.....</p>
</article>

```

但以上这种 header 中只有一个 h2 的场景中 header 是可以忽略的。

*MacOs VoiceOver 读屏软件对 div 中的 header 会说“横幅”，而对 article 、section 中的 header 会*忽略，直接读    内部的内容。

## 不是所有的导航链接都需要 nav

只用来将一些热门的链接放入 `<nav>` 导航栏，建议这些链接应该是跟当前页面或站点有较强的关联性。例如 `<footer>` 元素就常用来在页面底部包含一个不常用到，没必要加入 `<nav>` 的链接列表。

    *MacOs VoiceOver 读屏软件遇到 nav 时会先说“导航“，下一步读取内部的内容，最后会说”导航的结尾“。*

## address 的内容不只是地址

HTML `<address>` 元素 表示其中的内容提供了某个人或某个组织的联系信息，包括真实地址、URL、电子邮箱、电话号码、社交媒体账号、地理坐标等等，通过它会被放到 footer 里，但这并不是唯一的用法，在页头 header 中，article 或其它区块中需要显示联系信息的地方都可以使用 address。

    *MacOs VoiceOver 读屏软件遇到 address 只是当作普通文本朗读。*

## em 、 strong 、 b 、 i 、 mark 的用法区别

这几个元素表示的都是对文本内容的强调，但强调的含义是不一样的

- em 强调的是语句的重心，如“我`<em>`今天`</em>`吃薯条了”、“我今天吃`<em>`薯条`</em>`了”；
- strong 强调的是一句话中重要的一定要看的部分，如"每天早上9点打卡，`<strong`迟到者罚款1000元`</strong>`"；
- b 强调的是视觉上需要吸引用户来看的内容，类似广告语，对用户来说并不一定很重要；
- i 强调的是一段文本中，某些部分需要跟周边的文本做一些视觉上区别，但不一定是吸引人的；
- mark 强调的是上下文的关联性，如搜索关键字；

    *MacOs VoiceOver 读屏软件遇到这5个元素时只是当作普通文本朗读。*

## small 、 s 、 u 还能用吗

这三个元素在 HTML5 之前，都是为了表示明显的排版视觉效果，HTML5 中保留下来并添加了新的语义

- small 用来描述对内容的注释，如版权和法律文本等；
- s 用来表示不再相关或不再准确的事，如之前对某句话的解释，很多年之后已经不适用，但要保留在内容中的时候；
- u 用来标记中文文本中的专有名称，或将文本标记为拼写错误；

建议在除了上面提到的几个特殊用途之外，不再使用这三个元素；

    *MacOs VoiceOver 读屏软件遇到这3个元素时只是当作普通文本朗读。*

## blockquote 、 q 、 cite 都表示引用，如何区分

- blockquote 引用的是长文本；
- q 引用的是短文本；
- cite 引用的是一个作品的名称或链接；

    *MacOs VoiceOver 读屏软件遇到这3个元素时只是当作普通文本朗读。*

## 什么时候使用 div

根据元素的定义，只有在所有 html5 标签都不适用于你想表达的语义时，这时候才使用终极大法 div，从这个角度来说，目前对 div 元素的滥用其实是程序员偷懒的一种表现，反正有 div 兜底，也就懒得去思考那些语义元素的区别。

在追求开发效率和做不完的需求面前，使用 div 兜底也是很多人无奈的选择，我觉得这个是可以理解，某种程度上也可以接受的，但进一步去想一想，你的产品面向的用户也有可能会是存在各种行为障碍的视障、残障人群，他们无法像正常人那样使用你开发的功能，而需要借助类似于屏幕阅读器这样的辅助工具，这时候才是真正考验你的产品是否合格的时候。

我们做语义化开发，很大程度上就是在帮助更多人的人正常的使用我们的产品，同时也会让你离专业的程序员更进一步。

## 参考资料

- [https://www.w3.org/TR/html53/](https://www.w3.org/TR/html53/)
- [https://www.w3cschool.cn/html5/](https://www.w3cschool.cn/html5/)
- [https://juejin.im/post/5cb1a7af5188251b0c653736](https://juejin.im/post/5cb1a7af5188251b0c653736)