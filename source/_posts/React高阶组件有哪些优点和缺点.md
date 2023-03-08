---
title: React高阶组件有哪些优点和缺点
date: 2023-03-08 22:58:49
tags: React
categories: 面试题
cover: react-logo.png
top_img: react-logo.png
---

## HOC

**优点**

- 通过传递 props 去影响内层组件的状态，不直接改变内层组件的状态，降低了耦合度

**缺点**

- 组件多层嵌套,增加复杂度与理解成本
- ref 隔断， 可以通过 React.forwardRef 来解决
- 高阶组件多层嵌套，相同命名的 props 会覆盖老属性
- 不清楚 props 来源于哪个高阶组件

## render props

**优点**

- props 命名可修改，不存在相互覆盖
- - 清楚 props 来源
- 不会出现组件多层嵌套
  **缺点**
- 函数回调形式的嵌套
- 写法繁琐，没有 hoc 装饰器写法简单
- 无法在 return 以外的地方访问数据

## hook

**优点**

- 解决了 hoc，render props 的嵌套问题
- 可以在 return 之外使用数据
- 可以重命名，不存在覆盖，且清楚数据来源
  **缺点**
- 在闭包场景可能会引用到旧的 state、props 值
