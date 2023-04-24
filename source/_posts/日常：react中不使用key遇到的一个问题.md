---
title: 日常：react中不使用key遇到的一个问题
date: 2023-04-17 23:42:55
tags:
- 每日思考&问题记录
---

今天遇到个key值的问题，我们一般给组件加key是这样
```
Xxx.map((key)=>(<div key={key}></div>))
```
最外层组件加key，用于react的diff算法优化性能。但是现在这个VideoBox是我自己封装的自定义组件没有map，所以一般代码提示不会提示你加key
![组件截图](/picture/20230418005129.png)

当我没有给组件添加key时，再切换这个videoBox时出现了一定的延时，之前的组件没有被销毁，而是在video加载后才出现的，
联系之前key的作用我们可以得出一个结论，因为这里的key使得组件被即使销毁替换（即使video没有渲染好），但你不加key要等到video渲染好才上屏（可以类比看出video是有状态的，但开始渲染并不会主动更新），因此我们可以得出一个结论，即使我们没有使用map，但组件通过setState或者props进行重复切换渲染时，尤其是像video标签这种，资源加载完成后才渲染的组件，最好加上key，使得他资源更新时组件即可销毁

在浏览器中，``<video>`` 元素和 ``<audio>`` 元素都是动态加载的，这意味着它们是在资源加载完成后才更新的。
因此在有视频切换时，我们尽量去使用组件去渲染，而不是去修改video的s中的地址
```javascript
const images = useMemo(
    () => [
      ...SIDE_LIST.flatMap(({ selected, unSelect }) => [selected, unSelect]),
      ...VIRTUAL_PERSONALIZE_MAP.hair.matchList.flatMap(({ displayMan, displayWoman }) => [displayMan, displayWoman]),
      ...VIRTUAL_PERSONALIZE_MAP.face.matchList.flatMap(({ displayMan, displayWoman }) => [displayMan, displayWoman]),
      ...VIRTUAL_PERSONALIZE_MAP.cloth.matchList.flatMap(({ displayMan, displayWoman }) => [displayMan, displayWoman]),
    ],
    []
  );
  useImagePreload({
    images,
    trigger: !!isInViewport, // 判断当前元素是否在视窗内
  });

```

---
