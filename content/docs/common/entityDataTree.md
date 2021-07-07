---
title: "EntityDataTree"
date: 2021-06-29T13:41:36+08:00
author: 
---

## 寻找自定义该组件中的gql的方法
预算项目列表中的左树用了CustomerCategory组件，它又用了CategoryTree组件，其中又用了EntityDataTree组件，其中又用到了CommonProvider类，最终的gql就是在CommonProvider中生成并使用的。
```
return client
  .query<{ data: T[] }>({
    query: `query{
            data: ${queryBuilder.toString()}
        }`
  })
```