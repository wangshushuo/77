---
title: "BizForm的原理"
weight: 300
---
## FormController
LifecycleEvent.onInitialStart事件触发onInitStart方法，该方法中先是得到了initData，然后对Form进行初始化操作。初始化以后有创建了Form。

也就是initForm和createForm。

initForm中进行了initEntityOptions，然后用这个option创建EntityCRUD。
createForm实用initData对entityCRUD进行了初始化。然后触发了LifecycleEvent.onFormCreated事件。

initEntityOptions也是值得一提的，它组织了entity初始化需要的参数。



## BizForm的原理

总体来说分为三个阶段：
- 创建model（mobx-state-tree）
- 创建form
- 展示form

