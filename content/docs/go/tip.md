# tip

trait.GetValueByPath(res.Data, "isBusinessStatusEnabled", false)

ctx.GetBizFormRuleManager().AddReadonlyControl(gen_ef.F_Project_businessStatus, true)

api := ctx.GetMetadataApi()
api.AppendDetailColumns(childField)
api.SetDetailVisible(gen_ef.F_BusinessStatusExecSolution_scopes, "businessStatusArr", false)

标准CRud
ctx.GetContext().GetEntityService().Update(gen_en.EN_VerifyDef, transOutStr)

# dataTrunk

dataTrunk就是自己处理保存的数据

```go
func GetDataTrunk(params form_context.DataTrunkParams) form_context.DataTrunk {
	return form_services_trunks.NewDataTrunk(form_context.DataTrunkParams{
		DataSaveConsumer: form_context.DataSaveConsumer{
			Create: func(ctx form_context.FormSaveContext, data interface{}) interface{} {
				// TODO 1
				transOutStr := utils.ToString(data)
				result := ctx.GetContext().GetEntityService().Create(gen_en.EN_VerifyDef, transOutStr)
				return result
			},
			Update: func(ctx form_context.FormSaveContext, data interface{}) interface{} {
				// 数据处理
                // ...
                // 保存数据
				return ctx.GetContext().GetEntityService().Update(gen_en.EN_BusinessStatusExecSolution, d3)
			},
		},
	})
}
```


ctx.GetParamsTrunk().AddPrepareQueryFields
ctx.GetParams().PrepareParams
getParallelDataTrunk, initQuery