---
title: "EntityFormGrid"
date: 2021-11-05T17:49:01+08:00
author: 
---
EntityFormGrid一般用在自定义渲染，需要渲染一个表格（子表），行上有删除等按钮。

下面是一些例子：
```jsx
<EntityFormGrid
  autoHeightMaxRows={999}
  autoHeightMinRows={3}
  columnDefs={this.presenter.ColDefs}
  data={this.presenter.data}
  shouldRowInitialized={() => true}
  onRowInitialized={(
    logicPath: string,
    rowField: MSTFormField,
    rowIndex: number,
    disposers: Array<IDisposer>,
  ) => {
    const depnDepartment = rowField.select(F_AssetValueItem_depnDepartment);
    if (!depnDepartment) {
      return;
    }
    disposers.push(
      reaction(
        () => depnDepartment.value,
        value => {}
      ),
    );
  }}
  mstFormOption={mstFormOption}
  suppressAutoAppendRow
  actionColumnOption={{
    rowActions: this.rowActions(),
  }}
  // key={this.presenter.realIndex}
/>
```

```jsx
<EntityFormGrid
  autoContainerWidth={false}
  // onRowHovered={(index) => this.handleRowHover}
  shouldRowInitialized={() => {
    return true;
  }}
  onRowInitialized={() => { }}
  isRowChanged={(rowIndex, rowData) => {
    return rowData.summary;
  }}
  columnDefs={this.colDef}
  data={this.dataViewHandler(this.props.isGenerateVoucherSetting)}
  cellFormatter={this.cellFormatter}
  // height={400}
  columnResolver={this.columnResolver}
  actionColumnOption={this.actionColumnOptions}
  indicateColumnOption={this.indicateColumnOptions}
  onRowDragEnd={this.isEditMode && this.rowDragEnd}
  mstFormOption={{
    form: this.formPresenter.form,
    logicPath: 'mappingItems',
    path: 'mappingItems',
    isEmptyRow(rowData: any): boolean {
      return !rowData[VOUCHER_TEMPLATE_FACT_ITEM];
    },
    onWillAppendRow: () => {
      this.formPresenter.entityCRUD.appendRow('mappingItems', {});
    },
  }}
/>
```


```jsx
<EntityFormGrid
  columnDefs={this.columnDefs}
  shouldRowInitialized={() => true}
  onRowInitialized={() => {}}
  mstFormOption={{
      form: this.form,
      logicPath: 'auxItems',
      path: 'auxItems',
      onWillAppendRow: () => {},
      isEmptyRow: () => false,
    }}
  data={this.formValue}
/>
```

```jsx
 <EntityFormGrid
  autoHeightMaxRows={999}
  autoHeightMinRows={3}
  columnDefs={this.presenter.ColDefs}
  data={this.presenter.data}
  shouldRowInitialized={() => true}
  onRowInitialized={(
    logicPath: string,
    rowField: MSTFormField,
    rowIndex: number,
    disposers: Array<IDisposer>,
  ) => {
    const depnDepartment = rowField.select(F_AssetValueItem_depnDepartment);
    if (!depnDepartment) {
      return;
    }
    disposers.push(
      reaction(
        () => depnDepartment.value,
        value => {}
      ),
    );
  }}
  mstFormOption={{
    form: this.formPresenter.form,
    logicPath: 'mappingItems',
    path: 'mappingItems',
    isEmptyRow(rowData: any): boolean {
      return !rowData[VOUCHER_TEMPLATE_FACT_ITEM];
    },
    onWillAppendRow: () => {
      this.formPresenter.entityCRUD.appendRow('mappingItems', {});
    },
  }}
  suppressAutoAppendRow
  actionColumnOption={{
    rowActions: this.rowActions(),
  }}
  // key={this.presenter.realIndex}
/>

```