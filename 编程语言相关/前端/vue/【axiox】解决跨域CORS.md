
## 1. 修改baseURL

将baseURL修改为`'/api'`
```ts
const http = axios.create({
    // 1.接口基地址
    // baseURL: 'http://127.0.0.1:8080',
    baseURL: '/api',
    // 2.超时时间
    timeout: 5000
})
```

## 2. 修改`vite.config.ts`

在defineConfig中新增配置
```ts
export default defineConfig({

  // ...
  server:{
    proxy:{
      '/api':{ // 获取路径中包含 /api 的请求
        target:'http://127.0.0.1:8080',   // 后端服务所在源
	        changeOrigin:true,// 是否修改源
        rewrite:(path)=>path.replace(/^\/api/,'') //将/api 替换为空
      }
    }
  }
})
```