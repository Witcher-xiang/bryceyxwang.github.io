---
title: 文章推荐：The “const” Deception
date: 2023-05-08 15:10:59
tags:
  - 文章推荐
---

### [The “const” Deception](https://www.joshwcomeau.com/javascript/the-const-deception/)

我们都知道const对于引用类型中的属性改变是无法限制的，文章介绍了如果我想在使用const时，想限制这一点可以使用Object.freeze()方法达到“防弹”效果。在Ts中你也可以直接使用as const断言来达到类似效果，除此之外使用大白话讲解了在js中assignment和mutation的区别加深你对js的理解

- 使用Object.freeze()去除const 可能会被修改属性的情况
- assignment一般指的是let或者const声明，或者是let改变时的情况
- mutation 则是const 修改了引用类型的属性
- 在js中基本类型的改变不是修改，而是重新引用。比如let a = 1 改成2 是重新创建了2而不是修改，因此基本类型不能被修改，不能出现 1 = 2的情况

PS：他这个博客挺好玩的还会突然跳小人