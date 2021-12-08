---
title: "群晖折腾手记二：搭建个人数字图书馆"
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
date: 2021-09-26T21:32:16+08:00
lastmod: 2021-09-26T21:32:16+08:00
featuredVideo:
featuredImage:
draft: false
url: /posts/2021/11/06/synology-calibre-library
---

一直以来我都有收藏电子书的习惯，特别是实体书的PDF版本是我的最爱，收藏的书多了，如何管理是个问题，好在有 `Calibre` 这个好用的电子书管理软件，帮我把书籍归类，编辑，省去了不好事情，现在有了群晖 ，我就开始琢磨如何通过群晖来把本地的电子书做成在线电子图书馆，好在开源社区已经有了好的解决方案 [calibre-web](https://github.com/janeczku/calibre-web)，一个可以将本机的  `Calibre`  数据库转换成在线电子书网站的应用，另外它有一个由 LinuxServer 团队维护的  `Docker`  镜像，这正是本文要使用的工具。

在群晖720中，支持  `Docker`  套件，所以我们可以直接搜索安装 `linuxserver/calibre-web` 镜像，接下就随我一起来一步一步搭建个人数字图书馆，在实际的搭建过程中我遇到了一些难题，网上找的资料也不全，不过最终在不断摸索下成功了，所以本文就把一个可行的过程写出来。

## 写在开头

在线电子书平台所需的数据来自在我们本机的 `Calibre` ，所以你需要先了解 `Calibre` 如何管理电子书，以及如何导出数据，关于这点在本文不做详细说明，可以参见我的另外一篇文章[《 Calibre 入门指南》](/2021/10/17/calibre-introduction/)。

*好了本文正式开始*

## 选择镜像源

由于国内网络众所周知的原因，下载 `Docker` 镜像会非常慢，所以我们要做的第一件事就是先选择一个国内的 `Docker` 镜像源，有非常多的选择，这里我选择的是阿里云的 `Docker` 镜像。

用淘宝账号进入阿里云 [容器镜像加速器](https://cr.console.aliyun.com/cn-hangzhou/instances/mirrors)，复制类似这样的地址 `https://*******.mirror.aliyuncs.com` 备用

![](/images/2021-11-09-synology-calibre-library/1.jpg)

## 下载安装

1. 在套件中心搜索安装 `Docker` ，安装完成后打开

![](/images/2021-11-09-synology-calibre-library/2.jpg)

2. 在 `Docker` 中，进入注册表，点设置，选中  `Docker  Hub`，点编辑，勾选 `启用注册表镜像`，在 `注册表镜像URL` 中填入刚才获取到的阿里云镜像地址

![](/images/2021-11-09-synology-calibre-library/3.jpg)

3. 搜索 `calibre-web`，选中 `linuxserver/calibre-web` 点下载

![](/images/2021-11-09-synology-calibre-library/4.jpg)

4. 请求连接成功后，会弹出选择标签弹窗，我们保持默认就好，注意这一步视每个人网络情况而定，有可能需要重试多次才能成功

![](/images/2021-11-09-synology-calibre-library/5.jpg)

5. 开始下载，在映像中可以看到当前下载进度，下载中启动按钮是禁用状态

![](/images/2021-11-09-synology-calibre-library/6.jpg)

6. 下载完成，启动按钮变为可点击状态

![](/images/2021-11-09-synology-calibre-library/7.jpg)

## 启动服务

1. 点击启动按钮，会打开常规设置界面

![](/images/2021-11-09-synology-calibre-library/8.jpg)

2. 点击 `高级设置`，选择存储空间，添加文件夹，可以选择已有的文件夹或创建一个新的文件夹，这里我选择的是 `docker/calibre` 文件夹，设定一个装载路径 `/calibre-web`，**注意这里的斜杠是必须的**

![](/images/2021-11-09-synology-calibre-library/9.jpg)

3. 选择端口设置，本地端口设置可以自定义，容器端口必须为 `8083`

![](/images/2021-11-09-synology-calibre-library/10.jpg)

4. 应用设置，容器启动完成不会有提示，大概等2分钟后，你直接在浏览器中访问 `群晖IP地址:8083`，如 `192.168.1.123:8083`， 就可以看到已经启动好的电子书网站，使用默认的初始化账号 `admin/admin123` 登录

![](/images/2021-11-09-synology-calibre-library/11.jpg)

5. 如果此时我们直接开始接下来的第6步操作，会遇到 `DB Location is not Valid, Please Enter Correct Path` 报错

![](/images/2021-11-09-synology-calibre-library/12.jpg)

我研究发现产生这个错误有以下2个原因

- 选择的存储空间 `docker/calibre` 文件夹中没有预先准备数据
- `Docker`  中的  `/calibre-web` 目录没有读写权限

我们需要先在本机上找到 `Calibre` 的书库目录，默认是在用户目录的  `Calibre  书库` 文件夹中，把整个目录里的文件都复制到 `docker/calibre` 文件夹，最重要的是不要忘了 `metadata.db` 这个数据文件。

![](/images/2021-11-09-synology-calibre-library/13.jpg)

然后打开群晖上的 `Docker`，找到刚才创建的容器 `linuxserver-calibre-web1`，点击详情，打开 `终端机` tab，点击新增，会出现一个`bash` 的选项，点击 `bash`，在右侧的命令行中输入 `chmod 777 /calibre-web`，就是给 ` /calibre-web` 目录添加可读写权限

![](/images/2021-11-09-synology-calibre-library/14.jpg)

6. 以上准备工作完成，再次打开电子书网站，开始设置 Database Configuration ，输入第2步里设定的装载路径 `/calibre-web`，点保存，出现绿色提示框说明设置成功

![](/images/2021-11-09-synology-calibre-library/15.jpg)

7. 网站默认是英文界面，如果看不习惯，可以选择切换到中文界面，点击右上角的 `admin` 用户名，在 `language` 里选择中文，点击最底下的 `save` 就会切换到中文界面

![](/images/2021-11-09-synology-calibre-library/16.jpg)

8. 打开网站首页，就可以看到之前我们复制到群晖的电子书数据了

![](/images/2021-11-09-synology-calibre-library/17.jpg)

## 书籍管理

如果每次在本机的电子书数据更新了，要同步到群晖上，都要复制本机的文件及数据替换群晖上的数据，这让书籍管理起来就非常不方便，这里推荐一种在局域网环境中在本机  `Calibre`  直接管理群晖上数据的办法。

1. 进入 `控制面板`-`文件服务`，启用SMB服务

![](/images/2021-11-09-synology-calibre-library/18.jpg)

2. 在 `Calibre` 中创建新书库

![](/images/2021-11-09-synology-calibre-library/19.jpg)

3. 新书库文件夹从局域网络中选择之前我们在群晖上放置电子书数据的共享文件夹，选中 `在新位置使用现有的书库`。

![](/images/2021-11-09-synology-calibre-library/20.jpg)

此时我们看到的就是群晖上的电子书数据了，你直接编辑书籍信息后，刷新网站就能看到最新的改动

## 资料参考

- [https://post.smzdm.com/p/a6l8ovxe/](https://post.smzdm.com/p/a6l8ovxe/)
- [https://fugary.com/?p=203](https://fugary.com/?p=203)
- [https://csdaomin.com/2021/05/28/self-hosted-your-own-calibre-web-service-on-ubuntu-20/](https://csdaomin.com/2021/05/28/self-hosted-your-own-calibre-web-service-on-ubuntu-20/)
- [https://mariushosting.com/how-to-install-calibre-web-on-your-synology-nas/](https://mariushosting.com/how-to-install-calibre-web-on-your-synology-nas/)
- [http://ifoxfactory.com/2018/05/15/Synology-NAS-with-Calibre-web-one/](http://ifoxfactory.com/2018/05/15/Synology-NAS-with-Calibre-web-one/)
- [https://sspai.com/post/64202](https://sspai.com/post/64202)