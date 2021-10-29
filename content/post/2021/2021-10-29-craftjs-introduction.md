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

```js
<div id="gjs">
  <h1>Hello World Component!</h1>
</div>

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

```jsx
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
- react: 17.0.2
- craft.js: v0.1.0-beta.20

本文会以一个Demo项目的形式讲解如何使用craft.js，项目开源仓库地址： [https://github.com/gafish/craft.js_demo](https://github.com/gafish/craft.js_demo)

## 安装及项目初始化
...

## 基本使用
...

## 拖拽组件
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