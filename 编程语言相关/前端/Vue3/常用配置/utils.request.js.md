### 隧道管理项目
```js
import axios from "axios"
import qs from "querystring"
/**
 * 处理错误信息
 * status:状态吗
 * info:具体信息
 */
const errorHandle = (status, info) => {
    switch (status) {
        case 400:
            console.log("语义错误");
            break;
        case 401:
            console.log("服务器认证失败");
            break;
        case 403:
            console.log("服务器请求拒绝执行");
            break;
        case 404:
            console.log("请检查网路请求地址");
            break;
        case 500:
            console.log("服务器发生意外");
            break;
        case 502:
            console.log("服务器无响应");
            break;
        default:
            console.log(info);
            break;
    }
}
/**
 * 创建Axios对象
 */
const instance = axios.create({
    // 公共配置
    baseURL: "http://iwenwiki.com",
    timeout: 5000
})
/**
 * 拦截器
 *  发送请求和响应结果之前都可以拦截
 */
instance.interceptors.request.use(
    // 成功
    config => {
        // config：请求信息
        if (config.method === 'post'||config.method === 'put') {
            // post请求的参数格式化
            config.data = qs.stringify(config.data)
        }
        return config
    },
    // 失败
    error => Promise.reject(error)
)
instance.interceptors.response.use(
    // 成功
    response => response.status === 200 ? Promise.resolve(response) : Promise.reject(response),
    // 失败
    error => {
        const { response } = error;
        if (response) {
            errorHandle(response.status, response.info)
        } else {
            console.log("网络请求被中断了");
        }
    }
)
export default instance
```


### vue-shop项目
```js
import router from "@/router/index.js";
import axios from "axios"


const errorHandle = (status,info) =>{
  switch(status){
    case 400:
      console.log("语义错误");
      break;
    case 401:
      console.log("服务器认证失败");
      break;
    case 403:
      console.log("服务器请求拒绝执行");
      break;
    case 404:
      console.log("请检查网路请求地址");
      break;
    case 500:
      console.log("服务器发生意外");
      break;
    case 502:
      console.log("服务器无响应");
      break;
    default:
      console.log(info);
      break;
   }
}
/**
 * 创建Axios对象
 */
const instance = axios.create({
  timeout:5000,
})




instance.interceptors.request.use(
  config =>{
    // 获取token
    let token = sessionStorage.getItem('token')
    if(token){
      // 请求头添加token
      config.headers.token = token
    }
    return config
   },
  error => Promise.reject(error)
)
instance.interceptors.response.use(
  // response => response.status === 200 ? Promise.resolve(response) : Promise.reject(response),
  response=>{
    if (response.status===200){
      if (response.data.status === 401){
        // 删除无效token值
        sessionStorage.removeItem('token');
        // token失效
        router.push('/login');
      }
      return Promise.resolve(response);
      
    }else{
      return Promise.reject(response);
    }
  },
  error =>{
    const { response } = error;
    if(response){
      errorHandle(response.status,response.info)
     }else{
      console.log("网络请求被中断了");
     }
   }
)
export default instance
```


### 小兔鲜项目
```js
// axios基础封装
import axios from "axios";
import { ElMessage } from 'element-plus'
import 'element-plus/theme-chalk/el-message.css'
import {useUserStore} from '@/stores/userStore'
import router from '@/router'

// 创建axios实例  
const httpInstance = axios.create({
    // 1.接口基地址
    baseURL: 'http://pcapi-xiaotuxian-front-devtest.itheima.net',
    // 2.超时时间
    timeout: 5000
})

// 3.axios请求拦截器  
httpInstance.interceptors.request.use(config => {
    // 1. 从pinia获取token数据
    const userStore = useUserStore()
    // 2. 按照后端的要求拼接token数据
    const token = userStore.userInfo.token
    if (token) {
        // 按照后端要求拼接token
        config.headers.Authorization = `Bearer ${token}`
    }
    return config
}, e => Promise.reject(e))

// 4.axios响应式拦截器  
httpInstance.interceptors.response.use(res => res.data, e => {
    const userStore = useUserStore()
    // 统一错误提示
    ElMessage({
        type: 'warning',
        message: e.response.data.message
    })

    // 401 token失效处理
    if (e.response.status===401){
        // 清除用户数据
        userStore.clearUserInfo()
        // 跳转登录页面
        router.push('/login')
    }
    return Promise.reject(e)
})


export default httpInstance
```