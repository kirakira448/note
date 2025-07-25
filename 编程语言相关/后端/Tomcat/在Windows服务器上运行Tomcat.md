如果想要远程控制tomcat，就不能使用`startup.bat`脚本，而必须使用`service.bat`注册为Windows服务，这样才能远程控制。

## 基本流程
### 1. 安装服务
在服务器上，进入tomcat的bin目录，打开cmd
运行命令：
```bash
service.bat install Tomcat8
```

安装完成后，可以运行命令查看服务是否存在
```bash
sc query Tomcat8
```

运行结果如下
```text
C:\Users\telema\install\apache-tomcat-8.5.99\bin>sc query Tomcat8

SERVICE_NAME: Tomcat8
        TYPE               : 10  WIN32_OWN_PROCESS
        STATE              : 1  STOPPED
        WIN32_EXIT_CODE    : 0  (0x0)
        SERVICE_EXIT_CODE  : 0  (0x0)
        CHECKPOINT         : 0x0
        WAIT_HINT          : 0x7d0
```


现在大概率无法启动

### 2. 修改服务权限

直接安装好的服务默认是用当前用户作为登录身份。
需要修改为本地系统账户。

#### 方法1：图形界面修改
1. `Win+R`输入`services.msc`
2. 找到`Apache Tomcat8.5 tomcat8`
3. 右键选择属性
4. 选择`登录`tab
5. 登录身份选择`本地系统账户`
6. `确定`
![[Pasted image 20250704155638.png]]
#### 方法2：命令行执行（未实际验证）

```bash
sc config Tomcat8 obj= LocalSystem
```

⚠️ 注意：

- `obj=`后面有一个空格！    
- `LocalSystem` 表示“本地系统账户”。

### 3. 启动服务
```bash
net start Tomcat8
```

可以使用命令检查8080端口是否有服务
```bash
netstat -ano | findstr :8080
```

正常结果如下：
```text
C:\Users\telema\install\apache-tomcat-8.5.99\bin>netstat -ano | findstr :8080
  TCP    0.0.0.0:8080           0.0.0.0:0              LISTENING       14852
  TCP    [::]:8080              [::]:0                 LISTENING       14852
```

>如果从外部访问不了，检查服务器的防火墙是否开放了8080端口