---
title: "FormBuilder"
date: 2021-12-28T15:38:47+08:00
author: 王书硕
---
它由两部分组成：
一个是form，一个是UI组件

## 创建form

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

1. formScheme定义字段
2. createForm创建form，appendField创建字段，toForm方法，获取form，参数为初始值

## UI组件

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
1. MSTFormLayout是容器，form就是上面创建的form
2. MSTFormElement是字段，各个字段分别使用该组件渲染，根据字段的具体类型，传入相应的参数。

## 校验validate
``` ts
const valid = await this.form.validate();
if (!valid) {
    return;
}
```

1. 在保存等场景，如果需要校验，就调这个方法，会在对应的行出现错误提示

## 坑
1. 不要给MSTFormElement组件传`isRequire={true}`的参数。传了这个参数在手动删除输入框里的值的时候，不会修改form中的值。
2. 如果字段是必填，除了`initState.required`，还必须要`validators: [validators.required]`
3. 如果有必填属性，还要自己调validate方法。