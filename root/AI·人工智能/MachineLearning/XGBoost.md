![[XGBoost.png]]

# 基本流程
## 1) 创建简单模型 naive model
```python
from xgboost import XGBRegressor

my_model = XGBRegressor()
my_model.fit(X_train, y_train)
```

## 2) 预测并评估模型 predictions and evaluate the model
```python
from sklearn.metrics import mean_absolute_error

predictions = my_model.predict(X_valid)
print("Mean Absolute Error: " + str(mean_absolute_error(predictions, y_valid)))
```

## 3) 参数调优 Parameter Tuning
### `n_estimators`
`n_estimators` 指定经历上述建模循环的次数。它等于我们包含在集成中的模型数量。
- 太低导致欠拟合
- 太高导致过拟合
一般取值范围：100~1000
```python
my_model = XGBRegressor(n_estimators=500)
my_model.fit(X_train, y_train)
```

### `early_stopping_rounds`
当验证分数停止提高时，这个参数会导致模型停止迭代，即使我们没有处于 `n_estimators` 的硬停止状态。
由于随机性有时会导致单轮验证分数没有提高，因此您需要指定一个数字，表示在停止之前允许进行多少轮直接恶化。
设置 `early_stopping_rounds=5` 是一个合理的选择。在这种情况下，我们在连续 5 轮验证分数恶化后停止。
```python
my_model = XGBRegressor(n_estimators=500)
my_model.fit(X_train, y_train, 
             early_stopping_rounds=5, 
             # 需要留出一些数据来计算验证分数
             eval_set=[(X_valid, y_valid)],
             verbose=False)
```

### `learning_rate`
每个模型的预测乘以一个较小的数（称为学习率），然后再添加它们。
一般来说，较小的学习率和大量的估计器将产生更准确的 XGBoost 模型，但模型的训练时间也会更长。
默认情况下，XGBoost 设置 `learning_rate=0.1` 。
```python
my_model = XGBRegressor(n_estimators=1000, learning_rate=0.05)
my_model.fit(X_train, y_train, 
             early_stopping_rounds=5, 
             eval_set=[(X_valid, y_valid)], 
             verbose=False)
```

### `n_jobs`
通常将参数 `n_jobs` 设置为等于计算机上的内核数。
用于提高计算性能，使用并行性来更快地构建模型，一般只用在较大的数据集上。
```python
my_model = XGBRegressor(n_estimators=1000, learning_rate=0.05, n_jobs=4)
my_model.fit(X_train, y_train, 
             early_stopping_rounds=5, 
             eval_set=[(X_valid, y_valid)], 
             verbose=False)
```