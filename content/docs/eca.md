---
title: "Eca"
date: 2023-08-18T15:13:34+08:00
author: 
---

# 控制显示隐藏

```json
{
    "name": "ReactiveFieldStatus",
    "params": {
        "effect": {
            "expr": "$current.usedOrg.isSalesOrg",
            "fireImmediately": true,
            "status": "Visible"
        },
        "field": "isSales"
    }
}
```

```json
{
    "name": "FieldStatus",
    "description": "金额型存货【数量】不可编辑",
    "params": {
        "expr": "true",
        "field": "quantity",
        "status": "Visible"
    }
},
```

```json
{
    "name": "FieldStatus",
    "description": "金额型存货【数量】不可编辑",
    "params": {
        "expr": "false",
        "field": "quantity",
        "status": "Readonly"
    }
},
```