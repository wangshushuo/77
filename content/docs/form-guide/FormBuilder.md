---
title: "FormBuilder"
date: 2021-12-28T15:38:47+08:00
author: 王书硕
---
由两部分组成：
一个是form，一个是UI组件
```ts
const formScheme = {
    closeDate: {
        type: FieldTypeEnum.Timestamp,
        initState: {
            label: '关闭日期',
            required: true,
            visible: false,
        },
        validators: [validators.required]
    },
};

  const createForm = (): EntityForm =>  {
    const formBuilder = new FormBuilder();
    Object.entries(this.formScheme).forEach(([key, value]) => {
      formBuilder.appendField(key, makeField(value));
    });
    return formBuilder.toForm({
      closeDate: this.getDefaultCloseDate(),
    });
  }
```

```tsx
export function CloseForm(props) {
  return (
    <MSTFormLayout form={props.form} columnSize={1}>
      <MSTFormElement path={'closeDate'} minDate={props.minCloseDate} />
      <MSTFormElement
        path="closedReason"
        criteriaStr={`objectBizActions.objectBizAction.objectType = 'CalendarEntry' and objectBizActions.objectBizAction.action.id = 'close' and isDisabled = false`}
        isMulti={false}
        contextOrgIds={props.contextOrgIds}
      />
      <MSTFormElement path="closedReasonValue" />
    </MSTFormLayout>
  );
}
```

``` ts
const valid = await this.form.validate();
if (!valid) {
    return;
}
```

## 坑
1. 不要给MSTFormElement组件传`isRequire={true}`的参数。传了这个参数在手动删除输入框里的值的时候，不会修改form中的值。
2. 如果字段是必填，除了`initState.required`，还必须要`validators: [validators.required]`
3. 如果有必填属性，还要自己调validate方法。