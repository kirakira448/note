### - 首先下载Miniconda安装脚本：

```bash
wget https://repo.anaconda.com/miniconda/Miniconda3-latest-Linux-x86_64.sh
```

- 运行安装脚本：
```bash
bash Miniconda3-latest-Linux-x86_64.sh
```


### 安装过程中：

- 按回车阅读许可

- 输入"yes"同意许可条款

- 确认安装位置（默认是home目录下）

- 当问到是否初始化Miniconda3时，输入"yes"

### 如果选择了`no`
安装完成后出现提示：
```text
You have chosen to not have conda modify your shell scripts at all.
To activate conda's base environment in your current shell session:

eval "$(/root/miniconda3/bin/conda shell.YOUR_SHELL_NAME hook)"

To install conda's shell functions for easier access, first activate, then:

conda init

Thank you for installing Miniconda3!
```

#### 使用以下步骤完成配置
路径和提示的一致
```bash
eval "$(/root/miniconda3/bin/conda shell.bash hook)"
```

初始化conda
```bash
conda init
```

### 重新加载配置
- 使更改生效：
```bash
source ~/.bashrc
```

- 验证安装：
```bash
conda --version
```

- 创建一个Python 3.9的环境：
```bash
# 创建名为 py39 的环境，指定Python版本为3.9
conda create -n py39 python=3.9

# 激活环境
conda activate py39

# 验证Python版本
python --version
```



常用的conda命令：
```bash
# 列出所有环境
conda env list

# 激活环境
conda activate 环境名称

# 退出当前环境
conda deactivate

# 删除指定环境
conda remove --name 环境名称 --all

# 安装包
conda install 包名

# 更新conda
conda update conda
```



提示：

- 如果您使用的是zsh而不是bash，需要在`~/.zshrc`中初始化conda

- 建议在安装完成后运行`conda config --set auto_activate_base false`，这样可以避免自动激活base环境

- 如果需要，您可以使用`conda install pip`在conda环境中安装pip

需要我详细解释任何步骤吗？