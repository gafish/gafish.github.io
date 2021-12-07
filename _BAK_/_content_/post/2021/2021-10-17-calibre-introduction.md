---
title: "Calibre 入门指南"
date: 2021-10-17T11:00:52+08:00
end: 2021-10-26T09:20:00+08:00
description: "本文通过介绍 Calibre 添加、管理、分享功能，帮助大家了解 Calibre 的基本操作"
author: "gafish"
categories:
  - "折腾爱好"
keywords:
 - calibre
 - Calibre
 - Calibre 入门
 - Calibre 中文
 - Calibre 教程
url: "/2021/10/17/calibre-introduction"

---

Calibre 是一款功能强大且易于使用的电子书管理器，它可以帮助你管理你的电子书，并且可以自动生成电子书的索引。

具体的功能列表如下：

- 可以管理各种类别的电子书，office文档等。
- 可以制作电子书
- 可以导出到kindle等设备中
- 可以对电子书，文档等实现标签管理
- 可以对阅读电子书，标注，编辑图书信息
- 可以实现RSS订阅阅读
- 可以分享你的书目

作为一个入门指南，本文将介绍如何使用 Calibre 制作电子书，并且对电子书进行管理，分享等操作。

本文所使用的环境及版本

- MacOS Big Sur 11.6
- Calibre 5.30

## 安装 Calibre

