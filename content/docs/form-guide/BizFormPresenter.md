---
title: "BizFormPresenter"
date: 2021-11-15T10:59:00+08:00
author: 
---

## 顶层结构
![20211115110054_1bb5a402d5944b2d806d1df15abd8718.png](https://hugo-1256216240.cos.ap-chengdu.myqcloud.com/20211115110054_1bb5a402d5944b2d806d1df15abd8718.png)

## options
![20211115110139_7ff94f3d033892ec26b02baae8987a03.png](https://hugo-1256216240.cos.ap-chengdu.myqcloud.com/20211115110139_7ff94f3d033892ec26b02baae8987a03.png)

## api
![20211115110231_a4fd7c80384ee5534bb172cd0947c159.png](https://hugo-1256216240.cos.ap-chengdu.myqcloud.com/20211115110231_a4fd7c80384ee5534bb172cd0947c159.png)

## config
就是init接口的返回值
![20211115110316_f25898b7a4030002dfe74875f6c3ccde.png](https://hugo-1256216240.cos.ap-chengdu.myqcloud.com/20211115110316_f25898b7a4030002dfe74875f6c3ccde.png)

## 业务表单的Presenter
```ts
class CalendarEntryFormPresenter extends EasyBizFormPresenter{}
```
calendarEntryFormPresenter.formPresenter是BizFormPresenter类型的。

## 获取常用的数据

### 当前form的billType
有两种方式：
1. `config.data.billType`
1. `api.formController.initData.billType`

### billStatus
`api.formController.stateController.billStatus`