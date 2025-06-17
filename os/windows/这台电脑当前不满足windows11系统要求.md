### 修改注册表
1. 在安装页面按下`Shift+F10` 打开命令行界面
2. 输入`regedit`打开注册表
3. 定位到注册表位置
```text
HKEY_LOCAL_MACHINE\SYSTEM\Setup
```

4. **创建一个名为“LabConfig”的项，接着在“LabConfig”下创建两个 DWORD 值：**
	a. 键为`BypassTPMCheck`，值为`00000001`
	b. 键为`BypassSecureBootCheck`，值为`00000001`

5. 保存退出，重新选择安装