## 检查能否使用GPU

```python
import torch

print(torch.__version__)
print(torch.cuda.is_available())
print(torch.version.cuda)
```

## 使用GPU

```python 
device = torch.device("cuda:0" if torch.cuda.is_available() else "cpu") #数字切换卡号
model.to(device)
data.to(device)
```

