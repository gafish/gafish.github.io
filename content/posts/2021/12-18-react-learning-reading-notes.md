---
title: 《React 学习手册》2017版学习笔记
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
draft: true
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