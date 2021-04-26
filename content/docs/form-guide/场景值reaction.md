---
title: "场景值reaction"
date: 2021-04-26T17:49:17+08:00
author: 
---

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