## 导航守卫
### 全局前置守卫
`router.beforeEach` 注册一个全局前置守卫,当一个导航触发时，就会触发全局前置守卫
```js
router.beforeEach((to, from, next) => {
	// 返回 false 以取消导航
	next() 
})
```
to: 将要前往的路由。
from: 来源路由
next: 
- 不添加参数表示 继续执行
```js
next()
```
- 添加参数，可以重新定向
```js
next({
	path:"/login"
})
```
例：使用导航守卫验证登录
```js
// 在需要验证的路由中添加meta信息
/*
	meta:{
		requiresAuth:true
	}
*/
router.beforeEach((to,from,next)=>{
  if(to.meta.requiresAuth){
    // 需要验证登录
    const loginStore=useLoginStore()
    if(!loginStore.token){
      next({
        path:'/login'
      })
    }else{
      next()
    }
  }else{
    next()
  }
})
```
## 动态路由
### 404 路径匹配规则
```js
    {
      // 404 路径匹配规则
      path: '/:pathMatch(.*)*',
      name: 'notfound',
      component: ()=>import("../views/notFound/index.vue"),
    }
```
