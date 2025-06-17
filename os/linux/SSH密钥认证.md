## 1. 本机生成密钥
```bash
ssh-keygen -t rsa
```

你将被要求指定文件名和存储路径，通常默认存储在 `~/.ssh/id_rsa`。按回车键使用默认路径，接着可以选择是否为私钥设置密码短语（为了更安全的连接，可以设置，但也可以留空）。

## 2. 将公钥复制到服务器
### Linux
```bash
ssh-copy-id username@server_ip
```

- `username`：要登录的服务器用户名
- `server_ip`：目标服务器的IP地址

你将被提示输入密码，一次性输入后，公钥将被添加到服务器的 `~/.ssh/authorized_keys` 文件中。
### Windows

在Windows上使用PowerShell时，`ssh-copy-id` 命令不可用，但你可以手动完成将SSH公钥上传到Linux服务器的过程。

1. 在PowerShell中，执行以下命令，查看生成的公钥内容：
```bash
cat ~/.ssh/id_rsa.pub
```

2. 复制输出的内容，它是你的公钥（通常以 `ssh-rsa` 开头）。
3. 使用SSH登录到你的Linux服务器：
```bash
ssh username@server_ip
```

4. 在服务器上，手动创建 `.ssh` 目录（如果还不存在）并设置正确的权限：
```bash
mkdir -p ~/.ssh
chmod 700 ~/.ssh
```

5. 使用文本编辑器如 `nano` 或 `vi`，在Linux服务器上将公钥粘贴到 `authorized_keys` 文件中：
```bash
nano ~/.ssh/authorized_keys
```

6. 将你在本地复制的公钥内容粘贴进去，保存并退出。
7. 设置 `authorized_keys` 文件的权限：
```bash
chmod 600 ~/.ssh/authorized_keys
```

## 3. 测试无密码登录

```bash
ssh username@server_ip
```



## 【可选】Windows增加快捷方式

```bat
@echo off
start powershell ssh kang@10.177.1.130
```