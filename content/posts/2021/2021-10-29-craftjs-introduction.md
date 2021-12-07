---
title: "Craft.js 入门与实践"

toc: true
date:  2021-10-29T21:22:59+08:00
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

### 组件

- `<Editor />`        创建存储编辑器状态的上下文
- `<Frame />`         定义了页面编辑器中的可编辑区域
- `<Element />`       定义了可拖拽组件的放置区域给定用户元素的节点

### HOOK

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
        <div className="item">文本</div>
        <div className="item">图片</div>
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

以上代码我们定义了编辑器的基本结构，当拖拽 `<Element />` 的子节点时，会出现一个绿色的**放置指示器**，放开组件就会移动到当前放置位置。

预览效果

![](/images/2021-10-29-craftjs-introduction/1.jpg)

## 添加组件

上述示例中，编辑器中的组件是固定不变的，接下来我们通过 `useEditor()` 提供的 `create` 方法以拖拽的方式来为编辑器添加组件。

修改 `src/Demo1/Main.js`
```diff
import React from 'react'
-import { Frame, Element } from '@craftjs/core'
+import { Frame, Element, useEditor } from '@craftjs/core'

import './Main.css'

function App() {
  const { connectors } = useEditor()
  const { create } = connectors

  return (
    <div className="app">
      <div className="head">
-        <div className="item">文本</div>
-        <div className="item">图片</div>
        <div
          className="item"
          ref={ref => create(ref, <div className="text">显示一段文本</div>)}
        >文本</div>
        <div
          className="item"
          ref={ref => create(ref, 
            <div className="image">
              <img src="https://picsum.photos/200/200" alt=""/>
            </div>
          )}
        >图片</div>
      </div>
      <div className="container">

        <Frame>
            <Element is="div" className="main" canvas>
-              <div className="text">
-                显示第一段文本
-              </div>
-              <div className="image">
-                <img src="https://picsum.photos/200/200" alt=""/>
-              </div>
-              <div className="text">
-                显示第二段文本
-              </div>
-              <div className="image">
-                <img src="https://picsum.photos/200/200" alt=""/>
-              </div>
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

此时我们就可以通过拖拽的方式不断的从顶部拖动新组件到编辑器中，同时组件之间也可以调整位置。

预览效果

![](/images/2021-10-29-craftjs-introduction/2.jpg)

## 组件抽象

在目前的示例代码中，我们将组件 `<div className="text">显示一段文本</div>` 在代码中写死作为 `create` 的第2个参数，接下来我们来讲解如何将组件抽象成独立的组件，该章节中我们仅以文本组件为讲解示例，图片组件方法类似所以过程省略。

新建文本组件 `src/Demo1/Text.js`
```js
function Text(props) {
  const { text = '默认文本' } = props
  return (
    <div className="text">
      {text}
    </div>
  )
}

export default Text
```

在 `src/Demo1/Main.js` 中引入新建的组件替换之前的组件部分，此时如果预览页面，你会发现从顶部拖拽可以添加新组件，但添加的组件之间位置无法调整了，WHY?

这是因为在抽象成自定义组件之前，`create` 的参数是一个原生的 `div` 组件，它和 `<Editor />` 的默认行为是连接且可拖拽，但是自定义组件默认和 `<Editor />` 没有连接且不可拖拽，所以我们需要在自定义组件中使用 `connect` 方法连接到 `<Editor />`，并通过 `drag` 方法为自定义组件添加拖拽行为。

这里要注意的是 `connect` 方法的执行位置，决定了**放置指示器**的位置， `drag` 方法的执行位置，决定了自定义组件可拖拽区域的位置。

修改文本组件 `src/Demo1/Text.js`
```diff
+import { useNode } from '@craftjs/core'

function Text(props) {
  const { text = '默认文本' } = props
  const { connectors } = useNode()
  const { connect, drag } = connectors

  return (
    <div
      className="text"
      ref={ref => {
        connect(ref)
        drag(ref)
      }}
    >
      {text}
    </div>
  )
}

