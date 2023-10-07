- 损失函数 J
  $$J(w,b) = \frac{1}{2m} \sum\limits_{i = 0}^{m-1} (f_{w,b}(x^{(i)}) - y^{(i)})^2 \tag{1}$$

where

  $$f_{w,b}(x^{(i)}) = wx^{(i)} + b \tag{2}$$
 
 - 梯度下降
 $$\begin{align*} \text{repeat}&\text{ until convergence:} \; \lbrace \newline
\;  w &= w -  \alpha \frac{\partial J(w,b)}{\partial w} \tag{3}  \; \newline
 b &= b -  \alpha \frac{\partial J(w,b)}{\partial b}  \newline \rbrace
\end{align*}$$
where, parameters $w$, $b$ are updated simultaneously.  
The gradient is defined as:

$$
\begin{align}
\frac{\partial J(w,b)}{\partial w}  &= \frac{1}{m} \sum\limits_{i = 0}^{m-1} (f_{w,b}(x^{(i)}) - y^{(i)})x^{(i)} \tag{4}\\
  \frac{\partial J(w,b)}{\partial b}  &= \frac{1}{m} \sum\limits_{i = 0}^{m-1} (f_{w,b}(x^{(i)}) - y^{(i)}) \tag{5}\\
\end{align}
$$
$\frac{\partial J(w,b)}{\partial w}$、$\frac{\partial J(w,b)}{\partial b}$：$w$、$b$ 的偏导数，注意，要同时更新；
$\alpha$：学习率，太小导致速度慢，太大不能正确下降。

#### 三种梯度下降法

> **两个小概念**：
> 
> - 轮次：epoch,训练数据集学习的轮数
> - 批次：batch,如果训练数据集较大，一轮要学习太多数据，那就把一轮次要学习的 数据分成多个批次，一批一批数据地学习

- 批量梯度下降法(Batch Gradient Descent,BGD)：每次迭代时（每次计算梯度）使用所有样本来进行梯度的更新。
    
- 随机梯度下降法(Stochastic Gradient Descent,SGD)：每次迭代的过程中，仅通过随机选择的一个样本计算梯度
    
- 小批量梯度下降法(Mini-Batch Gradient Descent,MBGD):对BGD和SGD进行了折中，    
    每次迭代时，抽取一部分(batch-size)训练样本，进行梯度的运算


代码：
定义函数
```python
def J(X_b,y,theta):
    try:

        return np.sum((X_b.dot(theta)-y)**2)/(2*len(y))
    except:
        return float('inf')

def dJ(X_b,y,theta):
    return X_b.T.dot(X_b.dot(theta) - y) / len(y)

# 批量梯度下降法

def BGD(X_b,y,initial_theta,eta=0.01,iters=1e4,epsilon=1e-4):
    theta=initial_theta
    curr_iter=1
    while curr_iter < iters:
        gradient=dJ(X_b,y,theta)
        last_theta=theta
        theta=theta-eta*gradient
        cost_value=J(X_b,y,theta)
        last_cost_value=J(X_b,y,last_theta)
        # 停止条件
        if abs(cost_value-last_cost_value)<epsilon:
            break
        curr_iter+=1
    return theta,cost_value     # 返回最佳theta和cost_value
```
使用
```python
X_b=np.hstack([np.ones((len(X_train_std),1)),X_train_std])
initial_theta=np.random.random(size=(X_b.shape[1]))

theta,cost_value=BGD(X_b,y_train,initial_theta)

X_b_test=np.hstack([np.ones((len(X_test_std),1)),X_test_std])
y_pre=X_b_test.dot(theta)
```
