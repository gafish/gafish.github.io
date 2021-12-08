---
title: "群晖折腾手记四：搭建离线下载服务"
description:
keywords:
 - synology
 - synology 720+
 - 群晖 720+
toc: true
authors: []
tags: []
categories: 生活
series: []
date: 2021-11-22T21:00:56+08:00
lastmod: 2021-11-22T21:00:56+08:00
featuredVideo:
featuredImage:
draft: false
url: /posts/2021/11/22/synology-download
---

都用上了 群晖NAS ，那下载是逃不过去的一个服务，群晖的官方套件 `Download Station` 为我们提供了功能强大，上手简单的离线下载功能，虽然很多人诟病它下载慢，但作为入门级的离线下载功能，它还是值得我们来体验下的。

## 安装与启动

在安装之前，我们最好先在 `共享文件夹` 下新建一个下载目录，如：`download`，后面会用到

![](/images/2021-11-22-synology-download/1.jpg)

在套件中心搜索 `download station` 并安装，完成后会自动启动服务

![](/images/2021-11-22-synology-download/2.jpg)

打开 `download station` 会让我们选择一个默认下载目录，这里就可以选择一开始我们创建好的 `download` 目录

![](/images/2021-11-22-synology-download/3.jpg)

在默认选项下使用 `download station` 就可以开始下载了，点击+号添加下载任务，支持普通的网址下载、BT种子下载、磁力下载等

![](/images/2021-11-22-synology-download/4.jpg)

## BT搜索

在左上角有BT搜索功能，但默认的搜索引擎经常会搜索不到结果

![](/images/2021-11-22-synology-download/5.jpg)

我们可以在 `设置` - `BT搜索` 中添加其它的搜索引擎模块，有2种方式可以方便的找到网络上的BT搜索引擎模块

1. 在 github 中搜索 `synology-dlm`，可以找到很多开源代码的 dlm 包
2. 在 [synoboost.com](http://www.synoboost.com/) 中直接下载模块

这里我搜罗了一些现成的模块方便大家下载，[点击下载](/images/2021-11-22-synology-download/dlm.zip)

![](/images/2021-11-22-synology-download/6.jpg)

添加了新的搜索引擎模块后，最好把默认提供的2个搜索引擎模块删除，这样可以更加快速的搜索到结果

![](/images/2021-11-22-synology-download/7.jpg)

## 加速配置

默认配置下使用 `Download Station` 来下载文件，速度上确实不快，但也不是没有办法，我们可以通过添加 `Tracker服务器` 的方式来提速，最新的Tracker列表可以在[这里下载](https://raw.githubusercontent.com/ngosang/trackerslist/master/trackers_best.txt)

![](/images/2021-11-22-synology-download/8.jpg)

上面链接中复制过来的列表需要删除空格才能使用，这里我就直接将列表复制过来了

```
http://p4p.arenabg.com:1337/announce
udp://tracker.opentrackr.org:1337/announce
udp://9.rarbg.com:2810/announce
udp://open.tracker.cl:1337/announce
udp://exodus.desync.com:6969/announce
udp://tracker.openbittorrent.com:6969/announce
http://tracker.openbittorrent.com:80/announce
http://openbittorrent.com:80/announce
udp://www.torrent.eu.org:451/announce
udp://vibe.sleepyinternetfun.xyz:1738/announce
udp://udp-tracker.shittyurl.org:6969/announce
udp://u.wwwww.wtf:1/announce
udp://tracker1.bt.moack.co.kr:80/announce
udp://tracker0.ufibox.com:6969/announce
udp://tracker.zerobytes.xyz:1337/announce
udp://tracker.torrent.eu.org:451/announce
udp://tracker.tiny-vps.com:6969/announce
udp://tracker.theoks.net:6969/announce
udp://tracker.srv00.com:6969/announce
udp://tracker.pomf.se:80/announce
```

## 实用工具

我所使用的环境是 Mac，所以在下载到 Windows 自解压文件后就有点麻烦，这里推荐一个实用的解压工具：[The Unarchiver](https://apps.apple.com/cn/app/the-unarchiver/id425424353?l=en&mt=12)，免费并且支持 .exe 自解压格式，非常方便

![](/images/2021-11-22-synology-download/9.jpg)

## 资料参考

- [https://blog.myds.cloud/archives/%E7%BE%A4%E6%99%96%E4%B8%8B%E8%BD%BD%E5%99%A8%E6%B7%BB%E5%8A%A0bt%E6%90%9C%E7%B4%A2%E5%BC%95%E6%93%8E.html](https://blog.myds.cloud/archives/%E7%BE%A4%E6%99%96%E4%B8%8B%E8%BD%BD%E5%99%A8%E6%B7%BB%E5%8A%A0bt%E6%90%9C%E7%B4%A2%E5%BC%95%E6%93%8E.html)
- [https://www.kocpc.com.tw/archives/60972](https://www.kocpc.com.tw/archives/60972)
- [https://post.smzdm.com/p/aqno9lwx/](https://post.smzdm.com/p/aqno9lwx/)