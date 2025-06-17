对引用集合的 URI 使用复数名词
最好是将集合和项的 URI 组织成层次结构。
例如，`/customers` 是客户集合的路径，`/customers/5` 是 ID 为 5 的客户的路径。

## 返回结果

- GET /collection：返回资源对象的列表（数组）
- GET /collection/resource：返回单个资源对象
- POST /collection：返回新生成的资源对象
- PUT /collection/resource：返回完整的资源对象
- PATCH /collection/resource：返回完整的资源对象
- DELETE /collection/resource：返回一个空文档

## 数据筛选和分页

API 可以允许在 URI 的查询字符串中传递筛选器，例如 `_/orders?minCost=n_`。 然后，Web API 负责分析和处理查询字符串中的 `minCost` 参数并在服务器端返回筛选后的结果。
```http
/orders?limit=25&offset=50
```


## URI格式规范
- **URI中尽量使用连字符"-"代替下划线"_"的使用**
- **URI中统一使用小写字母**
- **URI中不要包含文件(脚本)的扩展名**