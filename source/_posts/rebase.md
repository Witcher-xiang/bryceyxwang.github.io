---
layout: 日常：git rebase
title: git rebase
date: 2023-05-22 20:51:42
tags: 日常
---

之前一直使用pull来合代码，是merge操作，突发奇想想用rebase合代码结果出了些问题

建议看这个[视频](https://www.bilibili.com/video/BV1VG411F7rB/?spm_id_from=333.880.my_history.page.click&vd_source=395f80277a4d78ccebf2a48d28e67ac4)






![merge](/picture/20230523-merge.jpg)
merge: 会按照时间顺序去合并，但会新创建一个merge的commit


![rebase](/picture/20230523.jpg)
rebase: 重新创建所有的commit，且不会有rebase节点，你的commit会被放到最前面，主线上的commit都会被放在后后面,这也是所谓的变基