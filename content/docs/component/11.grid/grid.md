# grid

grid是前端解决子表和列表的方案，封装了AdvanceGrid、EntityFormGrid等组件。

columnDef的文件 packages/kaleido/packages/uikit/athena-ui/src/components/ag-grid/entities/colDef.ts

## AdvanceGrid

### 配置
排序、过滤、搜索
```jsx
<AdvanceGrid
    key={this.state.overLogData.length}
    headerFilter={true}
    searchEnable={true}
    enableSorting={true}
/>
```
排序还要给columnDef设置sortable为true

- 列宽
autoContainerWidth为true会让grid自动充满容器，列宽会不规定，可以设置maxWidth控制最大宽大。同时不能手动调整列宽。

如果要手动调整列宽就要像下面的代码这样设置才行
```jsx
<AdvanceGrid
    key={this.state.overLogData.length}
    enableColResize={true}
    autoContainerWidth={false}
/>
```
