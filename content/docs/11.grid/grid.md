# grid

grid是前端解决子表和列表的方案，封装了AdvanceGrid、EntityFormGrid等组件。

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