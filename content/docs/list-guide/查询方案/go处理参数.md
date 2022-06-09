---
title: "Go处理参数"
date: 2022-05-18T23:49:05+08:00
author: 
---

trek/services/query-list/middlewares/entities/workforceResource/resource-load-query.go

中间件会处理前端传过来的查询条件，形成一个可以直接用的规则语句，它又会进入data-provider中。

![CriteriaStr](http://hugo-1256216240.cos.ap-chengdu.myqcloud.com/pasteimageintomarkdown/2022-05-18/48572449417000.png)
option.CriteriaStr就是最终的规则语句，可以直接传给后端或者查gql用。

![Criteria Values](http://hugo-1256216240.cos.ap-chengdu.myqcloud.com/pasteimageintomarkdown/2022-05-18/48624093350100.png)
还有各个查询条件的原始数据结构。
