## 查询id是否在array类型中

基本格式：
```sql
id = any(array[1,2,3,4])
```

复合查询：
```sql
select * from permission  
where id = ANY(array(select permission_id_list from role_permission where role_id=1))
```