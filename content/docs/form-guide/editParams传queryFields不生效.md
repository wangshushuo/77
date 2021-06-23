---
title: "EditParams传queryFields不生效"
date: 2021-05-21T18:15:30+08:00
draft: true
---

1. apps/link/src/components/form-layout/MSTFormLayout.tsx文件
这里用了DataField组件，189行，editParams中的queryFields和referConfig.queryFields都在。
2. 进入到DataField.tsx文件
case "refer"时，两个queryFields也都在。这里用了ReferField组件

3. apps/link/src/components/mst-field/ReferField.tsx文件
