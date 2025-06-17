# 隐藏表头

添加属性：`:show-header="false"`，可以动态控制
```vue
<el-table :data="tableData" table-layout="fixed" :show-header="false">

</el-table>
```

# 修改选中行样式

```css
::v-deep .el-table__body tr.current-row > td {
    background: #f0f9eb !important;
}
```