export default Text
```

修改 `src/Demo1/Main.js`
```diff
import React from 'react'
import { Frame, Element, useEditor } from '@craftjs/core'

+import Text from './Text'
+import Image from './Image'

import './Main.css'

function App() {
  const { connectors } = useEditor()
  const { create } = connectors

  return (
    <div className="app">
      <div className="head">
        <div
          className="item"
-          ref={ref => create(ref, <div className="text">显示一段文本</div>)}
          ref={ref => create(ref, <Text />)}
        >文本</div>
        <div
          className="item"
-          ref={ref => create(ref, 
-            <div className="image">
-              <img src="https://picsum.photos/200/200" alt=""/>
-            </div>
-          )}
          ref={ref => create(ref, <Image />)}
        >图片</div>
      </div>
      <div className="container">

        <Frame>
            <Element is="div" className="main" canvas>
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

预览效果

![](/images/2021-10-29-craftjs-introduction/3.jpg)

## 组件设置

在可视化编辑器中，`组件`和`组件设置`通常是相关联的，我们在设置中做的改动都需要即时的在组件中得到显示反馈，所以这里就存在一个共享上下文的问题。

`craft.js` 可以给自定义组件添加静态属性 `craft` ，它的值会与`组件设置`共享

我们先新建一个文本设置组件 `src/Demo1/TextSetting.js`
```js
function TextSetting() {
  return (
    <div>
      文本内容：
      <input />
    </div>
  )
}

export default TextSetting
```

在文本组件中，通过在静态属性 `craft` 的 `related` 字段中添加对 `TextSetting` 的引用，这样就可以将`组件`和`组件设置`进行关联，同时在静态属性 `craft` 中设置 `props` ，将组件的默认配置放在这里，这样就可以在`组件`和`组件设置`之间进行 `props` 共享。

修改 `src/Demo1/Text.js`
```diff
import { useNode } from '@craftjs/core'
+import TextSetting from './TextSetting'

function Text(props) {
-  const { text = '默认文本' } = props
-  const { connectors } = useNode()
  const { connectors, node } = useNode(node => ({ node }))
  const { text } = node.data.props
  const { connect, drag } = connectors

  return (
    <div
      className="text"
      ref={ref => {
        connect(ref)
        drag(ref)
      }}
    >
      {text}
    </div>
  )
}

+Text.craft = {
  props: {
    text: '默认文本',
  },
  related: {
    setting: TextSetting,
  },
+}

export default Text
```

修改 `src/Demo1/TextSetting.js`，在文本修改后通过 `setProp` 方法更新 `text` 属性
```diff
+import { useNode } from '@craftjs/core'

function TextSetting() {
  const { node, actions } = useNode(node => ({ node }))
  const { text } = node.data.props
  const { setProp } = actions

  return (
    <div>
      文本内容：
-      <input />
      <input value={text} onChange={e => setProp(props => props.text = e.target.value)} />
    </div>
  )
}

export default TextSetting
```

当我们选中编辑器中的文本组件时，`useEditor` 中的编辑器状态中就可以获取到选中的组件ID，进而获取到选中的节点，这样我们就可以在设置面板中把 `TextSetting` 渲染出来。


修改 `src/Demo1/Main.js`
```diff
import React from 'react'
import { Frame, Element, useEditor } from '@craftjs/core'

import Text from './Text'
import Image from './Image'

import './Main.css'

function App() {
-  const { connectors } = useEditor()
  const { connectors, editorState } = useEditor(editorState => ({ editorState }))
  const { nodes, events } = editorState
  const { selected } = events
  const selectedNode = nodes[selected]
  const { create } = connectors

  return (
    <div className="app">
      <div className="head">
        <div
          className="item"
          ref={ref => create(ref, <Text />)}
        >文本</div>
        <div
          className="item"
          ref={ref => create(ref, <Image />)}
        >图片</div>
      </div>
      <div className="container">

        <Frame>
            <Element is="div" className="main" canvas>
            </Element>
        </Frame>
        
        <div className="sider">
          <div className="title">配置栏</div>
          {
            selectedNode &&
            selectedNode.related &&
            selectedNode.related.setting &&
            React.createElement(selectedNode.related.setting)
          }
        </div>
      </div>
    </div>
  )
}

export default App
```

通过以上修改，当我们选中文本或图片组件时，就可以在设置面板中可以设置文本和图片的属性。

预览效果

![](/images/2021-10-29-craftjs-introduction/4.jpg)

## 编辑器结构序列化

到目前为止，我们实现了可视化编辑器组件的添加、移动、设置，基本上实现了一个较完整的编辑器，但是，我们还需要一个方法来将编辑器的结构序列化成 Schema，这样我们就可以将编辑器的结构保存下来，以便下次打开时直接加载。

`useEditor()` 提供了一个 `serialize` 方法，可以将编辑器的结构序列化为 JSON 字符串，另外还提供了一个 `deserialize` 方法反序列化 JSON 字符串，可以将编辑器的 Schema 反序列化为结构。

本文示例中会将序列化 JSON 字符串保存在 `localStorage` 中，下次打开时点加载再从 `localStorage` 中获取数据。

修改 `src/Demo1/Main.js`
```diff
-import React from 'react'
+import React, { useCallback } from 'react'
import { Frame, Element, useEditor } from '@craftjs/core'

import Text from './Text'
import Image from './Image'

import './Main.css'

function App() {
-  const { connectors, editorState } = useEditor(editorState => ({ editorState }))
+  const { connectors, actions, query, editorState } = useEditor(editorState => ({ editorState }))
  const { nodes, events } = editorState
  const { selected } = events
  const selectedNode = nodes[selected]
  const { create } = connectors
+  const { serialize } = query
+  const { deserialize } = actions

+  const loadJSON = useCallback(() => {
+    const json = localStorage.getItem('craftjs-demo1')
+    deserialize(json);
+  }, [])
+  const saveJSON = useCallback(() => {
+    localStorage.setItem('craftjs-demo1', serialize())
+  }, [])

  return (
    <div className="app">
      <div className="head">
        <div
          className="item"
          ref={ref => create(ref, <Text />)}
        >文本</div>
        <div
          className="item"
          ref={ref => create(ref, <Image />)}
        >图片</div>
      </div>
+      <div className="btns">
+        <button onClick={loadJSON}>加载</button>
+        <button onClick={saveJSON}>保存</button>
+      </div>
      <div className="container">

        <Frame>
            <Element is="div" className="main" canvas>
            </Element>
        </Frame>
        
        <div className="sider">
          <div className="title">配置栏</div>
          {
            selectedNode &&
            selectedNode.related &&
            selectedNode.related.setting &&
            React.createElement(selectedNode.related.setting)
          }
        </div>
      </div>
    </div>
  )
}

export default App
```

如果此时我们先保存一下，刷新页面再加载，控制台会报错，why?

这是因为 `craft.js` 在还原页面结构的时候，它没有找到 `Text` 和 `Image` 这2个组件名称所对应实际组件的映射，因此会报错。

我们在显示已保存结构的时候需要在 `<Editor>` 中对组件进行映射，这样才能正常显示。

修改 `src/Demo1/index.js`
```diff
import React from 'react'
import { Editor } from '@craftjs/core'

+import Main from './Main'
+import Text from './Text'
+import Image from './Image'

import Main from './Main'

function App() {
  return (
-    <Editor>
+    <Editor resolver={{ Text, Image }}>
      <Main />
    </Editor>
  )
}

export default App

```

预览效果

![](/images/2021-10-29-craftjs-introduction/5.jpg)

好了，`craft.js` 入门篇先更新到这里，后续如果有新的想法了再继续。

## 资源来源

[craft.js](https://craft.js.org/)
[grape.js](https://grapesjs.com/)