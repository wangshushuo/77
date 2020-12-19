---
title: 修改Menu中的Button
---
# 向Menu中添加Button

此攻略会向你介绍如何往查看态的menu中加一个按钮

![20201219173459_0df051375728f03fe55bfe251d82cfef.png](https://hugo-1256216240.cos.ap-chengdu.myqcloud.com/20201219173459_0df051375728f03fe55bfe251d82cfef.png)

## 已有按钮添加到menu中

```ts
class xxFormPresenter extends EasyBizFormPresenter {
  protected getMenuOptions(): MenuOptions {
    const menus = super.getMenuOptions().menus;
    // 删改menus数组
    return menus;
  }
}
```
在这里修改menus数组就可以了。

可以直接往里面添加按钮。也可能要根据权限、是不是变更单等条件过滤掉一些按钮。