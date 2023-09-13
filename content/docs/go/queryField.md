# queryFields

有现成的api可以添加queryField，并且QueryField是结构化的，可以加queryOption比如查询条件等。

```go
func newQueryFieldsMiddleware() form_context.FormMiddlewareCreator {
	return func() form_context.FormMiddlewares {
		return new(queryFieldsMiddleware)
	}
}

type queryFieldsMiddleware struct {
}

func (m *queryFieldsMiddleware) Register(ctx form_context.FormContext) {
	form_services_api.SetQueryField(context.QueryField{
		QueryOptions: &context.QueryOptions{CriteriaStr: "drawTypeId='BudgetDrawType.auxField' AND lineOrientation.id = 'BudgetLineOrientation.column'"},
		FieldName:    "planSubtables.lines",
	}, ctx)
	form_services_api.SetQueryField(context.QueryField{FieldName: "planSubtables.lines.lineIndex"}, ctx)
}

```