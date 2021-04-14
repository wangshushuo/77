---
title: "行按钮rowAction"
date: 2021-04-14T18:43:40+08:00
author: 
---

```tsx
export class BudgetModelList extends QueryListPagePresenter {

  // 覆盖父类的方法
  getRowActions(rowIndex: number, data: any): IGridAction[] {

    // 获取公共默认的actions
    const actions = this.presenter.listSolutionConnector.rowActionController.makeDefaultRowActions(
      data,
    );

    if (data && data.id) {
      // 加新的按钮
      actions.push({
        icon: ICON_VIEW,
        title: '预览',
        key: 'preview',
        onClick: (rowIndex, data) => this.preview(data),
      });
    }

    // 还可以对actions数组进行过滤
    return actions;
  }

}
```