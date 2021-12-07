---
title: "群晖折腾手记三：搭建个人网络音乐库"
date: 2021-11-21T16:10:06+08:00
description: ""
author: "gafish"
categories:
  - "记录折腾"
keywords:
 - synology
 - synology 720+
 - 群晖 720+
url: "/2021/11/21/synology-audio"
---

在当今互联网音乐盛行的年代，可能很多人都已经忘了曾经的我们是怎样听歌的，录音机、磁带、唱片光盘、VCD、MP3播放机、百度MP3、Winamp、千千静听，这些古董，估计当今的00后听都没听过，而这些伴随了我们很多人的成长。

现在的听歌方式都是各种音乐在线服务，像网易云音乐、酷狗音乐、QQ音乐，这些在线音乐服务，可以让你听音乐更加简单，更加方便，但同时因为版权的问题，也会让听歌更加费劲，为了你喜欢的歌曲，你可能需要在手机上安装好几个音乐APP。

如果说上面这个问题还不算问题，那对我而言，更大的问题是我喜欢的很多音乐因为敏感原因而导致下架，要想听就只能下载到本地播放，为解决这种种问题，搭建个人网络音乐库就势在必行，那今天，我就开始借助群晖强大的音乐管理功能来实现这个目标。

## 音乐服务器

打开群晖套件中心，搜索 `Audio Station` 并点击安装，这个音乐服务器是群晖的音乐管理功能，它可以让你更加方便的管理音乐

![](/images/2021-11-21-synology-audio/1.jpg)

安装好之后，打开 `Audio Station` 就会启动网络音乐服务

![](/images/2021-11-21-synology-audio/2.jpg)

打开 `File Station` 会看到一个 `music` 的文件夹，这个文件夹是你的音乐文件夹，你可以在这里通过在线上传或者局域网复制的方式添加你喜欢的音乐文件

![](/images/2021-11-21-synology-audio/3.jpg)

## 电脑音乐播放器

`Audio Station` 本身就是一个音乐播放器，在你添加好音乐之后，在 `所有音乐` 中就能看到你添加的音乐文件列表，直接点击就可以播放

![](/images/2021-11-21-synology-audio/4.jpg)

你也可以通过创建 `播放列表` 来归类你喜欢的音乐

![](/images/2021-11-21-synology-audio/5.jpg)

我特别推荐这里的 `智能播放列表` 功能，它可以通过一系列规则，为你智能匹配歌曲，比如你可以创建一个 `最近30天添加的歌曲`

![](/images/2021-11-21-synology-audio/6.jpg)

## 歌词插件

当你此时通过 `Audio Station` 来听歌时，你可能会发现，经常会没有歌词可用

![](/images/2021-11-21-synology-audio/7.jpg)

这是因为默认的歌词插件 `LyricWiki` 非常不好用，你可以在 `设置-歌词插件` 中，通过新增第三方歌词插件的方式来解决这个问题，比如我用的 [网易云歌词插件](https://github.com/LudySu/Synology-LrcPlugin)

![](/images/2021-11-21-synology-audio/8.jpg)

新增了歌词插件之后，最好关闭 `Audio Station`，重新再打开一次，这样就可以看到歌词了

![](/images/2021-11-21-synology-audio/9.jpg)

## 手机音乐APP

光在电脑上听歌肯定不能满足我们的需求，在手机上听才是目标，从应用商店下载 `DS Audio`，通过我们前期设置好的账号密码，就可以登录到 `DS Audio` 了

![](/images/2021-11-21-synology-audio/10.jpg)

登录后就可以看到跟电脑端一样的音乐列表，选择音乐就可以播放，从功能上来说这已经满足了我的需求，不过说实话，界面真的丑

![](/images/2021-11-21-synology-audio/11.jpg)

## 音乐信息管理

你可能会发现在网络上下载的音乐，好多元信息都是错误的，比如歌手、专辑、封面等等，通过在 `Audio Station` 的歌曲上右键，点击 `歌曲信息`，我们可以简单的编辑歌曲的信息，

![](/images/2021-11-21-synology-audio/12.jpg)
![](/images/2021-11-21-synology-audio/13.jpg)

如果需要编辑的歌曲很多，可以考虑使用 [Meta](https://www.macwk.com/soft/meta) 或 [Mp3tag](https://www.macwk.com/soft/mp3tag) 来批量编辑歌曲信息

![](/images/2021-11-21-synology-audio/14.jpg)


## 参考资料

- [https://segmentfault.com/a/1190000039068892](https://segmentfault.com/a/1190000039068892)