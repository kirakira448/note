# 菜单同步当前路由

修改`el-menu`属性，添加如下两个属性
```vue
<el-menu :default-active="$router.currentRoute.value.path" :router="true">
</el-menu>
```

修改`el-menu-item`属性，修改index属性为`:index="当前路由"`
```vue
<el-menu-item v-else :index="item.path">
</el-menu-item>
```

