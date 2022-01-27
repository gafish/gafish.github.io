---
title: 使用 Tauri+React+Tailwind 打造一款简单的Mac工具
description: 
keywords:
 - Tauri
toc: true
authors: []
tags: []
categories: 技术
series: []
date: 2022-01-26T16:53:14+08:00
lastmod: 2022-01-26T16:53:14+08:00
featuredVideo:
featuredImage:
url: /posts/2022/01-26-tauri-app
---

Tauri 是一个可以用前端来写界面的跨平台 Rust GUI 框架，简单的理解就是对标 Electron 的一个类似产品，本文我们将以 Tauri+React+Tailwind 的组合来打造一款简单的Mac系统信息查看工具。

## 本文所使用的环境及版本

- MacOS Monterey - 12.1.0 X64
- Homebrew - 3.2.15
- Node.js - 16.13.0
- npm - 6.14.15
- yarn - 1.16.0
- rustc - 1.58.0
- cargo - 1.58.0
- @tauri-apps/cli - 1.0.0-beta.10
- @tauri-apps/api - 1.0.0-beta.8

## 安装依赖

本文假定你使用的设备是 MacOS 系统，并且已经安装了 Homebrew、Node.js、Xcode、Yarn，最好是打开了翻墙软件。

开始安装 Tauri 开发环境相关依赖：

```bash
# gcc
$ brew install gcc
# rustc & cargo
$ curl --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs | sh
```

重新启动终端

## 启动一个新的 Tauri 项目

在终端中进入你的项目根目录，如 `~/github`，执行以下命令生成一个新的 Tauri 项目：

```bash
$ yarn create mac-system-viewer-app
$ yarn create tauri-app
```

当看到 `Press any key to continue...` 的提示时，请按任意键继续。

根据提示输入以下内容

项目名称
```bash
? What is your app name? (tauri-app) mac-system-viewer-app
```

App窗口标题
```bash
? What should the window title be? (Tauri App) Mac系统信息查看器
```

选择UI框架，这里我选择 create-react-app 生成 react 项目
```bash
? What UI recipe would you like to add? (Use arrow keys)
  Vanilla.js
❯ create-react-app
  create-vite
  Vue CLI
  Angular CLI
  Svelte
  Dominator
```

添加 @tauri-apps/api 依赖包
```bash
? Add "@tauri-apps/api" npm package? (Y/n) Y
```

选择 react 模板，这里我选择 Typescript
```bash
? Which create-react-app template would you like to use? (Use arrow keys)
  create-react-app (JavaScript) 
❯ create-react-app (Typescript) 
```

当看到 `>> Running initial command(s)` 的提示时，项目自动开始初始化与安装依赖

### 手动初始化项目

如果自动初始化成功则跳过此步骤

**如果安装过程中一直提示 `Downloading Rust CLI...` ，则说明下载服务器无法连接，可能需要在命令行中翻墙连接(**为翻墙软件的端口号)**

```bash
$ export HTTP_PROXY=http://127.0.0.1:**; export HTTPS_PROXY=http://127.0.0.1:**; export ALL_PROXY=socks5://127.0.0.1:**
```

设置好连接后进入刚创建的项目目录，手动执行初始化命令
```bash
$ cd mac-system-viewer-app/
$ yarn tauri init --app-name mac-system-viewer-app --window-title Mac系统信息查看器 --dist-dir ../build --dev-path http://localhost:3000 --ci
```

当看到 `✨  Done in 11.39s.` 的提示时，说明项目初始化成功

## 启动开发环境

进入创建好的项目目录，启动 react 开发服务环境
```js
$ yarn start
```

新开一个命令窗口，启动 Tauri 开发环境
```js
$ yarn tauri dev
```

**如果 Tauri 开发环境启动失败，可能是因为服务器无法连接，可能需要如之前的操作打开命令行翻墙连接**

开发环境启动成功会打开一个APP界面，效果如下面两图所示：

![](/images/2022-01-26-tauri-app/1.jpg)

![](/images/2022-01-26-tauri-app/2.jpg)

## 使用 Tailwind CSS

安装
```bash
$ yarn add tailwindcss
```

生成并初始化 `tailwind.config.js` 配置文件
```bash
$ npx tailwindcss init
```

配置文件路径
```js
module.exports = {
  content: ["./src/**/*.{html,js,jsx,ts,tsx,css,less}"],
  theme: {
    extend: {},
  },
  plugins: [],
}
```

在项目的入口样式文件中添加 `tailwind` 指令
```js
@tailwind base;
@tailwind components;
@tailwind utilities;
```

尝试在 `App.tsx` 中写一段HTML测试代码
```html
<h1 className="text-3xl text-red-500 font-bold underline">
  Hello world!
</h1>
```

重新启动 react 开发环境，如果如下图所示，则说明 Tailwind CSS 正常

![](/images/2022-01-26-tauri-app/3.jpg)

## 使用 Tauri API

在项目初始化的时候，已经在模板文件里自带了 `@tauri-apps/api` 依赖包，所以我们不需要额外的安装

跟系统相关的API都在 OS 模块中，可以[点击这里](https://tauri.studio/docs/api/js/modules/os)查看api文档

我们来构建一个显示系统信息的页面

```tsx
import { useState, useEffect } from 'react'
import { os } from '@tauri-apps/api'

function App() {
  const [arch, setArch] = useState('')
  const [platform, setPlatform] = useState('')
  const [tempdir, setTempdir] = useState('')
  const [type, setType] = useState('')
  const [version, setVersion] = useState('')

  useEffect(() => {
    os.arch().then(setArch)
    os.platform().then(setPlatform)
    os.tempdir().then(setTempdir)
    os.type().then(setType)
    os.version().then(setVersion)
  }, [])
  
  return (
    <div className='p-10 text-sm text-green-500 leading-loose'>
      <ul>
        <li><span className='text-xs text-black pr-2'>CPU 架构:</span> {arch}</li>
        <li><span className='text-xs text-black pr-2'>平台名称:</span> {platform}</li>
        <li><span className='text-xs text-black pr-2'>临时文件目录:</span> {tempdir}</li>
        <li><span className='text-xs text-black pr-2'>系统类型:</span> {type}</li>
        <li><span className='text-xs text-black pr-2'>系统版本:</span> {version}</li>
      </ul>
    </div>
  )
}

export default App
```

APP会自动更新并显示如下界面

![](/images/2022-01-26-tauri-app/4.jpg)

## 构建安装包

工具开发完成后，我们需要构建一个安装包，Tauri在当前开发环境中，只会构建一个当前平台的安装包

先构建web网站
```bash
$ yarn build
```

构建当前平台的安装包
```bash
$ yarn tauri build
```

**如果 Tauri 构建失败，可能是因为服务器无法连接，可能需要如之前的操作打开命令行翻墙连接**

构建成功后会生成一个安装包 `src-tauri/target/release/bundle/dmg/mac-system-viewer-app_0.1.0_x64.dmg` ，效果如下图所示：

![](/images/2022-01-26-tauri-app/5.jpg)

至此，我们已经完成了一个简单的 Tauri 应用的开发与构建，文章对应的仓库地址为：[https://github.com/gafish/mac-system-viewer-app](https://github.com/gafish/mac-system-viewer-app)

后续关于如何构建跨平台的应用，以及如何更新当前应用，我们放到下一篇博客中进行讨论

## 注意事项

1、 默认情况下，构建的安装包只支持当前系统的版本，如需要支持更低版本，需要修改 `src-tauri/tauri.conf.json` 配置文件，将 `tauri - bundle - macOS - minimumSystemVersion` 的版本号改为低于当前系统版本的版本号