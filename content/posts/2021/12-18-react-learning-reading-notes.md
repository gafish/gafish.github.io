---
title: 《React 学习手册》2017版读书笔记
description: 
keywords:
 - React 学习手册
toc: true
authors: []
tags: []
categories: 技术
series: []
date: 2021-12-18T22:52:51+08:00
lastmod: 2021-12-18T22:52:51+08:00
featuredVideo:
featuredImage:
url: /posts/2021/12/18/react-learning-reading-notes/
---

## Javascript 函数式编程

### 命令式与声明式

命令式编程的特点是，其代码重点关注的是达成目标的具体过程。

```js
var string = 'hello world';
var urlFriendly = '';

for (var i = 0; i < string.length; i++) {
  if (string[i] === '') {
    urlFriendly += '-';
  } else {
    urlFriendly += string[i]
  }
}

console.log(urlFriendly);
```

`命令式编程风格需要辅以大量注释说明帮助用户理解它的具体用途`

声明式编程有一个比较突出的特点，那就是对执行结果的描述远胜于执行过程。

```js
const string = 'hello world';
const urlFriendly = string.replace(/\s/g, '-');

console.log(urlFriendly);
```

`使用string.replace方法是一种说明可能会发生什么的方式：字符串中的空格将会被替换。如何处理空格的细节被抽象封装到了replace函数内部`

在一个声明式的程序中，语法本身描述了将会发生什么，相关的执行细节被隐藏了

本质上来说，使用声明式编程编写的应用程序更容易解释具体用途，当一个应用易于解释具体用途时，该应用也更易于进行功能扩展。

### 函数式编程基本概念

核心概念：不可变性、纯函数、数据转换、高阶函数、递归

#### 不可变性

不可变性就是指不可改变，在函数式编程中，数据是不可变的，它们永远无法修改

```js
let color_lawn = {
  title: 'lawn',
  color: 'green'
  rating: 0,
}

var rateColor = function(color, rating) {
  return Object.assign({}, color, {rating: rating});
}

console.log(rateColor(color_lawn, 5).rating);  // 5
console.log(color_lawn.rating);  // 0
```

- Array.concat 会将数组串联起来，并将它添加到原生数组的副本上
- Object.assign 会将对象的属性添加到原生对象的副本上
- 扩展运算符（...）有同样的效果

#### 纯函数

纯函数是指，对于相同的输入，必定会得到相同的输出，而且不会有任何副作用、不修改全局变量，纯函数至少需要接收一个参数并且总是返回一个值或者其它函数

编写纯函数三原则：

  - 函数应该至少接收一个参数
  - 函数应该总是返回一个值或者其它函数
  - 函数不应该修改或影响任何传入的参数


#### 数据转换

当需要从一个数组中移除某个元素时，我们倾向于使用 `Array.filter` 方法替代 `Array.pop` 或 `Array.splice` 方法，因为 `Array.filter` 方法是不可变的。

两个必须熟练掌握的函数：

  - `Array.map`
  - `Array.reduce`

它们是任何函数式程序员的主要武器，从其它数据源创建一个新的数据集的能力是程序员的必备技能。

`Array.reduce` 方法的几种用法示例(通过 copillot 生成)：

```js
// 使用 Array.reduce 求最大值
var numbers = [1, 2, 3, 4, 5];
var max = numbers.reduce(function(max, number) {
  return Math.max(max, number);
}, -Infinity);
```

```js
// 使用 Array.reduce 求和
var numbers = [1, 2, 3, 4, 5];
var sum = numbers.reduce(function(sum, number) {
  return sum + number;
}, 0);
```

```js
// 使用 Array.reduce 求组合
var numbers = [1, 2, 3, 4, 5];
var combinations = numbers.reduce(function(combinations, number) {
  return combinations.concat(
    combinations.map(function(combination) {
      return combination.concat(number);
    })
  );
}, [[]]);
```

```js
// 使用 Array.reduce 将数组转换为对象
var numbers = [{ name: 'a1', vlaue: 1 }, { name: 'a2', value: 2 }];
var object = numbers.reduce(function(object, number) {
  return Object.assign({}, object, { [number.name]: number.value });
}, {});
```

```js
// 使用 Array.reduce 将数组去重
var numbers = [1, 2, 3, 4, 5, 1, 2, 3, 4, 5];
var unique = numbers.reduce(function(unique, number) {
  if (unique.indexOf(number) === -1) {
    unique.push(number);
  }
  return unique;
}, []);
```

