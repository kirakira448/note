postgresql 自带user表，user是关键字！！！

例如：直接使用`user`，查询到的是自带的user
```sql
SELECT * FROM user;
```

错误写法：
```sql
SELECT * FROM user WHERE username='wangba';
```
这样可能会报错：找不到username列。


想要访问自定义的user，需要加public前缀
```sql
SELECT * FROM public.user WHERE username='wangba';
```