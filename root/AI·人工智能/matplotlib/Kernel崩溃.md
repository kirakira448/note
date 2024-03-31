## 解决办法

在plt代码块之前添加以下代码
```python
import os
# 解决subplots报错
os.environ["KMP_DUPLICATE_LIB_OK"]="TRUE"

```