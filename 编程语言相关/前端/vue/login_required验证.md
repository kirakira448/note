`router/index.js`
```js
// 做router跳转的login_required验证
router.beforeEach((to, from, next) => {
 if (to.path =='/login'){
  next()
  }else{
  // 获取token值
  const token = sessionStorage.getItem('token')
  if (!token){
   next('/login')
   }
  next()
  }
})
```