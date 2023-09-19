---
title: "EditParams"
date: 2022-10-25T15:08:47+08:00
author: 
---

```ts
class xxFormPresenter extends xx{
    protected getEditOptions(): EditOptions {
        return merge({}, super.getEditOptions(), {
            editParams: {
                [F_BudgetPlan_project]: () => getBudgetProjectEditParams(this.formValue),
                [F_BudgetPlan_model]: () => matchBudgetModel(this.form),
                profitMarginAmount: ({form, params, path}) => {
                    return {
                        numericProps: {
                            decimalPlaces: 精度,
                        }
                    }
                }
            },
        })
    }
}

```
## 参数
![](http://hugo-1256216240.cos.ap-chengdu.myqcloud.com/pasteimageintomarkdown/2022-11-24/831740835263800.png)

### form EntityForm
![](http://hugo-1256216240.cos.ap-chengdu.myqcloud.com/pasteimageintomarkdown/2022-11-24/832181983515400.png)

![](http://hugo-1256216240.cos.ap-chengdu.myqcloud.com/pasteimageintomarkdown/2022-11-24/839917885025000.png)

### params
好像没啥用
![](http://hugo-1256216240.cos.ap-chengdu.myqcloud.com/pasteimageintomarkdown/2022-11-24/832135456614300.png)

### path
略

## 常见问题

1. 子表Presenter设置了`suppressQuickCreate`不生效。要在主表中设置才行 
2. 主子表Presenter同时对一个字段进行设置，只有主表Presenter生效。