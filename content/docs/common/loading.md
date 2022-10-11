---
title: "Loading"
date: 2022-10-10T16:47:30+08:00
author: 
---

## 移动端
```ts
import { closeLoadingMask, showLoadingMask } from '@common/loadingMask';

showLoadingMask('加载编制详情...');
try {
  const params = router.getParams('/budgetPlanChange/detail');
  const data = await client.get(`${urls.budgetPlan.compare}/${params.id}/${params.bassBillId}`);
  const diffCells = data && data.data.data;
  if (diffCells) {
    this.setDiffCells(diffCells);
  }
} catch (e) {
  showErrorMessage(e.message || '编制详情加载失败');
} finally {
  closeLoadingMask();
}
```

## web端
```ts
import { hideLoading, showLoading } from '@root/common/loading';

showLoading({
  message: '正在取消中...',
  closeable: true,
});
try {
  await this.requestController.revertBudgetPlanDetail();
  const res = await this.initialController.queryData();
  this.renderSpreadFromJson(res);
} catch (err) {
  showError(oc(err).message('取消本次预算表修改失败'));
  throw err;
} finally {
  hideLoading();
}
```