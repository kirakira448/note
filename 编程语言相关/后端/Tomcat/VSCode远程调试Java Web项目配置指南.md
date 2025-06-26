
## 环境准备
- VSCode
- Java 8
- Tomcat 8.5.99
- 必要的VSCode扩展：
  - Extension Pack for Java
  - Tomcat for Java

## 配置步骤

### 1. VSCode配置
在项目根目录创建`.vscode/launch.json`文件，配置如下：
```json
{
    "version": "0.2.0",
    "configurations": [
        {
            "type": "java",
            "name": "Debug (Attach)",
            "request": "attach",
            "hostName": "localhost",
            "port": 8000,
            "timeout": 30000
        }
    ]
}
```

### 2. Tomcat调试配置
1. 进入Tomcat的bin目录：
```bash
cd C:\Users\kang\install\apache-tomcat-8.5.99\bin
```

2. 备份原始的catalina.bat文件：
```bash
copy catalina.bat catalina.bat.bak
```

3. 编辑catalina.bat文件，找到JAVA_OPTS的设置部分，添加调试参数：
```batch
set "JAVA_OPTS=%JAVA_OPTS% -Xdebug -Xrunjdwp:transport=dt_socket,address=8000,server=y,suspend=n"
```

4. 启动Tomcat：
```bash
startup.bat jpda start
```


### 3. 开始调试
1. 在VSCode中设置断点
2. 选择"Debug (Attach)"配置
3. 按F5开始调试

## 注意事项
1. 确保8000端口未被其他程序占用
2. 确保项目已正确部署到Tomcat
3. 如果调试连接失败，检查：
   - Tomcat是否正常运行
   - 8000端口是否成功开启
   - 防火墙设置是否允许该端口

## 常见问题解决
1. 如果端口被占用：
   - 修改`launch.json`中的端口号
   - 同时修改Tomcat启动参数中的端口号

2. 如果无法连接：
   - 检查Tomcat日志文件
   - 确认防火墙设置
   - 验证网络连接

## 调试技巧
1. 使用F5开始调试
2. 使用F10进行单步调试
3. 使用F11进入方法内部
4. 使用Shift+F11跳出当前方法
5. 使用Shift+F5停止调试

## 环境信息
- 操作系统：Windows 11
- Java版本：Java 8
- Tomcat版本：8.5.99
- Tomcat路径：C:\Users\kang\install\apache-tomcat-8.5.99
- 调试端口：8000
- 服务端口：8080

## 参数说明
启动Tomcat时，添加的参数如下：
```batch
set "JAVA_OPTS=%JAVA_OPTS% -Xdebug -Xrunjdwp:transport=dt_socket,address=8000,server=y,suspend=n"
```
1.JAVA_OPTS环境变量
- %JAVA_OPTS% 表示保留原有的JVM参数
- 通过set命令设置新的环境变量值

2.Xdebug
- 启用Java调试器
- 告诉JVM这是一个需要调试的应用程序

3.Xrunjdwp
- 启用Java调试线协议（Java Debug Wire Protocol）
- 这是Java调试器与JVM通信的协议

4.transport=dt_socket
- 指定调试器与JVM之间的通信方式
- dt_socket表示使用套接字（Socket）通信
- 这是最常用的通信方式，支持远程调试

5.address=8000
- 指定调试器监听的端口号
- 8000是默认的调试端口
- 可以根据需要修改为其他未被占用的端口

6.server=y
- 指定JVM作为调试服务器
- y表示JVM等待调试器连接
- 如果设置为n，则JVM会主动连接调试器

7.suspend=n
- 控制JVM启动时是否暂停等待调试器连接
- n表示不暂停，JVM会立即启动
- 如果设置为y，则JVM会暂停直到调试器连接

### 参数组合的效果
- 当这些参数组合在一起时，会创建一个调试服务器
- 服务器在8000端口监听调试器的连接
- 应用程序会正常启动，不会暂停
- 调试器（VSCode）可以随时连接到这个端口进行调试