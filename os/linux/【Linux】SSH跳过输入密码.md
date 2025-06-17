# 1. 安装 Git for Windows

首先，确保你已经安装了 Git for Windows，它不仅包含 Git 命令，还带有 Git Bash 终端，可以用于 SSH 操作。

- 下载 Git for Windows：[https://gitforwindows.org/](https://gitforwindows.org/)
- 安装完成后，打开 **Git Bash** 终端。

# 2. 生成 SSH 密钥

1. **打开 Git Bash**，然后输入以下命令来生成 SSH 密钥：
```bash
ssh-keygen -t rsa -b 4096
```

2. Git Bash 会提示你选择保存密钥的位置，通常默认保存在 `~/.ssh/id_rsa`：
```bash
Enter file in which to save the key (/c/Users/YourUsername/.ssh/id_rsa):
```
- 按回车键以使用默认位置。

3. 接着，它会询问是否设置密码短语（passphrase）。如果你希望为密钥增加额外的安全性，可以设置密码短语，否则直接按回车跳过：
```bash
Enter passphrase (empty for no passphrase):
```

4. 生成完成后，会输出如下信息：
```bash
Your identification has been saved in /c/Users/YourUsername/.ssh/id_rsa.
Your public key has been saved in /c/Users/YourUsername/.ssh/id_rsa.pub.
```


# 3. 将公钥上传到远程服务器

1. **使用 `ssh-copy-id` 命令将公钥上传到远程服务器**，在 Git Bash 中运行以下命令：
```bash
ssh-copy-id your-username@remote-server-ip
```
- `your-username` 是你在远程服务器上的用户名。
- `remote-server-ip` 是远程服务器的 IP 地址或域名。

2. 系统会提示你输入远程服务器的密码：
```bash
your-username@remote-server-ip's password:
```

3. 成功输入密码后，公钥会被复制到远程服务器，并显示如下消息：
```bash
Number of key(s) added: 1
Now try logging into the machine, with: "ssh 'your-username@remote-server-ip'"
```

# 4. 测试 SSH 密钥登录

1. 现在，你可以使用 SSH 密钥登录远程服务器，无需再输入密码。在 Git Bash 中运行以下命令：
```bash
ssh your-username@remote-server-ip
```

2. 如果公钥设置正确，你应该能够直接登录到远程服务器，而不需要输入密码。