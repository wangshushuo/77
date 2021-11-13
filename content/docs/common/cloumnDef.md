---
title: "CloumnDef"
date: 2021-11-13T15:29:37+08:00
author: 
---

## 典型用例

```tsx
{
  field: 'reimburseVoucherId',
  headerName: '报销凭证',
  editable: !disabledStatus,
  type: FieldTypeEnum.JsonObject,
  valueFormatter: params => {
    const { reimburseVoucherId } = params.data;
    return oc(reimburseVoucherId).name('') || '';
  },
  cellEditorParams: params => {
    const criteriaStr = this.getReimburseVoucherCriteriaStr;
    return {
      queryFields: [
        F_ReimburseVoucher_id,
        F_ReimburseVoucher_code,
        F_ReimburseVoucher_name,
        F_ReimburseVoucher_deductionTaxRate,
      ],
      criteriaStr: criteriaStr,
    };
  },
}
```

```
cellEditorParams: params => {
  const criteriaStr = this.getCostCriteriaStr;
  return {
    queryFields: [F_Cost_id, F_Cost_code, F_Cost_name, F_Cost_isLeaf],
    criteriaStr: criteriaStr,
    referConfigResolver: (referConfig: IReferConfig) => {
      return Object.assign({}, referConfig, {
        advanceEnabled: true,
        displayMode: 'grid',
        advanceOptions: {
          gridColumnsName: 'refer-list',
        },
        gridOptions: {
          // 如果展示模式是 Grid，则必须设置 Grid列设置
          gridColumnsName: 'refer-list',
        },
      });
    },
  };
}
```