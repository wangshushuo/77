---
title: "Fetch Gql"
date: 2021-08-19T11:00:12+08:00
author: 王书硕
---

```go
import (
	gql_util "q7link.com/app/trek/services/form-services/middlewares/entities/project/gql-util"
)

func fetchBudgetPlan(projectId string, usedOrgId string, ctx form_context.FormContext) []Plan {
	result := FieldMappingRes{}
	gql := gql_util.GQL{
		QueryGqlTemplate: `{
			BudgetPlan(criteriaStr: "createdOrgId='{{.createdOrgId}}' AND projectId='{{.projectId}}'") { 
				billStatus 
			}
		}`,
		BindVars: map[string]string{
			"createdOrgId": usedOrgId,
			"projectId": projectId,
		},
		Result:        &result,
		Ctx:           ctx.GetContext(),
	}
	gql.Fetch()
	return result.Data.BudgetPlan
}
```