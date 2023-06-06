---
title: monorepo
date: 2023-06-05 17:29:17
tags:
    工程化
---


[monorepo](https://juejin.cn/post/7215886869199896637)
1、nx：可以看作一个脚手架，解决代码重用性（monorepo），通过命令行添加修改子仓库,提供了很多插件、置的构建和部署工具（更侧重于项目的管理）
例：
 执行命令 npx create-nx-workspace@latest 可以直接使用nx创建一个你需要的模版，如公司项目中即使用nx进行打包
 Nx 仅管理 npm 脚本的调度和缓存

 nx是什么？有什么作用
相比其他monorepo有什么优势，为什么选择了nx？
快速的任务调度、任务流水线、缓存，内嵌的依赖管理系统

项目中用到了他的那些功能
任务调度：run-many，执行所有命令项,nx 打包
```sh
nx build:dev admin --skip-nx-cache
```

任务流水线： 对于执行build命令的项目A，会将项目A中所使用的依赖项（只要带build的都会提前打包出来）
```javascript
  "build": {
      "dependsOn": ["^build"]
    }
```

2、lenra：一个比nx功能少的脚手架，可以和nx结合使用，他主要做三件事（更侧重于npm包的管理）
（1）它为单个包或多个包运行命令 ( lerna run) 一个依赖包更新，其他依赖此包的包/项目无需安装最新版本，因为 Lerna 自动 Link
（2）它管理依赖项 ( lerna bootstrap) 多个包都使用相同版本的依赖包时，Lerna 优先将依赖包安装在根目录
（3）它发布你的包，处理版本管理，并生成变更日志 ( lerna publish)  Lerna 通过 Git 检测代码变动，自动发版、更新版本号；两种模式管理多个依赖包的版本号

总结：一般lenra会结合yarn workspace一起使用，主要原因在于lenra更专注于项目内发包之间发布时的依赖关系（发布问题）,而yarn workspace则更加关注同一个代码仓库下npm包的关系（npm依赖问题）

我们平时装依赖都会yarn add -W xx ，其中-W的作用是将 xx 添加到工作区的 "package.json" 文件中。"-W" 参数告诉 Yarn 将 xx 添加为工作区的共享依赖项，这意味着每个项目都可以使用该依赖项，而不需要在每个项目中单独安装。



