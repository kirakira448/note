# Regression 回归
从无限多的可能输出数字中预测数字
例：根据面积与总价的关系预测房价
## Linear regression 线性回归模型

### 公式
>$$f_w,_b(x)=wx+b $$
>w:斜率
>b:截距
### Cost function 成本函数
用于描述拟合直线的误差值
平方误差成本函数
>$$ J(w,b)=\frac{1}{2m}\sum_{i=1}^m(\hat{y}^{(i)}-y^{(i)})^{2} $$
>m:训练集数量
>可以将y帽转换为下面的形式
>$$ j(w,b)=\frac{1}{2m}\sum_{i=1}^m(f_w,_b(x^{(i)})-y^{(i)})^{2} $$

### Gradient descent 梯度下降
#### 公式

>$$\begin{align*} \text{repeat}&\text{ until convergence:} \; \lbrace \newline

\;  w &= w -  \alpha \frac{\partial J(w,b)}{\partial w} \tag{3}  \; \newline

 b &= b -  \alpha \frac{\partial J(w,b)}{\partial b}  \newline \rbrace

\end{align*}$$
>$$\alpha:学习率$$
$$\frac{\partial J(w,b)}{\partial b}:当前点，在J(w)上的斜率$$:
目的：使J(w,b)取最小值。通过这个公式，可以让w和b总是取能够使J(w,b)减小的值

The gradient is defined as:

$$

\begin{align}

\frac{\partial J(w,b)}{\partial w}  &= \frac{1}{m} \sum\limits_{i = 0}^{m-1} (f_{w,b}(x^{(i)}) - y^{(i)})x^{(i)} \tag{4}\\

  \frac{\partial J(w,b)}{\partial b}  &= \frac{1}{m} \sum\limits_{i = 0}^{m-1} (f_{w,b}(x^{(i)}) - y^{(i)}) \tag{5}\\

\end{align}

$$

# Classification 分类
对一个类型进行预测，所有可能的输出都是一个小组
例：根据图片特征预测是猫还是狗