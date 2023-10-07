*Amazon Elastic Compute Cloud*
# 基本介绍
## 功能
云计算服务。
在云端提供安全、可调整大小的运算容量。
可以使用 Amazon EC2 的简易的Web界面来轻松获取和设定容量。
>可解决预测前期需求问题。
>在设定架构时，不必事先知道需要多少运算容量或需要多少磁盘容量。
>可根据需求来扩充或所见规模。

## 优势
- 快速构建EC2执行个体。提供选项选取合适的CPU、存储和操作系统，以满足特定需求。
- 可以变更磁盘大小和执行个体类型，而不必终止执行个体。
- 可以扩充或缩减规模，以符合季节性需求。

## 如何使用 EC2 构建云端解决方案
![[imgs/Pasted image 20230810140905.png]]
>在公有子网中使用安全群组，建立执行个体托管网站。
>在私有子网中建立另一个执行个体过关数据库。

# 使用
## 基本流程
### 1.名称和标签
标签是您为 AWS 资源分配的标记。
每个标签都包含一个键和一个可选值，两者均由您定义。

优势：筛选、自动化、成本分配和存取控制。
### 2.Amazon Machine Image 应用程序和操作系统映像
AMI 是一种模板，其中包含了启动实例所需的软件配置(操作系统、应用程序服务器和应用程序)。
### 3.实例类型
选择满足您的计算、内存、网络或存储需要的实例类型。
实例类型决定了：CPU、RAM、磁盘空间与类型、网络性能

>**t3.large**
>t：系列名称
>3：第几代
>large：实例大小
### 4.密钥对（登录）
要在启动模板中指定密钥对，您可以选择**密钥对名称**字段中的密钥对。
在启动实例之前，请确保您有权访问所选密钥对。

密钥对由以下组成：
- AWS 存储的公有密钥
- 个人存储的私有密钥
### 5.网络设置
#### 区域
区域由控制台决定，不能在 EC2 中修改。

#### VPC 和 子网
每个 AWS 区域 都有预设的 VPC。
预设的 VPC 在当前区域的每个可用区（AZ）都有公有子网。

#### 公有 IP
可以从互联网访问的IP地址。
用于在实例和公网之间的通讯。

#### 防火墙（安全组）
安全组是一组负责为您的实例控制流量的防火墙规则。添加规则，以允许特定流量到达您的实例。

### 6.配置存储
使用 [[EBS]]作为存储模块。
- 像外接式硬盘一样工作
- 低延迟
- 能处理几乎任何运算需求
### 7.高级详细信息


## Windows 使用 PowerShell 连接 EC2 
win10 以上版本可以在 cmd 或 PowerShell 使用 ssh
### 1. 检查保存在本地的`.pem`密钥文件
### 2. 在 PowerShell 中执行命令
`ssh -i 文件地址 ec2-user@公网ip`
例如：`ssh -i G:\perpetual_files\EC2Tutorial.pem ec2-user@184.72.142.43`
### 3. 有可能会出现警告
```shell
@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@
@         WARNING: UNPROTECTED PRIVATE KEY FILE!          @
@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@
Permissions for 'G:\\perpetual_files\\EC2Tutorial.pem' are too open.
It is required that your private key files are NOT accessible by others.
This private key will be ignored.
Load key "G:\\perpetual_files\\EC2Tutorial.pem": bad permissions
ec2-user@184.72.142.43: Permission denied (publickey,gssapi-keyex,gssapi-with-mic).
```
### 4. 解决方法：
[真正解决 windows OpenSSH WARNING: UNPROTECTED PRIVATE KEY FILE!](https://blog.csdn.net/joshua2011/article/details/90208741)
1) 非常重要的一步：
在得到当前用户名（就如同在linux运行 id 命令一样）
在PowerShell 运行如下命令
```shell
PS C:\vm\share_vm> $env:username
EduPlus        <------ 记住这个当前用户名，下面步骤要用到
```
PS C:\vm\share_vm> $env:username
EduPlus        <------ 记住这个当前用户名，下面步骤要用到
2) 右键这个 私钥文件，选择
【属性】--> 【安全】--> 【高级】
3) 更改当前所有者。
4) 输入第一步查询到的用户名，【检查名称】--> 【确定】
5) 删除权限条目中的其他主体
6) 如果没有当前用户，点击添加，输入第一步查询到的用户名，【检查名称】--> 【确定】
7) 给予完全控制权限。
8) 确定。

