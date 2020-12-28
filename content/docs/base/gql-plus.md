---
title: GQL plus
---
# gql plus
如何用gql做关联查询/子查询呢？看下面的例子。
```
BudgetIndicator(criteriaStr: "isComposite=true") {
  isComposite
  id
  parents {
    parentIndicatorId
    childIndicator {
      name
      id
    }
  }
  a: exprField(expr: "(select string_agg(id,',') from BudgetIndicatorComposition where parentIndicatorId=m.id)")
  b: exprField(expr: "(select count(id) from BudgetIndicatorComposition where parentIndicatorId=m.id)")
}
```
每个实体上都有一个exprField字段，这个字段接收一个sql作为expr参数。其中的`m.id`是主表（BudgetIndicator）的id，也就是说子查询中可以通过`m`引用到主表。

这样就可以避免在前端进行多次查gql了。