1. 从官网下载 Calibre 安装包。[MacOS下载页面](https://calibre-ebook.com/zh_CN/download_osx)

*注意：从官网的链接地址下载可能会比较慢，推荐使用 备用下载位置#2 或者 使用迅雷下载*
![](/images/2021-10-17-calibre-introduction/1.jpg)

2. 打开下载好的 *osx.dmg* 文件，将右侧的 *calibre.app* 文件夹拖拽到左侧的 *Applications* 文件夹中。

![](/images/2021-10-17-calibre-introduction/2.jpg)

3. 安装好之后就可以在应用列表中打开 Calibre

![](/images/2021-10-17-calibre-introduction/3.jpg)

## 制作第一本电子书

Clibre 可以制作的电子书格式有：Azw3、Docx、Epub、MD、TXT

在开始制作电子书前，我们需要准备好电子书的内容，这里假设我们将要制作一本《宋词精选》，内容参照网络资源: [http://www.shuzhai.org/gushi/song/](http://www.shuzhai.org/gushi/song/)，准备就绪，那我们就开始吧。

1. 点击 *添加书籍* 右侧的下拉框，选择 *添加空白书籍*

![](/images/2021-10-17-calibre-introduction/4.jpg)

2. 填写电子书基本信息

![](/images/2021-10-17-calibre-introduction/5.jpg)

3. 生成后可以在列表中看到新添加的电子书，点击右键 *编辑书籍*

![](/images/2021-10-17-calibre-introduction/6.jpg)

4. 进入到书籍编辑器窗口

![](/images/2021-10-17-calibre-introduction/7.jpg)

5. 双击左侧的 *start.xhtml* 会看到一个 HTML 编辑器，在这里编辑电子书的内容

![](/images/2021-10-17-calibre-introduction/8.jpg)

看到这里，如果你是个像我一样的程序员，那应该是非常熟悉了，这里所要做的就是编辑 HTML 代码，这里可以使用你最喜欢的编辑器，比如 *Sublime Text* 或者 *VSCode* 在本地编辑好再复制过来，但对于没有编程基础的人来说，可能就有点难度了。

6. 编辑完电子书的内容后，点左上角的保存按钮或者按下 *CMD+S* 就可以保存了

![](/images/2021-10-17-calibre-introduction/9.jpg)

7. 回到 Calibre 列表页，双击打开我们刚编辑的电子书就可以开始阅读了

![](/images/2021-10-17-calibre-introduction/10.jpg)

好了，作为一个入门指南，我们已经完成了制作一本电子书的基本过程，如果希望电子书做的更加精美，可以多尝试书籍编辑器里提供的其它功能，或者后续我们再出一个高级教程。

## 管理电子书

如果你像我一样收藏了几百本PDF格式的电子书，那应该经常会为如何管理这些电子书而头疼，我最开始就是放在移动硬盘里，按类型目录划分不同类型的书籍，但有些书籍属于跨类型的，又不好在两个类型目录里各放一本，还有比如我没办法按作者来检索书籍等等，这时候就需要用到 *Calibre* 的电子书管理功能了。

1. 从文件夹中添加书籍，本文以添加 PDF 电子书为例，从电脑上选择三本小说

![](/images/2021-10-17-calibre-introduction/11.jpg)
![](/images/2021-10-17-calibre-introduction/12.jpg)

2. 编辑书籍信息，Calibre 通过编辑书籍元数据的方式为每本书籍补充信息，我们可以在元数据中手动给书籍补充完整的信息，当然这会比较累

![](/images/2021-10-17-calibre-introduction/13.jpg)

3. 自动下载元数据，Calibre 为我们提供了下载元数据的功能，我们可以从以下数据源下载元数据（**需要开全局翻墙代理**）：

![](/images/2021-10-17-calibre-introduction/14.jpg)

通过点击“下载元数据”按钮，默认会以书名+作者的方式查找网络上的书籍元数据，我们在返回的结果中选择对应的元数据，点确定后再选择一个书籍封面，就可以将元数据信息自动填充到我们的书籍信息中

![](/images/2021-10-17-calibre-introduction/15.jpg)

这里有一个问题，搜索到的书籍信息可能会非常多，需要我们肉眼去辨识哪本书最合适比较耗时费力，我推荐一种更简单的办法，先打开电子书，找到书籍的 *ISBN* 号码，只需要数字部分

![](/images/2021-10-17-calibre-introduction/16.jpg)

在编辑元数据时，先手动输入书籍的 *ISBN* 号码，然后再点击“下载元数据”按钮，这时候搜索出来的结果就非常精准了

![](/images/2021-10-17-calibre-introduction/17.jpg)
![](/images/2021-10-17-calibre-introduction/18.jpg)

4. 网络上搜索的元数据也可能不太全面，剩下的部分就需要我们手动来补充了，比如 *星级*、*标签*、*丛书* 等等，以刚才添加的小说为例，我们为它添加 *小说*、*科幻* 标签

![](/images/2021-10-17-calibre-introduction/19.jpg)

点确定后，我们就可以看到左侧面板有了2个刚才我们添加的标签，**这里要重点提一下，Calibre 在管理书籍时，没有我们平常习惯的目录概念，而主要是通过标签的方式来分类，所以无法用常规的一类目录、二类目录的方式来管理图书**

## 分享电子书

Calibre 可以启动一个网络服务器，提供给用户在线阅读、下载电子书，接下将讲解如何使用这个功能

1. 通过点击 “连接/共享” => "启动内容服务器" 可以在本机启动一个网络服务器

![](/images/2021-10-17-calibre-introduction/20.jpg)

2. 当 “连接/共享” 变成绿色时，表示服务器已经启动，可以通过再次点击 “连接/共享” 查看服务器的地址，如本教程中的地址就是：*http://10.0.1.28:8080/*

![](/images/2021-10-17-calibre-introduction/21.jpg)

3. 在浏览器中打开刚才启动的网络地址：*http://10.0.1.28:8080/* 就可以看到一个在线的电子书网站，通过在线网站我们可以在线阅读、下载电子书，甚至可以在线编辑电子书元数据、删除电子书等操作

![](/images/2021-10-17-calibre-introduction/22.jpg)

## 结语

本文通过介绍 Calibre 添加、管理、分享功能，帮助大家了解 Calibre 的基本操作，作为一个入门指南，我们只是看到了 Calibre 强大功能的冰山一角，还有很多更强大的功能等着我去探索，后续随着使用的深入，我还会再写一些文章，敬请期待！


## 资料参考

- 官网：[https://calibre-ebook.com/](https://calibre-ebook.com/)
- 中文：[https://calibre-ebook.com/zh_CN](https://calibre-ebook.com/zh_CN)