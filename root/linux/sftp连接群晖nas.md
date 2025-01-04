## 结论

`remotePath`不是从`/var`开始的
配置文件如下
`sftp.json`
```json
{
    "name": "NAS Service",
    "host": "yourHost",
    "protocol": "sftp",
    "port": 22,
    "username": "yourUsername",
    "password": "yourPassword",
    "remotePath": "/从共享文件夹起始"
}

```

例如，我想连接这个路径
```text
/var/services/web/service/homepage
```

直接连接会提示`Permission Denied`

正确的做法是使用
```text
/web/service/homepage/front
```

这里我的`/web`是一个共享文件夹，所以才有权限访问。
如果还不能访问，请检查：
1. 当前用户的访问权限
2. 当前路径的访问权限


## 解决过程

### 1. 连接失败
我想使用vscode插件sftp连接我的nas，来快速同步文件
我通过ssh连接确认我的路径没有问题
![[Snipaste_2024-12-31_00-16-31.png]]

但是当我在vscode中尝试上传时，总遇到`Permission Denied`报错
当前`sftp.json`配置如下
```json
{
    "name": "NAS Service",
    "host": "192.168.3.21",
    "protocol": "sftp",
    "port": 22,
    "username": "kyj",
    "password": "******",
    "remotePath": "/var/services/web/service/homepage",
    "uploadOnSave": false,
    "ignore": [
        "**/.vscode/**",
        "**/.git/**",
        "**/.DS_Store",
        "**/__pycache__/**",
        "**/*.pyc",
        "**/venv/**",
        "**/output/**"
    ]
}

```

### 2. 使用FileZilla

我尝试直接使用`FileZilla`连接，可以正常上传文件。
说明我的基础配置都正确，并且权限也正常，可能是文件路径有问题。

检查`FileZilla`连接的路径
![[Snipaste_2024-12-31_00-21-26.png]]

发现路径并不是从`/var`开始的，而是使用共享文件夹作为起始。

### 3. 修改配置文件

将配置文件修改为新的路径
```json
{
    "name": "NAS Service",
    "host": "192.168.3.21",
    "protocol": "sftp",
    "port": 22,
    "username": "kyj",
    "password": "******",
    "remotePath": "/web/service/homepage/server",
    "uploadOnSave": false,
    "ignore": [
        "**/.vscode/**",
        "**/.git/**",
        "**/.DS_Store",
        "**/__pycache__/**",
        "**/*.pyc",
        "**/venv/**",
        "**/output/**"
    ]
}

```

现在可以正常连接，正常上传了