当子组件中需要使用动态数据时，需要使用emit发送给父组件。
>一般，父传子的数据可以由父组件动态修改，但是不能被子组件修改
>例如：`<el-pagination>` 组件中，`current-page`属性不能直接用prop传递

### 【示例】`<el-pagination>` 动态传递`current-page`

子组件
```vue
<script setup >
const props=defineProps({
    currentPage: {
        type: Number,
        default: 5
    },
    pageSize: {
        type: Number,
        default: 23
    },
    total: {
        type: Number,
        default: 1000
    },
    handleSizeChange: {
        type: Function,
        default: () => console.log('Size Change')
    },
})

const emits=defineEmits(['currentPage'])
function emitToParent() {
  emits('currentPage', currentPageRef.value);
}

import { ref} from "vue";

const currentPageRef=ref(props.currentPage)


</script>

<template>
<el-pagination  v-model:current-page="currentPageRef" :page-size="pageSize"
	layout="total, sizes, prev, pager, next, jumper" 
	:total="total" @size-change="handleSizeChange"
	@current-change="emitToParent" />
</template>
```

>1. 使用prop接收父组件第一次传入的currentPage
>2. 创建新的ref变量，动态存储数据，并绑定到v-model
>3. 使用emits定义变量名
>4. 定义一个函数，使用emits发送子组件数据
>5. 将函数绑定到`@current-change`（组件自带的方法），每当`currentPage`改变，就触发函数，发送当前页码。


父组件：
```vue
<script>
// 当子组件的currentPage变更时，触发这个函数接收变更，并执行翻页
const pageChange=(num:number)=> {
    paginationInfo.value.currentPage = num;
    getVehicleData(8, paginationInfo.value.currentPage * 8)
    // console.log(paginationInfo.value.currentPage, paginationInfo.value.total);
}
</script>
<template>
<MainFooter :current-page="paginationInfo.currentPage" :page-size="paginationInfo.pageSize"
:total="paginationInfo.total" :handle-size-change="paginationInfo.handleSizeChange"
 @currentPage="pageChange"/>
 </template>
```

>1. 使用`@emit变量名="自定义函数名"`接收子组件发送的变量
>2. 函数接收一个参数，这个参数值就是子组件发送的变量值
>3. 因为每次接收到变量，都是触发了`@current-change`，所以可以直接在这个函数里执行`handleCurrentChange`的逻辑。
