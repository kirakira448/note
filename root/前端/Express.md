## MySql
### Node使用Express中的mysql连接mysql8失败
控制台报错, 最后几行内容为:
``` shell
  code: 'ER_NOT_SUPPORTED_AUTH_MODE',
  errno: 1251,
  sqlMessage: 'Client does not support authentication protocol requested by server; consider upgrading MySQL client',
  sqlState: '08004',
  fatal: true

```
### 报错原因
mysql8更换了新的密码验证方式, 我们的node客户端不支持新的验证方式
### 解决办法
#### 方法1: 将mysql密码验证降级
登录mysql,并运行一下代码, 务必`记得执行第二句`
```shell
mysql> alter user 'root'@'localhost' identified with mysql_native_password by '123456';
Query OK, 0 rows affected (0.27 sec)

mysql> flush privileges;
Query OK, 0 rows affected (0.08 sec)
```
#### 方法2: 使用新版mysql连接器
删除旧连接器, 使用新连接器. 项目的控制台输入:
```shell
npm un mysql && npm i mysql2
```
然后在js代码中修改引入文件为:
```js
// 导入myslq模块
const mysql = require('mysql2')
```

