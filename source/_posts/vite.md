---
title: vite
date: 2023-05-05 11:25:12
tags:
    -技术记录
---


推荐回答：[尤大的回应](https://www.zhihu.com/question/477139054/answer/2156019180)


vite走的是no-bundle路线，他不像webpack走babel打包出很多bundle，然后直接从浏览器中引入这些bundle，vite则不需要走bundle，他直接使用浏览器支持的ESModule引入（script标签中type 为module (https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Modules)）

- 能解析依赖关系，对于monorepo有良好的支持
- 开发环境下使用ESM，代替打包，但有预构建功能，可以将 CommonJS / UMD 转换为 ESM 格式
- ts自动配置，但不执行检查


今日好文：[何为技术](https://mp.weixin.qq.com/s/DHeayzVwF_K9Oi9w_ae1lQ)

vite开发环境：走预构建，将一个包的内部模块全部转化为一个ESmodule，目的是为了一个module就只发一个http请求