---
tags:
  - Linux
  - PostgreSQL
---

以`Ubuntu`为例

## 安装postgres(16版本)
```bash
sh -c 'echo "deb http://apt.postgresql.org/pub/repos/apt $(lsb_release -cs)-pgdg main" > /etc/apt/sources.list.d/pgdg.list'
```

```bash
curl -fsSL https://www.postgresql.org/media/keys/ACCC4CF8.asc | sudo gpg --dearmor -o /etc/apt/trusted.gpg.d/postgresql.gpg
```

```bash
apt update
apt install postgresql-16 postgresql-contrib-16

systemctl start postgresql.service
systemctl enable postgresql.service
```

## postgres 初期设置

### 修改`listen_addresses`

打开配置文件
```bash
nano /etc/postgresql/16/main/postgresql.conf
```

`ctrl+w`搜索`listen_addresses`
未修改前：
```conf
#listen_addresses = 'localhost'
```
修改为：
```conf
listen_addresses = '*'
```

### 检查port

`ctrl+w`搜索`port`
可以查看或修改port
```conf
port=5432
```


### 配置host

打开配置文件
```
nano /etc/postgresql/16/main/pg_hba.conf
```

在最后追加内容
```conf
host    all             all             0.0.0.0/0               md5
```


### 重启服务

所有配置完成后，重启服务
```
systemctl restart postgresql.service
```

### 修改用户postgres 的 password
```
sudo -u postgres psql
ALTER USER postgres WITH PASSWORD 'your_password';
```

>默认postgres用户是通过`peer`协议验证，没有密码
>Navicat等工具必须通过密码验证连接
