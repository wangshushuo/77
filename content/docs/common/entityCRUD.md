---
title: 脱离form对entity进行crud
author: 王书硕
---
# 脱离form对entity进行crud

```ts
import { EntityCRUDHelper } from '@root/solutions/entity-crud';

EntityCRUDHelper.getInstance().update(EN_BudgetAccountDocImport, data)
```

## 注意事项

entity不能是子表。子表必须通过主表创建。

EntityCRUDHelper的其他api
方法 | 参数 | 描述
:---:|:---|:---
create | entityName, data | 创建一条记录
update | entityName, data | 修改一条记录