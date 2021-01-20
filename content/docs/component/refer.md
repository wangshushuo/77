---
title: "Refer"
date: 2021-01-13T11:39:09+08:00
author: 王书硕
---

## form中设置

### getEditOptions之editParams
editParams是定义每个field（也可以设置子表的field）的编辑态的参数。
```
{
  [key: fieldName]: 参数对象
}
```
参数对象需要根据field具体是什么来行确定，比如field可能是数字、字符串、参照等，对应的渲染组件就是NumberField，ReferField，TextField等，参数对象就是对应的渲染组件的参数。

## 参数
```
// 高级参照支持多选
enableMultiInsert: true,
criteriaStr: criteriaStr,
referConfigResolver: referConfig => {
  return Object.assign({}, referConfig, {
    displayField: 'code',
  });
},
advanceReferProps: {
  categoryCriteriaStr: ,
},
queryFields: [],
onMultiInsert: (
  data: Array<ICustomizedCarryoverProgrammeSubjectSetting>,
  editRowField: MSTFormField,
) => {
  if (Array.isArray(data) && data.length > 0) {
    const origin = editRowField.value || [];
    for (let i = 0, len = data.length; i < len; i += 1) {
      data[i] = Object.assign(data[i], {
        summary: origin.summary,
      });
    }
  }
},
```

### enableMultiInsert
高级参照，多选插入子表。

在ParamsController中处理它。为true时，会在advanceReferProps中加isMulti和onChange。从而实现了多选自动插入子表。
```ts
if (referParams.enableMultiInsert && this.presenter.api.isDetailInsertable(detailName)) {
  referParams['advanceReferProps'] = Object.assign({}, referParams['advanceReferProps'], {
    isMulti: true,
    onChange: value => {
      this.detailController.onAdvanceReferMultipleSelect(
        detailName,
        colFieldName,
        value,
        rowIndex,
        referParams,
      );
    },
  });
```