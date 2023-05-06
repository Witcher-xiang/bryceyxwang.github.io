---
title: vite
date: 2023-05-05 11:25:12
tags:
---


推荐回答：[尤大的回应](https://www.zhihu.com/question/477139054/answer/2156019180)


vite走的是no-bundle路线，他不像webpack走babel打包出很多bundle，然后直接从浏览器中引入这些bundle，vite则不需要走bundle，他经过基础的编译直接使用浏览器自带的module引入（script标签中type 为module (https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Modules)）

今日好文：[何为技术](https://mp.weixin.qq.com/s/DHeayzVwF_K9Oi9w_ae1lQ)