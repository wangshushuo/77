---
title: "创建form时带默认数据"
date: 2021-01-05T11:25:11+08:00
author: 王书硕
---

## 场景
在新建”项目“时，选择了项目分类后点新建，所选择的分类会出现在表单的”项目分类“中。

1. 选择分类
2. 点新建
![20210105112657_4fa7e3652b235b5982986c22831f3c9b.png](https://hugo-1256216240.cos.ap-chengdu.myqcloud.com/20210105112657_4fa7e3652b235b5982986c22831f3c9b.png)
3. 自动填写了“项目分类”
![20210105112712_7cfbb3e12c9b9268cc18cc75e8bae239.png](https://hugo-1256216240.cos.ap-chengdu.myqcloud.com/20210105112712_7cfbb3e12c9b9268cc18cc75e8bae239.png)

## 怎么实现

### 1.通过路由传数据
在跳转页面时，将需要的参数放入proxyHistory.push的第二个参数passParams中。
```ts
function onClick(billTypeId) {
  const hash = appRouterHashManager.generateHash(EN_Project, PageModeEnum.Form, {
    mode: BizFormModeEnum.Create,
    billTypeId: billTypeId,
  });
  proxyHistory.push(hash, {
    onSuccess: this.presenter.refresh,
    category: this.category.curParent,
  });
}
```
proxyHistory.push方法的第二个参数会被放到FormPresenter的options.passParams中。

### 2.在formPresenter中取数据
passParams中的数据会放到formPresenter的option中，取出使用即可。
```ts
class ProjectFormPresenter extends EasyBizFormPresenter<IProject> {
  private options: IEasyBizFormPresenterOptions;

  constructor(options: IEasyBizFormPresenterOptions, private isBase?: boolean) {
    super(EN_Project, options);
    this.options = options;
  }

  @autobind
  protected onFormCreated(form: EntityForm<IProject>, disposers: Lambda[]) {
    const category = this.opotions.passParams.category;
    if (category) {
      form.select(F_Project_category).value = category;
    }
  }

}
```
❗这里需要注意❗由于表单的入口可能有多个，在使用passParams时，要注意判空。
