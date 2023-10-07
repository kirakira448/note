## 基础用法
### 安装
```cmd
npm install pinia --save
```
### 创建store仓库
1. 创建一个stores文件夹
2. 创建js文件，根据功能命名，如"count.js"
3. 声明导出对象时的命名规范："use"+"功能（文件名）"+"store"。使用驼峰命名法
```js
import { defineStore } from "pinia"


export const useCountStore = defineStore("count",{
  state:() =>{
    return{
      count:10
     }
   }
})
```
### 加载store
```js
// main.js
import { createApp } from 'vue'
import App from './App.vue'
import { createPinia } from "pinia"


createApp(App).use(createPinia()).mount('#app')
```
### 组件中使用
```HTML
<template>
  <h3>Pinia</h3>
  <p>Count:{{ count }}</p>
</template>
<script setup>
import { useCountStore } from "../stores/count"
const { count } = useCountStore();
</script>

```


## 解构赋值响应式
### 解构赋值
```js
const userInfo={
	name:"zs",
	age:20
}

// 使用 解构赋值 直接获取数值
const { name,age }=userInfo
```
### 解构赋值在pinia中的问题
如果直接从 pinia 中解构数据，会丢失响应式
```js
import { useCountStore } from "../store/count"
const store = useCountStore();
// 这样获得的count可以在template中正常显示，但不能动态更新（失去了响应式）
const { count } = store
```
### 解决方案
引入``storeToRefs`` 解决
```js
// 引入了storeToRefs
import { storeToRefs } from "pinia"
import { useCountStore } from "../store/count"
const store = useCountStore();
// 经过storeToRefs处理后，解构赋值的变量具有响应式

const { count } = storeToRefs(store)
```
## 插件
### 自定义插件
1. 创建plugins文件夹
2. 在文件夹下创建 ``功能.js`` 文件
```js
// 定义插件
export function piniaStoragePlugins({ store}) {
	console.log(store.count)
	store.$subscribe(() => {
		console.log(store.count)
	})
}
```
3. 在``main.js``中引入插件
```js
// 使用插件
import { createApp } from 'vue'
import App from './App.vue'
import { createPinia } from "pinia"
// 引入插件
import { piniaStoragePlugins } from "./stores/plugins"
const pinia = createPinia()
// 使用插件
pinia.use(piniaStoragePlugins)
createApp(App).use(pinia).mount('#app')
```

### 引入第三方插件
*示例-引入持久化插件*
#### 安装
```shell
npm install --save pinia-plugin-persist
```
#### 引入持久化插件
```js
import { createApp } from 'vue'
import App from './App.vue'
import { createPinia } from "pinia"
// 引入
import piniaPersist from 'pinia-plugin-persist'
const pinia = createPinia()
pinia.use(piniaPersist)
createApp(App).use(pinia).mount('#app')
```
#### 使用持久化插件
在需要使用插件的``store``文件中加入代码
```js
import { defineStore } from "pinia"
export const useCountStore = defineStore("count", {
  state: () => {
    return {
      count: 10
     }
   },
  // 引入插件
  persist: {
    enabled: true,
    strategies: [
       {
        key: 'counts', //自定义 Key值
        storage: localStorage, // 选择存储方式
       },
     ],
   }
})

```
