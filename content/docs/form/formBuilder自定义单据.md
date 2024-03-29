---
title: "formBuilder自定义单据"
date: 2021-04-13T21:07:54+08:00
author: 王书硕
---

两部分组成：
1. 创建form
2. form组件
```ts
function createForm(): EntityForm {
  const formScheme = {
    closeDate: {
      type: FieldTypeEnum.Timestamp,
      initState: {
        label: '关闭日期',
        required: false,
        visible: false,
      },
    },
    closedReason: {
      type: FieldTypeEnum.JsonObject,
      referType: EN_BizReason,
      initState: {
        label: '关闭原因',
        required: false,
        visible: false,
      },
    },
    closedReasonExplain: {
      type: FieldTypeEnum.String,
      initState: {
        label: '关闭原因说明',
        required: false,
        visible: false,
      },
    },
  };
  const formBuilder = new FormBuilder();
  Object.entries(formScheme).forEach(([key, value]) => {
    formBuilder.appendField(key, makeField(value));
  });
  return formBuilder.toForm({});
}
```

```tsx
function CloseInfoForm({ form }: { form: EntityForm }) {
  return (
    <MSTFormLayout form={form} columnSize={1}>
      <MSTFormElement path={'closeDate'} />
      <MSTFormElement path="closedReason">
        <Observer>
          {() => (
            <Refer
              entityName={EN_BizReason}
              value={form.value['closedReason']}
              isMulti={false}
              onChange={value => {
                form.select('closedReason').value = value;
              }}
            />
          )}
        </Observer>
      </MSTFormElement>
      <MSTFormElement path="closedReasonExplain" />
    </MSTFormLayout>
  );
}
```