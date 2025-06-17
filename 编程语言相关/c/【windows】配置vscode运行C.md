
# 1. 配置运行环境 

## 1.1 下载安装MinGW-w64
[官网下载地址](https://sourceforge.net/projects/mingw-w64/)

![[Pasted image 20240508223651.png]]

选择下载`x86_64-win32-sjlj`

下载完成后解压到安装目录

## 1.2. 配置系统环境变量

将解压后的`/mingw64/bin`的路径添加到`系统环境变量Path`中

![[Pasted image 20240508224155.png]]


# 2. 配置VSCode

## 2.1. 安装扩展

在扩展中搜索`c`，安装`C/C++`
![[Pasted image 20240508224356.png]]

安装完成后，点击`设置`->`安装另一个版本..`
选择`1.8.4`版本
安装成功后重启vscode
![[Pasted image 20240508224516.png]]

>新版本的扩展不能自动生成`launch.json`文件，所以这里使用旧版本，方便运行和调试


# 3. 运行文件

## 3.1. 编写一个`.c`文件

`hello.c`
```c
#include <stdio.h>
#include <stdlib.h>
int main()
{
    printf("hello world!\n");
    printf("你好 世界!\n");
    system("pause");
    return 0;
}
```

## 3.2. 运行`.c`文件

点击`运行`->`启用调试`/`以非调试模式运行`（两种都可以）
![[Pasted image 20240508225015.png]]

这时会在当前目录下生成`.vscode/launch.json`文件
```json
{
    // 使用 IntelliSense 了解相关属性。 
    // 悬停以查看现有属性的描述。
    // 欲了解更多信息，请访问: https://go.microsoft.com/fwlink/?linkid=830387
    "version": "0.2.0",
    "configurations": [
        {
            "name": "gcc.exe - 生成和调试活动文件",
            "type": "cppdbg",
            "request": "launch",
            "program": "${fileDirname}\\${fileBasenameNoExtension}.exe",
            "args": [],
            "stopAtEntry": false,
            "cwd": "${fileDirname}",
            "environment": [],
            "externalConsole": false,
            "MIMode": "gdb",
            "miDebuggerPath": "D:\\01_install_dir\\mingw64\\bin\\gdb.exe",
            "setupCommands": [
                {
                    "description": "为 gdb 启用整齐打印",
                    "text": "-enable-pretty-printing",
                    "ignoreFailures": true
                },
                {
                    "description": "将反汇编风格设置为 Intel",
                    "text": "-gdb-set disassembly-flavor intel",
                    "ignoreFailures": true
                }
            ],
            "preLaunchTask": "C/C++: gcc.exe 生成活动文件"
        }
    ]
}
```

以及`task.json`文件
```json
{
    "tasks": [
        {
            "type": "cppbuild",
            "label": "C/C++: gcc.exe 生成活动文件",
            "command": "D:\\01_install_dir\\mingw64\\bin\\gcc.exe",
            "args": [
                "-fdiagnostics-color=always",
                "-g",
                "${file}",
                "-o",
                "${fileDirname}\\${fileBasenameNoExtension}.exe"
            ],
            "options": {
                "cwd": "${fileDirname}"
            },
            "problemMatcher": [
                "$gcc"
            ],
            "group": {
                "kind": "build",
                "isDefault": true
            },
            "detail": "调试器生成的任务。"
        }
    ],
    "version": "2.0.0"
}
```

>如果安装的是新版本的`C/C++`扩展，可能不会生成`launch.json`文件

# 4. 常用设定值

## 4.1. 让文件运行在一个弹出的控制台中

修改`launch.json`
```json
"configurations": [
	{
		...
		"externalConsole": false,
	}
]
```

## 4.2. 修复中文乱码

修改`task.json`
```json
"args": [
		...
		"-fexec-charset=GBK"
	],
```