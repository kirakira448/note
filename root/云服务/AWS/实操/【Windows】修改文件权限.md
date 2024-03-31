## 问题描述

windows下使用ssh连接EC2实例时，需要使用`.pem`密钥。
但是如果直接连接，会报警告
```shell
@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@
@         WARNING: UNPROTECTED PRIVATE KEY FILE!          @
@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@
Permissions for 'KANGSAA.pem' are too open.
It is required that your private key files are NOT accessible by others.
This private key will be ignored.
```

## 解决方法

1. 找到密钥文件所在目录，右键->属性
2. 安全->高级
![[修改文件权限_1.png]]

3. 删除原有权限
![[修改文件权限_2.png]]

4. 新增权限，选择完全控制
![[修改文件权限_3.png]]

5. 现在已经修改完毕，回到powershell中再次输入连接命令，可以连接成功。
