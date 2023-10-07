解决过拟合问题
### 定义
公式：
The equation for the cost function regularized linear regression is:

$$J(\mathbf{w},b) = \frac{1}{2m} \sum\limits_{i = 0}^{m-1} (f_{\mathbf{w},b}(\mathbf{x}^{(i)}) - y^{(i)})^2  + \frac{\lambda}{2m}  \sum_{j=0}^{n-1} w_j^2 \tag{1}$$

where:

$$ f_{\mathbf{w},b}(\mathbf{x}^{(i)}) = \mathbf{w} \cdot \mathbf{x}^{(i)} + b  \tag{2} $$

正则惩罚项为：
$$
\frac{\lambda}{2m}  \sum_{j=0}^{n-1} w_j^2 \tag{3}
$$
$\lambda$：正则化参数


### 梯度下降中使用正则化
$$\begin{align*}
&\text{repeat until convergence:} \; \lbrace \\
&  \; \; \;w_j = w_j -  \alpha \frac{\partial J(\mathbf{w},b)}{\partial w_j} \tag{4}  \; & \text{for j := 0..n-1} \\
&  \; \; \;  \; \;b = b -  \alpha \frac{\partial J(\mathbf{w},b)}{\partial b} \\
&\rbrace
\end{align*}$$

$$\begin{align*}

\frac{\partial J(\mathbf{w},b)}{\partial w_j}  &= \frac{1}{m} \sum\limits_{i = 0}^{m-1} (f_{\mathbf{w},b}(\mathbf{x}^{(i)}) - y^{(i)})x_{j}^{(i)}  +  \frac{\lambda}{m} w_j \tag{5} \\

\frac{\partial J(\mathbf{w},b)}{\partial b}  &= \frac{1}{m} \sum\limits_{i = 0}^{m-1} (f_{\mathbf{w},b}(\mathbf{x}^{(i)}) - y^{(i)}) \tag{6}

\end{align*}$$
当对$w_j$求偏导后，成本函数转化为公式(5)。
注意，因为是偏导数，正则惩罚项只留下$w_j$，其他$w$被消去。
为了寻找$min(J_{(w,b)})$，$w_j$每次更新减去$\frac{\partial J(\mathbf{w},b)}{\partial w_j}$，所以过大的特征($x_j$)的参数($w_j$)将被减小到约等于0。
>说明:
>如果$x_j$很大或为高次幂，将导致$w_j^2$的系数很大，例如10000。
>$x_j$很大导致$loss(w,b)$变大，进而导致$w_j$减小的更快。
>最终$w_j$减小为一个接近0的值，消除$x_j$的影响，解决过拟合问题。

### 范数、L1正则化与L2正则化

- 范数    
    假设x是一个向量，它的Lp范数定义
    $$
  ||x||_p=(\sum_i|x_i|^p)^{\frac{1}{p}}  
  $$
  - L1正则惩罚项：对应于L1范数
$$
  ||w||_1=\sum_i|w_i| 
$$
  - L2正则惩罚项：对应于L2范数的平方
$$
  ||w||_2^2=\sum_{i}w_i^2
$$

### 岭回归与Lasso回归的形式
- 线性回归的损失函数
$$
J(\mathbf{w},b) = \frac{1}{2m} \sum\limits_{i = 0}^{m-1} (f_{\mathbf{w},b}(\mathbf{x}^{(i)}) - y^{(i)})^2
$$
- 岭回归的损失函数
$$
J(\mathbf{w},b) = \frac{1}{2m} \sum\limits_{i = 0}^{m-1} (f_{\mathbf{w},b}(\mathbf{x}^{(i)}) - y^{(i)})^2  + \frac{\lambda}{2m}  \sum_{j=0}^{n-1} w_j^2 
$$
- Lasso回归的损失函数
$$
J(\mathbf{w},b) = \frac{1}{2m} \sum\limits_{i = 0}^{m-1} (f_{\mathbf{w},b}(\mathbf{x}^{(i)}) - y^{(i)})^2  + \frac{\lambda}{2m}  \sum_{j=0}^{n-1} |w_j| 
$$

#### 代码实现
##### 岭回归
sklearn中使用sklearn.linear_model.Ridge实现岭回归
可以使用Pipeline管道机制将岭回归封装到操作中
```python
def ridge_regression(degree,alpha):
	return Pipeline([
		("poly",PolynomialFeatures(degree=degree)),
		("std",StandardScaler()),
		("ridge",Ridge(alpha=alpha)) # 岭回归使用Ridge实现
	])

```

##### LASSO回归
sklearn中使用sklearn.linear_model.Lasso实现Lasso回归
可以使用Pipeline管道机制将岭回归封装到操作中
```python
def LassoRegression(degree, alpha):
  return Pipeline([
     ("poly", PolynomialFeatures(degree=degree)),
     ("std_scaler", StandardScaler()),
     ("lasso_reg", Lasso(alpha=alpha)) # Lasso回归使用Lasso实现
   ])

```





