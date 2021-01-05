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

1. 在跳转页面时，将需要的参数放入proxyHistory.push的第二个参数passParams中。
{{< highlight ts "linenos=table,hl_lines=19,linenostart=1" >}}
class ProjectListPagePresenter extends QueryListPagePresenter<
  IProjectListPagePresenterOption
>{
  protected commandActionResolver(commandActions: ToolbarAction[]): ToolbarAction[] {
    commandActions.unshift({
      id: 'project-view',
      group: ToolbarActionGroup.Group1,
      action: this.presenter.toolbarConnector.makeCreateButton({
        onClick: billTypeId => {
          const hash = appRouterHashManager.generateHash(EN_Project, PageModeEnum.Form, {
            mode: BizFormModeEnum.Create,
            billTypeId: billTypeId,
            extraParams: {
              isBase: this.isBase,
            },
          });
          proxyHistory.push(hash, {
            onSuccess: this.presenter.refresh,
            category: this.category.curParent,
          });
        },
      }),
    });
    return commandActions;
  }
}
{{< / highlight >}}

2. passParams中的数据会放到formPresenter的option中，取出使用即可。
{{< highlight ts "linenos=table,hl_lines=2 6 17,linenostart=1" >}}
class ProjectFormPresenter extends EasyBizFormPresenter<IProject> {
  private options: IEasyBizFormPresenterOptions;

  constructor(options: IEasyBizFormPresenterOptions, private isBase?: boolean) {
    super(EN_Project, options);
    this.options = options;
  }

  @autobind
  protected onFormCreated(form: EntityForm<IProject>, disposers: Lambda[]) {
    // ...
    const stageGroup = form.select(F_Project_stageGroup);
    if (stageGroup && stageGroup.required) {
      form.select(F_Project_enableStage).value = true;
    }
    if (this.opotions.passParams.category) {
      form.select(F_Project_category).value = this.options.passParams.category;
    }
    if (this.bizFormPresenter.api.mode === 'Copy') {
      const clearFields = [
        'startDate',
        'closedDate',
        'changedReason',
        'lastChangedTime',
    // ...
  }
}
{{< / highlight >}}
