1.config table CRUD
```
id
key  text
value array
```

input: key
output: list(value)

2.product
input:list(id)
output:list(ProductSearchDto)

3.cart
input: list(product_id)
更新cart数据
output: latest_cart_data

查询


4.order
日期处理

月，周，日，売上データ
注文統計

根据状态groupby返回数据



5.添加product状态字段
添加product库存警戒值
