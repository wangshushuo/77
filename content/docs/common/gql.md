---
title: GQL
author: 王书硕
weight: 1
---
## 普通的gql
最简单的，直接查一个对象（表）的全部数据
```
{
  BudgetAccount{
    id
    name
    accountType {
      id
      name
    }
  }
}
```

加一点查询条件
```
{
  BudgetAccount(criteriaStr:"name in ('1','2','3')"){
    id
    name
    accountType {
      id
      name
    }
  }
}
```
这个会查到name为1、2、3的多条数据

## 高级的gql
上面只能查到一个表的数据及其关联的外键，子表的数据。下面来搞一个子查询。
> 因为有的时候，后端的模型中，没有包含我们需要的子表，只能我们自己构建
```
{
  BudgetAccount(criteriaStr:""){
    a: exprField(expr:"()")
    b: exprField(expr:"()")
  }
}
```
其中`a:`是个模型上的一个字段起别名，`exprField`是一个可以扩展的额外字段，利用这两个就可以做成子查询了。

举个例子。对于预算指标，复合指标有若干个子指标，但是直接通过BudgetIndicator模型获取不到它们。就可以这样做
```
{
  BudgetIndicator(criteriaStr:"isComposite=true"){
    id
    isComposite
    child: exprField(expr:"(select string_agg(CONCAT_WS(',',childIndicator.id,childIndicator.name),';')  from BudgetIndicatorComposition where parentIndicatorId=m.id)")
  }
}
```
这里使用了两个sql函数把多条记录、多个字段组合成了一个字符串。拿到数据后前端经过简单的split转化就可以拿到json对象了。

### 常用的sql函数
**string_agg**: 如果查出来有多条结果，会将它们拼装为一个字符串  
例子：string_agg(object.name, ', ')

**coalesce**：如果alias存在则取alias，不存在取name  
例子：string_agg((coalesce(indicator.alias, indicator.name)), ', ')

**concat_ws**：拼装一条记录的多个字段为一个字段  
例子：string_agg(CONCAT_WS(',',childIndicator.id,childIndicator.name),';')


## DataLoader
```ts
const settingDataLoader = new DataLoader(EN_Setting, ['values.value'], {
  criteriaStr: `key='${accountingBook}'`,
} as QueryOptions);

const ret = await settingDataLoader.query();
```

## 不适用DataLoader，直接使用gql
```ts
import client from '@client';
const fetchControlBalance = async (criteriaStr: string, dimensionField: string[]) => {
  const res = await client.query<{ data: Array<IInvoiceType> }>({
    query: `
    {
      data: BudgetControlBalance(criteriaStr: "${criteriaStr}"){
        id
      }
    }
    `,
  });
  return res.data.data
};
```