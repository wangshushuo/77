---
title: "子表RowActions问题排查"
author: 王书硕
---

问题：日程变更时子表不能增删行。

一个解决方案是在go上把response加rowActions
```
rowActions["participants"] = []string{
    context.BizFormAction_Add,
    context.BizFormAction_Copy,
    context.BizFormAction_Delete,
}
```
但是这样处理以后只有新增按钮，没有删除、复制按钮。debug发现子表的getRowActions没有调用。

rowActions的渲染时在DetailGrid.tsx组件中处理的。

initRowActions方法中
```ts
const actions: any = actionOptions.rowActions[fieldName] || []; // 子表的getRowActions
actionCallback = (rowIndex: number, data) => actions(rowIndex, data, defaulCallback);
this.rowActions = (rowIndex: number, data) => {
    if (this.formField.disabled) {
        return [];
    }
    if(this.fieldStatusController.getEffectedReadonly(this.formField)) {
        return [];
    }
    const actions = actionCallback(rowIndex, data);
}

```
这里没有渲染删除、复制按钮是因为`this.formField.disabled`为`true`，也就是`this.form.select('participants').disabled`为`true`。至于哪里设置的disabled就不好排查了。
所以临时解决方案就是在`onRowInitialized`中加一个把`disabled`改为`false`的reaction
```ts
const fixChildTableDisabled = reaction(
    () => this.form.select(F_CalendarEntry_participants).disabled,
    () => {
        this.form.select(F_CalendarEntry_participants).disabled = false
    },
    {
        fireImmediately: true
    }
)
```

## 审批流中设置了允许增删行，但是表单不显示按钮
如果有审批模板的话，审批流中设置的新增删除就不生效了