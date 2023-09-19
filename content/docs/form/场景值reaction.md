---
title: "场景值reaction"
date: 2021-04-26T17:49:17+08:00
author: 
---

如果表单的A字段设置了reaction监听。当修改A的value的时候，对应的reaction都会触发。如果希望不触发reaction，就要用到下面的场景值reaction

```ts
// 根据场景值忽略执行的reaction
const reactionOmit = this.bizFormPresenter.api.reactionOmitCreator(
  BizFormScenarios.SourcePicking,
);

// 使用reactionOmit监听
disposers.push(
  reactionOmit(
    () => form.select('F_TimesheetLine_orgRoleType').value,
    value => {
     
    }
  )
)

// 使用reactionOmit对应的场景值赋值，就不会触发reaction
this.bizFormPresenter.api.runInScenarios(BizFormScenarios.SourcePicking, () => {
  rowField.select(F_TimesheetLine_orgRoleType).value = {
    id: EN_Department,
    title: '部门',
    name: EN_Department,
  };
})
```