## 1. 配置`PlatformIO`

### 1.1. 安装

在扩展中搜索`PlatformIO`，安装扩展

![[Snipaste_2024-11-02_23-35-05.png]]

安装成功后会在扩展中看到`PlatformIO`的选项
![[Snipaste_2024-11-02_23-35-53.png]]

## 1.2. 驱动下载

进入`PlatformIO`主页，选择`Platforms`

![[Snipaste_2024-11-02_23-40-27.png]]

第一次进入时没有项目，选择 `create New Project`


![[Snipaste_2024-11-02_23-45-57.png]]
>- Name: 项目名
>- Board: 根据自己的板子选择版本，我的板子是`ESP-WROOM-32`,选择`Espressif ESP32 Dev Module`
>- Framework: 选择Arduino

取消勾选`Use default location`可以自定义存储位置

点击`Finish`开始下载并创建项目

## 2. 基本使用

### 2.1. 项目结构

创建完成后会生成初始项目文件
![[Snipaste_2024-11-03_00-07-09.png]]

#### 2.1.1. 基本代码结构
`src/main.cpp`
```cpp
void setup()
{
	// setup中编写需要在loop之前执行的逻辑
	// 例如配置信息、wifi连接等等
}

void loop()
{
	// 项目的逻辑代码
}
```
### 2.2. 编译项目

当完成了函数编写后，需要先编译项目

点击窗口下方的`√`标志
![[Snipaste_2024-11-03_00-14-04.png]]

### 2.3. 烧录编译文件

编译完成后，需要将编译文件上传至esp32

点击窗口下方的`→`标志
![[Snipaste_2024-11-03_00-16-06.png]]

