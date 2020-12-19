---
title: 模型、entity与元数据
weight: 50
---
# 模型、entity与元数据

## 模型
我们系统的后端是领域模型驱动的。
![20201220003015_f822a09b4e13a03ab672a165a5f510b8.png](https://hugo-1256216240.cos.ap-chengdu.myqcloud.com/20201220003015_f822a09b4e13a03ab672a165a5f510b8.png)
上图是预算编制方案的模型，其中包含了很多实体(entity)(蓝色的)。

## entity
一个entity就是一个对象，可以通过模型看到各个属性的名字和类型，以及entity之间的关系。

我们前端工作就是为entity制作表单和列表，来创建entity的实例或展示entity的信息。

## 元数据
前度的元数据主要是对entity的描述。entity的名字、entity的属性名等等。