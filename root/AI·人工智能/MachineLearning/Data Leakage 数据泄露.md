数据泄露会导致模型看起来很准确，但无法用于实际预测。
泄漏主要有两种类型：目标泄漏(**target leakage**)和训练测试污染(**train-test contamination**)。

### Target leakage
与目标值相关的特征被包含在训练集中。

例如：

|got_pneumonia|age|weight|male|took_antibiotic_medicine|...|
|---|---|---|---|---|---|
|False|65|100|False|False|...|
|False|72|130|True|False|...|
|True|58|100|False|True|...|

注意，表中`got_pneumonia`代表是否患肺炎，`took_antibiotic_medicine`代表是否服用抗生素药物。
人们在患肺炎后服用抗生素药物才能康复。
所以，原始数据显示这些列之间存在很强的关系，这就是目标泄漏。

为了防止这种类型的数据泄漏，应**排除在实现目标值后更新（或创建）的任何变量**。

### Train-Test Contamination
当我们不知不觉地或巧妙地将信息从训练数据集传递到验证数据集时，就会发生这种情况。
即训练集拥有了验证集的部分信息。
例如：
```python
# 错误代码！
X_valid = imputer.fit_transform(X_valid)
```

我们不应该在验证集上调用 fit_transform 方法，而只能在训练数据集上调用。
```python
# 正确写法
X_train = imputer.fit_transform(X_train)  
X_valid = imputer.transform(X_valid)
```