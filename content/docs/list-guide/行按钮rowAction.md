---
title: "行按钮rowAction"
date: 2021-04-14T18:43:40+08:00
author: 王书硕
---

适用于：多列表

效果图：
![20210414185013_5073428437796c793bbcf61706247d3b.png](https://hugo-1256216240.cos.ap-chengdu.myqcloud.com/20210414185013_5073428437796c793bbcf61706247d3b.png)

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