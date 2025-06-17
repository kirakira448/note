>官网：https://element-plus.org/zh-CN

## 1.安装Element-Plus
```shell
npm install element-plus --save
```

### 按需导入
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
## 2.使用字体图标
### 安装`icons`字体图标
```shell
npm install @element-plus/icons-vue
```
### 全局注册
在项目根目录(src)下，创建`plugins`文件夹，在文件夹下创建文件`icons.js`文件
```js
// icons.js
import * as components from "@element-plus/icons-vue";
export default {
  install: (app) => {
    for (const key in components) {
      const componentConfig = components[key];
      app.component(componentConfig.name, componentConfig);
     }
   },
};
```
### 引入文件
在`main.js`中引入`icons.js`文件
```js
import elementIcon from "./plugins/icons";
app.use(elementIcon)
```
### 使用方式
接下来就可以直接在组件中引入使用了
```vue
<el-icon class="myicon" ><House /></el-icon>
<el-icon class="myicon" ><Star /></el-icon>
<el-icon class="myicon"><Ticket /></el-icon>
```
#### 在按钮或者菜单中使用
```vue
<el-button type="success" :icon="Check" circle />
```
```vue
<script setup>
import { Check,Edit,Search,Message,Star,Delete } from '@element-plus/icons-vue'
</script>
```


# 组件
## Basic 基础组件
### icon图标
#### 动态使用icon
将`<el-icon><Pouring /></el-icon>`标签的形式替换为：
```vue
<component class="icon" :is="item.icon"></component>
```
#### 垂直居中
默认情况，icon不能垂直居中，与文字形成偏移
***解决方法***
1. 将外层div设置为display:flex，设置垂直居中
```CSS
.logo-show{
    display: flex;
    align-items: center;
}
```
2. 将el-icon设置一个size，大概和文字一样大即可
```CSS
.logo-show-icon{
    size: 16px;
}
```
## Form 表单组件
### Form 表单
- prop:
	-  `model` 的键名。 它可以是一个路径数组(例如 `['a', 'b', 0]`)。 在定义了 `validate`、`resetFields` 的方法时，该属性是必填的。
	- Form组件提供了表单验证的功能，只需为 `rules` 属性传入约定的验证规则，并将 `form-Item` 的 `prop` 属性设置为需要验证的特殊键值即可。
- 在输入框里添加icon
	1. :prefix-icon="User"     "User" 为icon名称
	2. 注意，需要在script中引入icon图标
- 
## Navigation 导航
### Menu 菜单
#### router:
	- 定义
		- 是否启用 `vue-router` 模式。 启用该模式会在激活导航时以 index 作为 path 进行路由跳转 使用 `default-active` 来设置加载时的激活项。
	- 使用方法
		- 在父元素`el-menu`中定义 `:default-active="active"` 添加 `router`
		- 在子元素`el-menu-item`中定义 `index="/"`
		- 点击将会跳转路由
#### 折叠
##### 开启折叠
添加属性 `collapse`开启折叠
```vue
<el-menu :collapse="menuStore.isCollapse">
	...
</el-menu>
```
##### 折叠时不能显示icon
***错误示例***
`<component>`用于承载icon，外层不包裹`<el-icon>`时，menu在折叠时不能显示icon
```vue
<el-sub-menu v-if="item.children" :index="item.path">
	<template #title>

			<component class="icon" :is="item.icon"></component>

		<span>{{ item.name }}</span>
	</template>
</el-sub-menu>
```
***正确做法***
在`<component>`外层包裹`<el-icon>`后可以正确显示icon
```vue
<el-sub-menu v-if="item.children" :index="item.path">
	<template #title>
		<el-icon>
			<component class="icon" :is="item.icon"></component>
		</el-icon>
		<span>{{ item.name }}</span>
	</template>
</el-sub-menu>
```
### Dropdown 下拉菜单
#### 去除外框
- 问题描述
	在鼠标触发下拉菜单时，有时会出现外框
- 解决方法
```css
.el-dropdown-link:focus {
	outline: none;
}
```

## Feedback 反馈组件
### Dialog 对话框
#### destroy-on-close
关闭时，销毁对话框，可以用于刷新对话框，清除缓存
# 进阶
## 国际化
Element-Plus组件默认是英文的，需要使用其他语言版本时要进行国际化配置
### 全局配置
`main.js`
```js
import ElementPlus from 'element-plus'
import zh from 'element-plus/dist/locale/zh-cn.mjs'
import en from 'element-plus/dist/locale/en.mjs'

app.use(ElementPlus, {
  // 静态
  // locale: zh,
  // 绑定本地存储，可以动态切换
  locale: localStorage.getItem("lang") === 'zh' ? zh : en,
})
```
