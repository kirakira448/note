>vue3版本官网：https://vant-contrib.gitee.io/vant/#/zh-CN
## 1.安装Element-Plus
```shell
npm i vant --save
```
### 1.1 项目中引入Vant
```js
// main.js
// 根据需求选择要引入的组件
import { Button } from 'vant';
import 'vant/lib/index.css';

app.use(Button);
```
```vue
<template>
 <van-button type="primary">主要按钮</van-button>
 <van-button type="success">成功按钮</van-button>
 <van-button type="default">默认按钮</van-button>
 <van-button type="warning">警告按钮</van-button>
 <van-button type="danger">危险按钮</van-button>
</template>
<script setup></script>
```
### 2.1 按需加载
使用 `unplugin-vue-components` 插件，它可以自动引入组件，并按需引入组件的样式。
#### 安装插件
注意：需要先安装vant
```shell
npm i unplugin-vue-components -D
```
#### 配置插件
在`vite.config.js` 文件中配置
```js
import { fileURLToPath, URL } from 'node:url'
import { defineConfig } from 'vite'
import vue from '@vitejs/plugin-vue'
// 1.引入
import Components from 'unplugin-vue-components/vite';
import { VantResolver } from 'unplugin-vue-components/resolvers';

export default defineConfig({
 plugins: [
  vue(),
  // 2.添加组件
  Components({
   resolvers: [VantResolver()],
   })
  ],
 resolve: {
  alias: {
   '@': fileURLToPath(new URL('./src', import.meta.url))
   }
  }
})
```

#### 使用组件
可以直接使用，已经在config文件中引用过了
```vue
<template>
 <van-button type="primary">主要按钮</van-button>
 <van-button type="success">成功按钮</van-button>
 <van-button type="default">默认按钮</van-button>
 <van-button type="warning">警告按钮</van-button>
 <van-button type="danger">危险按钮</van-button>
</template>
<script setup></script>
```