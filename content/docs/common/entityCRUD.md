---
title: 脱离form对entity进行crud
author: 王书硕
---

有时我们需要新增、修改、删除一条entity的数据。但是这个entity又没有开发对应的form，无法通过表单来完成。这时就要用到EntityCRUDHelper了
```ts
import { EntityCRUDHelper } from '@root/solutions/entity-crud';

EntityCRUDHelper.getInstance().update(EN_BudgetAccountDocImport, data)
```

EntityCRUDHelper提供了create/update/delete等几个方法，可以直接基于entity进行crud操作。

方法 | 参数 | 描述
:---:|:---|:---
create | entityName, data | 创建一条记录
update | entityName, data | 修改一条记录

## 注意事项

entity不能是子表。子表必须通过主表创建。