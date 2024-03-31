## 1. 查看自己显卡支持的cuda版本

cmd中输入命令
```shell
nvidia-smi
```
![[Snipaste_2024-01-28_15-30-17.png]]
这里显示我的显卡最高支持12.1版本

## 2. 进入PyTorch官网查看版本

[PyTorch](https://pytorch.org/get-started/locally/)
![[Snipaste_2024-01-28_15-33-45.png]]
当前PyTorch支持到12.1版本

>注意：
>当`本机显卡支持的版本 > PyTorch支持版本` 时，以PyTorch的版本为准


## 3. 下载cuda

去Nvidia官网下载对应版本
[cuda12.1](https://developer.nvidia.com/cuda-12-1-0-download-archive)

双击exe程序安装，全部选下一步。


## 4. 安装PyTorch

打开cmd，[[虚拟环境#激活 | 进入conda环境]]，运行[PyTorch官网](https://pytorch.org/get-started/locally/)生成的命令。
```shell
pip3 install torch torchvision torchaudio --index-url https://download.pytorch.org/whl/cu121
```

## 5. 验证torch版本

打开cmd，进入python
```shell
python
```

输入以下命令：

```python
>>> import torch
>>> print(torch.cuda.is_available())
```
如果返回值为True，则安装成功

退出python：
```python
>>> exit()
```