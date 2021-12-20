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

