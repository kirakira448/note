解决多分类问题
公式：
$$
p_l=\frac{e^{z_l}}{\sum_{j=1}^ke^{z_j}}
$$

代码实现：
```python
# 创建softmax回归对象
# sklearn中没有对softmax的直接实现，可以用逻辑回归实现
sm=LogisticRegression(multi_class='multinomial')
```