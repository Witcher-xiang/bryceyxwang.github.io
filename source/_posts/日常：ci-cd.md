---
title: 日常：ci/cd
date: 2023-04-21 23:13:42
tags:
- 每日思考&问题记录
---

### CI/CD


CI：持续部署

CD：持续集成


CI: 通过质测平台进行监控，当检测到配置的目标仓库有变动时（Merge后），就会执行你配置好的shell脚本，比如yarn run docker，帮你打包构建镜像然后推到目标镜像位置，到此步 我们还差让镜像自动重启

对于我们使用的monenrepo的处理是写判断语句，挨个执行，如下

```
yarn install
if [ $targetBranch = $devMain ]
then
    echo "是devMain环境"
    yarn run docker:admin dev
  yarn run docker:xxx dev
  yarn run docker:xxx dev
  yarn run docker:xxx dev
  yarn run docker:xxx dev
elif [ $targetBranch = $qaMain ]
```
但这样的坏处如果只有一台机子就会很很慢

CD：
也在质测平台中，叫持续部署
首先选择项目，输入应用名，代码仓库和分支名称，以及部署的镜像名称，他会监控是否有镜像推送有的话就自动重启

#### 总结

CI+CD = 代码merge后-》打镜像 -》 镜像推送