#### 高阶函数

  - 函数作为参数传递
  - 函数作为返回值返回

`Array.map`、`Array.filter`、`Array.reduce` 等方法都是高阶函数，它们接收一个函数作为参数

`Currying(柯里化)` 是一种将某个操作中已经完成的结果保留，直到其余部分后续也完成后可以一并提供的机制。

```js
const userLogs = userName => message => {
  console.log(`${userName}: ${message}`);
};
const log = userLogs('John');

log('Hello'); // John: Hello
log('World'); // John: World
```

#### 递归

递归是用户创建的函数调用自身的一种技术，一般来说，在解决实际问题涉及到循环时，递归函数可以提供一种替代性方案。

```js
const countdown = (n, fn) => {
  if (n <= 0) {
    fn();
  } else {
    countdown(n - 1, fn);
  }
}
```

#### 合成

链式调用是合成技术的一种

合成的目标是：通过整合若干简单函数构造一个更高阶的函数


#### 总结

三个简单的规则

- 保持数据的不可变性
- 确保尽量使用纯函数，只接收一个参数，返回数据或其它函数
- 尽量使用递归处理循环



## React

虚拟DOM是由React元素组成的，概念上和HTML类似，不过它们实际上是JavaScript对象，直接访问JavaScript对象比访问DOM API高效的多。

浏览器的DOM是由DOM元素构成的，同样React的DOM是由React元素构成的，一个Reaact元素是对实际DOM元素应该如何表示的具体描述。

一个React元素只是一个JavaScript语法，用来告知React如何构造一个DOM元素。

两种创建React元素的方式：

  - React.createElement(type, props, children)
  - React.createFactory(type) / React.DOM.type

React元素 `<h1 id="recipe-0" data-type="title">Baked Salmon</h1>` 实际创建的内容

```js
{
  $$typeof: Symbol(react.element),
  type: 'h1',
  key: null,
  ref: null,
  props: {
    id: 'recipe-0',
    'data-type': 'title',
    children: 'Baked Salmon'
  },
  _owner: null,
  _store: {}
}
```

三种创建React组件的方式

  - React.createClass（将废弃）
  - React.Component
  - 无状态函数式组件

### 无状态函数式组件

它们是简单的纯函数，所以我们应该在项目开发中尽可能地使用它们。

React开发团队承诺使用它们之后能够在某些方向提高性能，Facebook暗示将来无状态函数式组件将会比类组件更加高效。


## React与JSX

`React.createElement(IngredientList, { list: [...] })`

vs

`<IngredientList list={[...]}>`

### jsx使用注意事项

  - 支持组件嵌套
  - calssName替代class
  - JavaScript表达式用花括号包裹
  - 支持求值计算
  - JSX数组映射

### Babel

Babel的主要功能是转译，它的第一版程序叫6to5，是一款可以将 ES6 转换成 ES5 的工具。该项目于2015年2月正式更名为Babel

Babel presets 模块

    备注：以年命名的preset已经不再推荐使用，建议使用@babel/preset-env

  - babel-preset-es2015 将ES2015、ES6转换成ES5
  - babel-preset-es2016 将ES2016转换成ES5
  - babel-preset-es2017 将ES2017转换成ES5
  - babel-preset-env 包含前面三个preset，并且支持最新的ES语法
  - babel-preset-react 将React转换成ES5
  - babel-preset-stage-0 实验性提议
  - babel-preset-stage-1 建议
  - babel-preset-stage-2 草稿
  - babel-preset-stage-3 候选

### Webpack

一个可以兼容多种不同类型文件的模块绑定器，并且可以将它们转换成单个文件，两个主要优点是模块化和网络性能。

模块化：用户可以将源代码分解成易于使用的部分或模块，特别是对于团队开发来说非常有用。

网络性能：在浏览器中只需载入依赖即可，即bundle，每个脚本标签都会创建http请求，并且每个http请求都会有延迟。将所有依赖项打包成单个文件后，只需发送一次http请求，就能加载所有必须的资源，从而避免了额外的网络延迟。

webpack可以处理的任务

  - 代码转译
  - 代码拆分
  - 代码压缩
  - 特性标记
  - 热替换(HMR)

