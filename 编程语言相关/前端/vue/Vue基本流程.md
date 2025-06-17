[官网地址](https://vuejs.org/)
[官方中文文档](https://cn.vuejs.org/guide/introduction.html)
*Vue (发音为 /vjuː/，类似 **view**) 是一款用于构建用户界面的 JavaScript 框架。*
## 0. 基本环境

安装 16.0 或更高版本的 [Node.js](https://nodejs.org/)
## 1. 初始化项目
创建文件目录，在目录下打开命令行工具，运行命令
```shell
npm create vue@latest
```

![[Snipaste_2023-10-30_10-23-49.png]]
[搭配 TypeScript 使用 Vue](https://cn.vuejs.org/guide/typescript/overview.html)
[vue-router官网](https://router.vuejs.org/)
[Pinia官网](https://pinia.vuejs.org/)

选择结束后，如果创建成功会出现提示

![[Snipaste_2023-10-30_10-29-22.png]]

按照提示输入命令，就可以成功运行项目。

点击出现的链接，看到如下画面说明成功。
![[Snipaste_2023-10-30_10-31-32.png]]

## 2. 引入 ElementPlus
[ElementPlus官网](https://element-plus.org/zh-CN/)
*ElementPlus 是一个Vue3 UI 框架*
### 安装Element-Plus
```shell
npm install element-plus --save
```

### 按需导入

>如果不配置按需导入，需要在每一次使用时导入所需组件

首先你需要安装`unplugin-vue-components` 和 `unplugin-auto-import`这两款插件
```shell
npm install -D unplugin-vue-components unplugin-auto-import
```
然后修改`vite.config.js`配置文件
```js
// vite.config.ts
import { defineConfig } from 'vite'
import AutoImport from 'unplugin-auto-import/vite'
import Components from 'unplugin-vue-components/vite'
import { ElementPlusResolver } from 'unplugin-vue-components/resolvers'


export default defineConfig({
 // ...
 plugins: [
  // ...
  AutoImport({
   resolvers: [ElementPlusResolver()],
   }),
  Components({
   resolvers: [ElementPlusResolver()],
   }),
  ],
})
```
之后，在组件中可以直接使用element-plus。

## 3. 引入axios

*用于网络请求*
### 3.1. 安装axios

```bash
npm i axios
```

### 3.2. 基础配置

> 官方文档地址：[https://axios-http.com/zh/docs/intro](https://axios-http.com/zh/docs/intro) 基础配置通常包括：
> 
> 1. 实例化 - baseURL + timeout
>     
> 2. 拦截器 - 携带token 401拦截等
>     

```js
// axios基础封装
import axios from "axios";
  
// 创建axios实例  
const httpInstance = axios.create({
    // 1.接口基地址
    baseURL: 'http://127.0.0.1:3000',
    // 2.超时时间
    timeout: 5000
})
  
// 3.axios请求拦截器  
httpInstance.interceptors.request.use(config => {
    return config
}, e => Promise.reject(e))
  
// 4.axios响应式拦截器  
httpInstance.interceptors.response.use(res => res.data, e => {
    return Promise.reject(e)
})
    
export default httpInstance
```

## 4. 基本文件结构

根据需要创建文件夹

![[Snipaste_2023-10-30_10-48-44.png]] 

- api: 存放所有api文件
- assets：存放静态资源
- components：自定义组件，通常都是可以复用的组件
- plugins：自定义插件，引入的第三方插件通常在这里
- router：路由文件，vue-router的使用
- stores：Pinia的状态管理文件
- types：ts的type存放位置
- utils：自定义工具
- **views**：所有页面的位置
- `App.vue`：所有组件的根组件（root component）


## 5. 基本开发流程

1. 创建页面组件
	1. 在 ElementPlus 中选择合适的组件，组成所需的页面
	2. 根据需要可以选择其他第三方插件或自定义
	3. 定义script与style
2. 定义api文件
	1. 确定需要发送与接收的数据
	2. 定义api
3. 使用api工具测试
	1. stoplight
	2. postman
	3. ...
4. 完成前端页面与api设计后，与后端连接。






