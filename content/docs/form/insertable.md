---
title: "Insertable"
date: 2022-06-08T15:54:27+08:00
author: 
---

```ts
class x extends EasyBizFormPresenter{
  protected getOtherFormOptions(): IBizFormOptions {
    return {
      gridOptions: {
        ['subscriptions']: {
          indicateColumnOption: {
            // insertable: ,
            isRowInsertable: (rowIndex) => {
              if (!this.form || !this.form.select('createdUser') || !this.form.select('createdUser').value) return true;
              return this.form.select('createdUser').value.id === oc(this.userInfo).id('')
            }
          },
        },
      },
    }
  }
}
 
```