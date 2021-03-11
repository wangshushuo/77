---
title: "Gen"
date: 2021-03-10T17:41:36+08:00
author: 
---

http://172.31.23.98:8080/job/front-gen/

gen:
1. 在app/go-gen中修改main/index.go中的ApiHost变量为你环境的host，运行gen.sh；
2. 提交代码，部署trek到目标环境；
3. 在jinkens的front-gen中，左边的Build with Parameters生成目标分支、目标环境的web的gen；
4. 获取PR地址，修改remote分支，默认是master，合并代码

## 问题
1. 某些变量在本地跑完gen后不见了
    - 可能是后端该了某些属性的名字，但是0租户没有同步。