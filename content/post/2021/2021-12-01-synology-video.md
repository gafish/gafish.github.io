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
url: "/2021/12/01/synology-video"
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

在 Synology [下载中心](https://www.synology.cn/zh-cn/support/download/DS720+?version=7.0#androids) 下载 `AndroidTV-DSvideo` [apk 安装包](https://archive.synology.cn/download/Mobile/Android-DSvideo)。

将安装包复制到U盘上，插入电视机的USB口，一般的电视在设置中找到U盘，点击安装包安装即可，有些电视系统会屏蔽U盘中的安装文件，这时候可能就需要针对这类系统在网上找找资料。以我家的TCL电视为例，在系统应用 `电视卫士` 中找到 应用管理-极速安装 就可以看到没有屏蔽安装包的U盘入口，点击进去就可以安装

![](/images/2021-12-01-synology-video/8.jpg)


群晖TV DS Video使用了Android TV的特性，导致部分电视和电视盒设备在安装DS Video后没有显示启动图标，我们可以通过安装 [DSVideo-Go](http://www.tengmuz.com/index.php/2020/01/27/dsphoto-go%E7%BE%A4%E6%99%96tv-dsphoto%E5%90%AF%E5%8A%A8%E5%99%A8%EF%BC%8C%E8%A7%A3%E5%86%B3dsphoto%E5%AE%89%E8%A3%85%E5%90%8E%E6%97%A0%E5%90%AF%E5%8A%A8%E5%9B%BE%E6%A0%87%E9%97%AE%E9%A2%98-solut/) 来修复这个问题。

## 常见问题及解决办法

### 為什麼我無法在 Video Station 播放 DTS 或 EAC3 音訊檔的影片？

以下摘自官方的说明

```md
因專利授權的因素，Video Station 目前不支援以下的音訊播放格式：

- 所有 DTS 音訊格式 (包含但不限於 DTS 及 DTS-HD)
- 部分 Dolby Digital 音訊格式 (包含但不限於 Dolby Digital Plus (EAC3) 及 Dolby TrueHD)
```

解决办法

在第三方套件中搜索安装 `FFmpeg` (关于第三方套件的安装方法可以参考 [这里](/2021/12/04/synology-spk))

![](/images/2021-12-01-synology-video/9.jpg)

进入 `控制面板`-`终端机和SNMP`-`终端机` 启用SSH功能

![](/images/2021-12-01-synology-video/10.jpg)

在电脑上通过终端命令行执行 `ssh 管理员用户名@群晖的IP地址` 连接群晖，并输入 `sudo -i` 输入群晖管理员密码切换至root用户模式

![](/images/2021-12-01-synology-video/11.jpg)

依次执行以下内容脚本

```shell
#备份 VideoStation's ffmpeg
mv -n /var/packages/VideoStation/target/bin/ffmpeg /var/packages/VideoStation/target/bin/ffmpeg.orig

#下载ffmpeg脚本
wget -O - https://gist.githubusercontent.com/BenjaminPoncet/bbef9edc1d0800528813e75c1669e57e/raw/ffmpeg-wrapper > /var/packages/VideoStation/target/bin/ffmpeg

#设置脚本相应权限
chown root:VideoStation /var/packages/VideoStation/target/bin/ffmpeg
chmod 750 /var/packages/VideoStation/target/bin/ffmpeg
chmod u+s /var/packages/VideoStation/target/bin/ffmpeg

# 备份VideoStation's libsynovte.so
cp -n /var/packages/VideoStation/target/lib/libsynovte.so /var/packages/VideoStation/target/lib/libsynovte.so.orig
chown VideoStation:VideoStation /var/packages/VideoStation/target/lib/libsynovte.so.orig

# 为libsynovte.so 添加 DTS, EAC3 and TrueHD支持
sed -i -e 's/eac3/3cae/' -e 's/dts/std/' -e 's/truehd/dheurt/' /var/packages/VideoStation/target/lib/libsynovte.so

#备份CodecPack的ffmpeg41
cp /var/packages/CodecPack/target/bin/ffmpeg41 /var/packages/CodecPack/target/bin/ffmpeg41.bak

#链接ffmpeg解码模块
cp /var/packages/VideoStation/target/bin/ffmpeg /var/packages/CodecPack/target/bin/ffmpeg41
```

在套件中心先停用 `Video Station` 再重新打开，让ffmpeg与Video Station的关联生效

![](/images/2021-12-01-synology-video/12.jpg)

### 资料参考

- [https://todsay.com/share/25.html](https://todsay.com/share/25.html)
- [https://zhuanlan.zhihu.com/p/393311059](https://zhuanlan.zhihu.com/p/393311059)
- [https://www.znds.com/jc/article/2950-1.html](https://www.znds.com/jc/article/2950-1.html)
- [https://kb.synology.com/zh-hk/DSM/tutorial/Why_can_t_I_play_videos_with_DTS_or_EAC3_audio_format_on_Video_Station](https://kb.synology.com/zh-hk/DSM/tutorial/Why_can_t_I_play_videos_with_DTS_or_EAC3_audio_format_on_Video_Station)

...