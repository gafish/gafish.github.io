---
title: "Craft.js 从入门到进阶"
date: 2021-10-29T21:22:59+08:00
description: "Craft.js 是一个用于构建可扩展的拖放页面编辑器的 React 库"
author: "gafish"
categories:
  - "编程开发"
keywords:
 - Craft
 - Craft.js
 - Craft 入门
 - Craft 中文
 - 可视化编辑器
url: ""
---

在做可视化页面编辑器技术选型调研的时候，我发现了2个很好的开源库： `grapes.js` 和 `craft.js`

`grapes.js` 是一个 HTML Web 构建器框架，它提供了一个开箱即用的解决方案，自带非常完整的组件，基本用法如下：

```html
<div id="gjs">
  <h1>Hello World Component!</h1>
</div>
```
```js
const editor = grapesjs.init({
  container: '#gjs',
  fromElement: true,
  height: '300px',
  width: 'auto',
  storageManager: false,
  panels: { defaults: [] },
});
```

`craft.js` 是一个用于构建可扩展的拖放页面编辑器的 React 框架，不提供组件本身，可以根据业务需要完全自己开发组件，基本用法如下：

```js
import React from "react";
import {Editor, Frame, Canvas, Element} from "@craftjs/core";
import TextComponent from './TextComponent'
import Container from './Container'

const App = () => {
  return (
    <div>
      <header>Some fancy header or whatever</header>
      <Editor resolver={TextComponent, Container}>
        <Frame>
          <Element is="div" canvas>
            <TextComponent text="I'm already rendered here" />
          </Element>
        </Frame>
      </Editor>
    </div>
  )
}
```

我们团队是以 React 技术栈为主，所以非常明显，我选择了 `craft.js` 来开发我们的可视化编辑器，当然还有2个重要的原因：

1. 它支持完全的组件定制，对组件UI没有限制；
2. 它的API设计足够简单，逻辑清晰，功能强大；

在 `craft.js` 的官网 [https://craft.js.org/](https://craft.js.org/) 有着完善的文档和教程来讲解如何使用它来搭建你自己的编辑器，但因为项目还在发展期，版本更新比较快，文档更新却比较落后，官网上的很多示例都已经无法正常运行，所以我才决定自己写一篇文章来讲解如何入门及深入的使用。

本文所使用的环境及版本

- MacOS Big Sur 11.6
- node: 16.13.0
- yarn: 1.22.4
- react: 17.0.2
- craft.js: v0.1.0-beta.20

本文会以一个Demo项目的形式讲解如何使用craft.js，项目开源仓库地址： [https://github.com/gafish/craft.js_demo](https://github.com/gafish/craft.js_demo)

## 项目初始化及安装

```bash
# 初始化React项目
npx create-react-app craft.js_demo

# 安装craft.js
yarn add craft.js

# 运行项目
cd craft.js_demo
yarn start
```

## 基本概念

`craft.js` 的API非常简单，只有3个组件、2个Hook

```js
import { Editor, Frame, Element, useEditor, useNode } from '@craftjs/core'
```

#### 组件

- `<Editor />`        创建存储编辑器状态的上下文
- `<Frame />`         定义了页面编辑器中的可编辑区域
- `<Element />`       定义了可拖拽组件的放置区域给定用户元素的节点

#### HOOK

- `useEditor()`        提供与整个编辑器相关联的方法和状态信息
- `useNode()`          提供与管理当前组件的相应方法和状态信息相关的方法和状态信息

## 基本使用

我们先添加第1个Demo，如示例仓库中的 `src/Demo1`，文件结构如下：

```
src/
  Demo1/
    index.js
    Main.js
    Main.css
```

这里之所以要新建一个 `<Main />` 组件，是因为 `<Editor />` 组件需要注入状态给到它后面的组件中，下面的组件才可以通过  `useEditor()` 拿到编辑器的状态。

本文中我们主要讲解js逻辑，所以本文会省略css代码，此时代码如下：

`src/Demo1/index.js`

```js
import React from 'react'
import { Editor } from '@craftjs/core'

import Main from './Main'

function App() {
  return (
    <Editor>
      <Main />
    </Editor>
  )
}

export default App

```

`src/Demo1/Main.js`

```js
import React from 'react'
import { Frame, Element } from '@craftjs/core'

import './Main.css'

function App() {
  return (
    <div className="app">
      <div className="head">
        <div className="item">折线图</div>
        <div className="item">饼图</div>
      </div>
      <div className="container">

        <Frame>
            <Element is="div" className="main" canvas>
              <div className="text">
                显示第一段文本
              </div>
              <div className="image">
                <img src="https://picsum.photos/200/200" alt=""/>
              </div>
              <div className="text">
                显示第二段文本
              </div>
              <div className="image">
                <img src="https://picsum.photos/200/200" alt=""/>
              </div>
            </Element>
        </Frame>
        
        <div className="sider">
          <div className="title">配置栏</div>
        </div>
      </div>
    </div>
  )
}

export default App
```

以上代码我们定义了编辑器的基本结构，当拖拽 `<Element />` 的子节点时，会出现一个绿色的占位条，放开组件就会移动到当前占位位置。

预览效果

![](/images/2021-10-29-craftjs-introduction/1.jpg)

## 添加组件
...

## 组件设置
...

## 编辑器结构序列化
...

## 操作历史记录
...

## 图层管理
...

## 项目实战
...



## 资源来源

[grape.js](https://grapesjs.com/)
[craft.js](https://craft.js.org/)