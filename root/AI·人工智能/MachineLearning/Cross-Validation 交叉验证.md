# 定义
在交叉验证中，我们对不同的数据子集运行建模过程，以获得模型质量的多种度量。

例如：
将一个数据集拆成 5 份（A、B、C、D、E）。
实验：
	第一次实验中，A作为验证集，B~E作为训练集。
	第二次实验中，B作为验证集，A、C、D、E作为训练集。
	... ...
	重复使用所有数据集作为验证集。
# 代码
```python
# (estimator：估计器,X,y,cv=3:拆分为3组)
scores=cross_val_score(knn,X_train,y_train,cv=3)
score=np.mean(scores)
```
可以使用pipeline，因为pipeline中已经定义过了估计器
```python
from sklearn.model_selection import cross_val_score

# Multiply by -1 since sklearn calculates *negative* MAE
scores = -1 * cross_val_score(
						# 定义管道，输入值，输出值
						my_pipeline, X, y,
						# cv: 拆分份数(number of folds)						  
						cv=5,
						# 模型质量评估方法
						scoring='neg_mean_absolute_error')

print("MAE scores:\n", scores)
```
输出的 `scores`是一个列表
`MAE scores:
 \[301628.7893587  303164.4782723  287298.331666   236061.84754543
 260383.45111427\]  `
 
 我们通常需要单一的模型质量度量来比较替代模型。所以我们取实验的平均值。
```python
print("Average MAE score (across experiments):")
print(scores.mean())
```
`Average MAE score (across experiments):
277707.3795913405`

`