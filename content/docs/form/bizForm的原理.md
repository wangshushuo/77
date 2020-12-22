---
title: "BizForm的原理"
weight: 300
---
## BizForm的原理

## FormController
LifecycleEvent.onInitialStart事件触发onInitStart方法，该方法中先是得到了initData，然后对Form进行初始化操作。初始化以后有创建了Form。

也就是initForm和createForm。

initForm中进行了initEntityOptions，然后用这个option创建EntityCRUD。
createForm实用initData对entityCRUD进行了初始化。然后触发了LifecycleEvent.onFormCreated事件。

initEntityOptions也是值得一提的，它组织了entity初始化需要的参数。


1. 创建FormEntityCRUD

```ts
this.entityCRUD = new FormEntityCRUD(entityOptions);
```
使用entityOptions创建FormEntityCRUD。entityOptions的类型是IEntityOptions，具体参数如下

```ts
export interface IEntityOptions extends IBaseEntityOptions {
    httpOptions?: {
        headers?: {
            [key: string]: any,
        }
    };
}
export interface IEntityOptions extends IEntityLifecycle {
  // entity 名称
  entityName: string;
  // query 模式，是新增 还是 查询
  queryMode?: 'blank' | 'query';
  // 查询数据时，需要额外查询的字段
  queryFields?: Array<string>;
  // 如果是查询或者删除，则需要给 id
  dataId?: string;
  // formOptions
  formOptions?: EntityFormOptions;
  // 是否为空行
  isEmptyRow?(logicPath: string, path: string, rowField: MSTFormField): boolean;

  // 在 update 时，阻止数据处理，返回原始数据
  suppressDataFilterWhenUpdate?: boolean;

  // 阻止空行的清理
  suppressCleanEmptyRow?: boolean;

  // 阻止unchanged行的清理
  suppressCleanUnchangeRow?(logicPath: string, path: string, rowField: MSTFormField): boolean;

  // 在保存成功后阻止刷新
  suppressQueryAfterSave?: boolean;
  // 需要返回 responseData
  needResponseData?: boolean;

  // 在clean时，需要忽略的字段
  ignoreCleanPath?: Array<string>;
  // 在clean时，需要保留的字段
  containCleanPath?: Array<string>;
  // 排序方法
  sortResolver?(path: string, data: Array<any>): Array<any>;
  // 数据处理器
  processors?: Array<IDataProcessor>;

  // 是否清理ID
  isIgnoreCleanId?: boolean;
}

```

总体来说分为三个阶段：
- 创建model（mobx-state-tree）
- 创建form
- 展示form

