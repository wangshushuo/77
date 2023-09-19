---
title: 新建一个MenuButton
---
# 向Menu中添加Button

此攻略会向你介绍如何往查看态表单的menu中加一个按钮

![20201219173459_0df051375728f03fe55bfe251d82cfef.png](https://hugo-1256216240.cos.ap-chengdu.myqcloud.com/20201219173459_0df051375728f03fe55bfe251d82cfef.png)

## 新建一个menu按钮

按下面的步骤就可以创建一个按钮，并把它加到menu中
1. 按钮的名字
1. 按钮的Creator函数
1. 声明按钮
1. 声明分组
1. 添加到menu中

### 给搞一个名字
在 `apps/link/src/solutions/biz-form/page/menu-buttons/declare.ts` 文件中在BizFormMenuButtons对象声明按钮的 id 。

### 搞Creator函数创建按钮

```tsx
export const ProjectBudgetCreator = () => {
  return {
    id: BizFormMenuButtons.ProjectBudget,
    render: () => {
      return (
        <React.Fragment>
          <ProjectBudgetButton key={BizFormMenuButtons.ProjectBudget} />
        </React.Fragment>
      );
    },
  };
};
```

其中的React组件需要自己实现，主要是一个Button组件。要注意模块启用、权限。

### 声明按钮
有了id和creator函数，就可以声明按钮了。
在 `apps/link/src/solutions/biz-form/page/menu-buttons/index.tsx` 文件中声明了所有menu按钮的Creator函数。你新创建的按钮也需要在这里声明。

```ts
export const buildInMenus = {
  [BizFormMenuButtons.SourcePicking]: SourcePickCreator,
  [BizFormMenuButtons.ImportConsumeItem]: ImportConsumeItemCreator,
}
```

### 声明类型
相同类型的按钮会放到同一分组。
在 `apps/link/src/solutions/biz-form/page/declare.ts` 文件的 BizformMenuButtonType 对象中为按钮一个类型。

### 把按钮放到menu中

```ts
class xxFormPresenter extends EasyBizFormPresenter {
  protected getMenuOptions(): MenuOptions {
    const menus = super.getMenuOptions().menus;
    menus.push(buildInMenus.ProjectPlan());
    return menus;
  }
}
```
