## 问题

使用`psycopg2`和`psycopg2-binary`出现报错
```text
ImportError: DLL load failed while importing _psycopg
```

## 原因

新版Python（>=3.7）不再支持`psycopg2`，需要使用`psycopg 3`
## 结论

使用`psycopg(the latest)`代替`psycopg2`

1. 卸载 psycopg2
```bash
pip uninstall psycopg2
```

2. 安装psycopg
 这将安装最新的 psycopg，现在是version 3
```bash
pip install psycopg
```

3. 修改代码
在你的 python 程序中
```python
import psycopg
```
***不要使用 `import psycopg2`***


## 示例代码

```python
import psycopg
import time

start_t = time.time()

# 连接到远程PostgreSQL数据库
conn = psycopg.connect(
    host = "192.168.3.21", #IP地址
    port = "5433",  #端口号
    dbname = "homepage",  #数据库名
    user = "postgres",  #用户名
    password = "123456"  #密码
)

cursor = conn.cursor()
sqlstr = "SELECT current_user;"
cursor.execute(sqlstr)

for row in cursor:
    user = row[0] 
    print(f'当前用户: {user}')

conn.commit()
cursor.close()
conn.close()

end_t = time.time()
print(f'程序成功执行，耗时{(end_t - start_t) / 60.0}分钟!')
```