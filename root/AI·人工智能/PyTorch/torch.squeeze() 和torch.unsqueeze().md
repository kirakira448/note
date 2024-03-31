
对数据维度操作的函数

定义一个用于演示的对象
```python
a=torch.randn(1,3)
print(a)
print(a.shape)
```
output:
```text
tensor([[ 0.7615, -0.8953, -1.9833]])
torch.Size([1, 3])
```

## torch.unsqueeze() 维度扩充

对数据维度进行扩充

给指定位置加上维数为一的维度。

```python
b=torch.unsqueeze(a,1)
print(b)
print(b.shape)
```
output:
```text
tensor([[[ 0.7615, -0.8953, -1.9833]]])
torch.Size([1, 1, 3])
```


## torch.squeeze() 维度压缩

对数据的维度进行压缩

去掉维数为1的的维度，不为1的维度没有影响。

```python
c=torch.squeeze(a)
print(c)
print(c.shape)
```
output:
```text
tensor([ 0.7615, -0.8953, -1.9833])
torch.Size([3])
```