使用webpack模块打包工具的好处

  - 模块化
  - 合成
  - 效率
  - 一致性

## Props 和 State

ECMAScript提案中提供了 Class Fields & Static Properties 的支持，类的静态属性允许用户在类的内部声明中封装 propTypes 和 defaultProps。

大部分情况下，用户将会希望避免根据属性初始化state变量，因为在使用React组件时，用户希望限制包含state的组件的数量。

## 组件扩展

我们可以将任意JavaScript库与React集成，生命周期函数是其它JavaScript库进入，React库离开的地方，不过我们应该竭力避免添加管理UI的脚本库，这是React的工作。

高阶组件是一种极佳的功能复用方式，并且能够将组件State和生命周期管理的细节封装起来，它允许用户构建更多无状态函数式组件，以便可以一心一意的管理UI。

在React之外管理State意味着很多不同的事情，用户可以把React和Backbone模型搭配使用，或者其它任意MVC库的模型State，用户可以创建专属于自己的State管理系统，甚至可以使用全局变量，本地存储和Javascript纯文本管理State。在React之外管理State，简单的理解就是不在应用程序中使用React的State或者setState方法。


### Flux

Flux是Facebook开发的一种设计模式，旨在保持数据单向流动，在Flux诞生之前，Web开发架构由多种MVC设计模式的变体所主导，Flux是MVC的替代品，是一种完全不同的设计模式，并且与函数编程范式相辅相成。

Flux为我们提供一种Web应用架构，可以把它视为React的有益补充，具体来说，Flux提供了一种方法可以为React创建UI将要用的数据提供支持。

在Flux中应用程序的State数据是存放在React组件外部的Store进行管理的，Store保留或者修改数据，是唯一可以更新Flux视图的办法。

## Redux

Redux是类Flux的脚本库，但它不完全是Flux，它包含Action、Action生成器、Store，以及用于修改State的Action对象。

Redux通过移除Dixpatcher，对Flux的概念进行了一些简化，并使用单个不可变对象表示应用程序的State，Redux还引入了Reducer，它并不是Flux模式中的内容，Reducer是纯函数，它会根据当前的State和Action来返回一个新的State。

### State

在纯React或者Flux应用中，比较推荐的做法是将State尽量存放在少数几个对象中，在Redux中，这是一条规则。

在构建Redux应用时，用户首先需要考虑的事情就是State树，尝试在单个对象中定义State，使用一些占位符数据草拟一个State树的JSON示例是一个非常好的习惯。

### Action

Action是更新Redux应用程序State的唯一方式，Action为我们提供了应该变更哪些内容的指令。

使用一个Javascript常量来代替字符串，Javascript变量中的拼写错误将会导致浏览器抛出异常，将Action定义为常量也使得用户能够充分利用IDE工具的智能提示和代码自动补全功能。常量的使用并不是必需的，但是采用这种编码习惯也不失为一个好主意。

### Reducer

Reducer是一个纯函数，它接受当前的State和Action，并返回一个新的State。

### Store

Store是Redux应用程序中保存和管理State的地方，也是通过Store分发ction的形式，唯一的修改State数据的方式。Store会将应用程序的State作为单个对象进行保存。State的变更是通过Reducer来完成的。Store的创建是通过提供一个Reducer和可选的初始State来完成的。

### Action 生成器

Action对象是通过简单的Javascript语法表示的，Action生成器就是返回这类语法格式的函数。

### 中间件

Redux中间件扮演了Store分发管理的角色，在Redux中，中间件是在分发某个Action过程中一系列顺序执行的若干函数构成。

## React-Redux

属性在组件树中向上和向下传递的过程增加了程序的复杂性，类似Redux这样的库就是为了缓解这一问题而诞生的，为了替代通过双向函数绑定实现组件树上的数据传递，我们可以直接从子组件分发Action来达到更新应用程序的目的。

## 结语

React开发的关键是在正确的时间选择正确的工具。用户工具箱中已经拥有大量可以构建健壮应用程序的工具。现在只要按需取用即可。如果用户的应用程序没有涉及大量的数据，那么不必使用Redux。React和State是一个非常适合普通规模应用程序的解决方案。用户的应用程序也许并不需要用到服务器端渲染。不用急于集成它们，直到用户的应用程序人机交互频繁，并且包含大量移动流量时再添加这些特性也不晚。

