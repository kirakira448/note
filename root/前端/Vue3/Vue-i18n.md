>官网地址：[https://vue-i18n.intlify.dev/](https://vue-i18n.intlify.dev/)
# 初始化
## 安装
```shell
npm install --save vue-i18n@next
```
## 配置
新建文件：`src/plugins/i18n/i18n.js`
```js
import { createI18n } from 'vue-i18n'
import zh from "./lang/zh"
import en from "./lang/en"
const messages = {
// 字段较多时，新建一个lang文件夹，分别用zh.js,en.js存储字段
  zh,
  en
}


const i18n = createI18n({
  legacy:false, // 必须配置，否则报错,而且只能是false
  // 从本地存储获取值（'zh','en'）
  locale: localStorage.getItem("lang"), // 设置当前语言环境
  globalInjection:true, // 允许访问形式 $t 来访问
  messages
})


export default i18n
```
`./i18n/lang/zh.js`
```js
export default{
    message:{
        navs: '当前'
    }
}
```
## 引入
`main.js`
```js
import { createApp } from 'vue'
import Vuei18n from "./locales/i18n.js"


const app = createApp(App)


app.use(Vuei18n)
app.mount('#app')
```
## 应用
```vue
<div>{{ $t("message.navs") }}</div>
<div class="lang">
	<el-dropdown>
	  <span class="el-dropdown-link">
		语言切换
		<el-icon class="el-icon--right">
			<arrow-down />
		</el-icon>
	</span>
	<template #dropdown>
		<el-dropdown-item @click="changeLang('zh')">中文</el-dropdown-item>
		<el-dropdown-item @click="changeLang('en')">English</el-dropdown-item>
	</template>
	</el-dropdown>
</div>

<script setup>
// 切换语言
const changeLang=(lang)=>{
	// 与i18n.js中设定的字段相同
    localStorage.setItem("lang",lang)
    // 刷新页面
    location.reload();
}
</script>
```