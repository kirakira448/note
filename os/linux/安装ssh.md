## 1. 确认SSH是否已安装

```bash
which sshd
```
如果没有输出，说明SSH服务未安装。



## 2. 安装SSH服务

Ubuntu/Debian 系列:
```bash
sudo apt update
sudo apt install openssh-server
```



## 3. 启动SSH服务

安装后启动SSH服务：

- **启动服务**:
```bash
sudo systemctl start ssh
```

- **设置开机自启**:
```bash
sudo systemctl enable ssh
```


## **4. 检查SSH服务状态**

确保服务正常运行：
```bash
sudo systemctl status ssh
```

## **5. 测试连接**

从客户端尝试连接目标主机：
```bash
ssh username@host
```
