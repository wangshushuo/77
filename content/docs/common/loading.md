---
title: "Loading"
date: 2022-10-10T16:47:30+08:00
author: 
---

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