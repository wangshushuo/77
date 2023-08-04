---
title: "Spread.js"
date: 2022-07-13T14:27:15+08:00
author: 
---

## 开启过滤功能
```js
// Configure Workbook and Worksheet
var spread = new GC.Spread.Sheets.Workbook("ss");
var activeSheet = spread.getActiveSheet();    

activeSheet.setValue(0, 0, "North");
activeSheet.setValue(1, 0, "South");
activeSheet.setValue(2, 0, "East");
activeSheet.setValue(3, 0, "South");
activeSheet.setValue(4, 0, "North");
activeSheet.setValue(5, 0, "North");
activeSheet.setValue(6, 0, "West");
activeSheet.setColumnWidth(0, 80);
           
// Set a row Filter
activeSheet.rowFilter(new GC.Spread.Sheets.Filter.HideRowFilter(new GC.Spread.Sheets.Range(0, 0, 7, 1)));

// Filter column 1 by "North"
var rowFilter = spread.getActiveSheet().rowFilter();
var condition = new GC.Spread.Sheets.ConditionalFormatting.Condition(
    GC.Spread.Sheets.ConditionalFormatting.ConditionType.textCondition, {
        compareType: GC.Spread.Sheets.ConditionalFormatting.TextCompareType.equalsTo,
        expected: "North"
});
rowFilter.addFilterItem(0, condition);
rowFilter.filter(0);
```

`GC.Spread.Sheets.Range` 会设置过滤的范围，查过这个范围不会过滤和隐藏。

## 合并单元格
```js
sheet.addSpan(1, 4, 1, 7); // 参数依次：开始行、开始列、行数、列数
sheet.removeSpan(20, 1);
```