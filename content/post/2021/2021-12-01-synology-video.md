---
title: "群晖折腾手记五：家庭影视娱乐上手指南"
date: 2021-12-01T21:45:25+08:00
description: ""
author: "gafish"
categories:
  - "记录折腾"
keywords:
 - synology
 - synology 720+
 - 群晖 720+
url: "/2021/11/22/synology-download"
---


## 安装与设置

在套件中心搜索 `video station` 并安装，完成后会在一个新窗口打开界面

![](/images/2021-12-01-synology-video/1.jpg)

默认会打开设置界面，提示你启用视频信息插件，它的作用是自动为你的电影下载元数据和封面数据

![](/images/2021-12-01-synology-video/2.jpg)

点击 `The Movie Database`，再点击编辑，会看到一个 API 密钥的输入框，点击下方的 `申请API密钥` 链接，会打开如何申请 API 密钥的帮助页面，按照教程一步步操作

![](/images/2021-12-01-synology-video/4.jpg)

需要注意的是，在填写 API 申请理由时，如果遇到一直报错 `Application summary please elaborate on how you plan to use our API`，直接把申请理由改成 `Application summary please elaborate on how you plan to use our API` 就可以了

![](/images/2021-12-01-synology-video/5.png)

## 视频库

在设置界面中，点击 `视频库`，会有3个默认的视频库，点击右侧的 `+` 号，选择视频资源所在的文件夹，点击 `确定` 就会开始创建索引，大概1分钟后左侧点击视频库菜单就可以看到文件夹中的电影资源了

![](/images/2021-12-01-synology-video/3.jpg)

如果默认的视频库不能满足你的需求，你也可以创建自定义的视频库，同样可以在设置界面为自定义的视频库添加视频资源文件夹

![](/images/2021-12-01-synology-video/6.jpg)

## 权限管理

我有一个需求是给女儿的账号创建了一个学习视频库，但默认的视频库里添加的电影她也能看到，为了不耽误她的学习，我需要把其它的视频库资源隐藏起来，这里就可以用上自定义视频库的指定权限功能

首先创建一个单独的账号，在自定义视频库的指定权限功能中，为不同账号指定访问权限

![](/images/2021-12-01-synology-video/7.jpg)

## 视频播放

直接在电脑上访问 `video station` 就可以播放电影，在其它平台需要安装相应的 `DS Video` APP，用设置好的账号登录即可访问

### 手机

在应用商店下载 `DS Video` APP

### 平板

在应用商店下载 `DS Video` APP

### 电视

...