---
title: "GridRowAction的popover"
date: 2021-04-01T18:45:12+08:00
author: 王书硕
---

多列表方案中

```tsx
getRowActions(rowIndex: number, data: any): IGridAction[] {
  const actions = this.presenter.listSolutionConnector.rowActionController.makeDefaultRowActions(
    data,
  );

  const disabledTimeAction = {
    icon: 'icontuichu',
    title: '停用日期',
    key: 'disabledDate',
    onClick: () => {},
    popoverRender: () => {
      return {
        content: (
          <div />
        ),
      };
    },
  }
}
```