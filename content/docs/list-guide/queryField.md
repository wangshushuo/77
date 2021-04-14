---
title: "QueryField"
date: 2021-04-14T18:57:28+08:00
author: 王书硕
---

列表数据会查询哪些字段一般是在预置数据里设置的。也可以通过代码控制。

{{< highlight tsx "linenos=table,hl_lines=7-9,linenostart=1" >}}
export class ProjectConfirmationListListPresenter extends QueryListPagePresenter {

   getQueryListOption(): IQueryListSolutionPresenterOptions {
    return {
      ...super.getQueryListOption(),
      resourceId: ResourceConstants.Res_ProjectConfirmation,
      getDynamicQueryFields: () => {
        return ['task.project.id'];
      }
    };
  }

}
{{< / highlight >}}
