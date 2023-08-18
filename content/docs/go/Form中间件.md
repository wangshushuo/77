---
title: "Form中间件"
date: 2023-08-18T14:38:49+08:00
author: 
---

# GetFormSolutionPipeline 修改solution

```go
type userHandlerMiddleware struct {
	ctx context.TrekContext
}

func NewUserHandleMiddleware() form_context.FormMiddlewares {
	return new(userHandlerMiddleware)
}

func (m *userHandlerMiddleware) Register(ctx form_context.FormContext) {
	ctx.GetFormSolutionPipeline().Add(m.resolveUser)
}

func (m *userHandlerMiddleware) resolveUser(ctx form_context.FormContext, solution *context.SolutionMetadata) *context.SolutionMetadata {

	hasOwnerLegalEntityOrg := solution.FormTemplate.Contains("ownerLegalEntityOrg")
	if hasOwnerLegalEntityOrg && !ctx.IsEnabledMultiOrg() {
		solution.FormTemplate.Header[0].Remove("ownerLegalEntityOrg")
	}

	if !hasOwnerLegalEntityOrg && ctx.IsEnabledMultiOrg() {
		ownerLegalEntityOrgField := new(template.Field)
		ownerLegalEntityOrgFieldStr := `{
			"path": "ownerLegalEntityOrg",
			"required": true,
			"readonly": false,
			"displayName": "",
			"isSlot": false,
			"extended": false,
			"colspan": 1,
			"rowspan": 0
		}`
		json.Unmarshal([]byte(ownerLegalEntityOrgFieldStr), ownerLegalEntityOrgField)

		solution.FormTemplate.Header[0].Items = append([]template.Field{*ownerLegalEntityOrgField}, solution.FormTemplate.Header[0].Items...)
	}

	return solution
}
```

# AddInitItem 修改response

```go
type userHandlerMiddleware struct {
	ctx context.TrekContext
}

func NewUserHandleMiddleware() form_context.FormMiddlewares {
	return new(userHandlerMiddleware)
}

func (m *userHandlerMiddleware) Register(ctx form_context.FormContext) {
	ctx.AddInitItem(promise_util.PromiseItem{
		Executor: func() (i interface{}, e error) {
			tenantId := ctx.GetContext().GetTenantUser().TenantId
			return GetTenantRightsInfo(m.ctx, tenantId), nil
		},
		Resolve: func(result interface{}) {
			if result != nil {
				ctx.GetResponse().ExtraData["userRightAuthInitData"] = result
			}
		},
	})
}
```