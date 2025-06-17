## 实现动态面包屑
```vue
<el-breadcrumb separator="/">
	<el-breadcrumb-item v-for="(item,index) of $router.currentRoute.value.matched" :key="index" :to="{ path: item.path }">
		{{ item.name }} 
	</el-breadcrumb-item>
</el-breadcrumb>
```

`$router.currentRoute.value.matched`的值：
![[Snipaste_2023-10-30_09-40-58.png]]

效果
![[Snipaste_2023-10-30_09-42-40.png]]

