---
title: "删除行"
date: 2021-02-22T18:20:56+08:00
author: 
---

```js
const refDocMappingsField = this.form.select(F_BudgetAccount_refDocMappings);

if (refDocMappingsField.value !== undefined) {
  let len = refDocMappingsField.value.length;
  while (len>0){
    this.formController.deleteRowByRealIndex(
      F_BudgetAccount_refDocMappings,
      len - 1,
    );
    len --;
  }
}
```