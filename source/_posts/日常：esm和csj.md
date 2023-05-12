---
title: esModuleInerop
date: 2023-05-11 14:33:18
tags:
---

### ts Config中的esModuleInterop选项
https://zhuanlan.zhihu.com/p/148081795

在我们使用esm写代码时，tsc会给我们编译出最终是commonjs
```javascript
TS、babel 对 export 变量的转译规则为：（代码经过简化）
// before
 export const name = "esm";
 export default {
   name: "esm default",
 };

 // after
 exports.__esModule = true;
 exports.name = "esm";
 exports["default"] = {
   name: "esm default"
 }
```

可以看到：

- 对于 export default 的变量，TS 会将其放在 module.exports 的 default 属性上
- 对于 export 的变量，TS 会将其放在 module.exports 对应变量名的属性上
- 额外给 module.exports 增加一个 __esModule: true 的属性，用来告诉编译器，这本来是一个 esm 模块

当开启这个选项后，编译结果就变了
```javascript
mport React from 'react';
 console.log(React);
 // after 代码经过简化
 var react = __importDefault(require('react'));
 console.log(react['default']);


 // before
 import {Component} from 'react';
 console.log(Component);
 // after 代码经过简化
 var react = require('react');
 console.log(react.Component);
 
 
 // before
 import * as React from 'react';
 console.log(React);
 // after 代码经过简化
 var react = _importStar(require('react'));
 console.log(react);

```
将exports["default"]替换成了函数，来帮助我们规避这个问题


总结：在esm中使用commonJS模块时，需要添加这个配置，来改变转换规则，使得能在ESM中使用CMJ的包而不报错，TS、babel、webpack都有他们自己的处理机制

### 打一个包出来同时存在ESM和CMJ

![自动曝光](/picture/20230512.jpg)

- main为CMJ的入口
- module为ESM的入口
- type为.t.ds的入口

优先级：一般情况下module 的优先级更高，具体可以看[这个文章](https://juejin.cn/post/6844903862977953806#heading-5)

另一个打包啊工具[tsup](https://tsup.egoist.dev/)

- 无需配置直接打包
- 有坑，如果你有declare 为any的包，打.d.ts的包就会报错，不允许为存在any引入的包