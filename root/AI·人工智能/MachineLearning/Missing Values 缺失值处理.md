数据集会因为各种原因出现缺失值，如果不进行处理，会导致大多数机器学习库（如`scikit-learn`）报错。
# 三种方法
## 1) 删除缺失值的列
只有在`被删除列`中缺失大量信息时，才建议使用。
![[Drop Columns with Missing Values.png]]
```python
# 直接删除
# data=data.dropna(axis=1)


# 要 同时删除 训练集与验证集中相同列的情况
# Get names of columns with missing values
cols_with_missing = [col for col in X_train.columns
                     if X_train[col].isnull().any()]
# Drop columns in training and validation data
reduced_X_train = X_train.drop(cols_with_missing, axis=1)
reduced_X_valid = X_valid.drop(cols_with_missing, axis=1)
```
## 2) 插补
插补：用数字填补缺失值。例如，当前列的平均值。
![[Imputation.png]]
```python
from sklearn.impute import SimpleImputer

# Imputation
my_imputer = SimpleImputer()
imputed_X_train = pd.DataFrame(my_imputer.fit_transform(X_train))
imputed_X_valid = pd.DataFrame(my_imputer.transform(X_valid))

# Imputation removed column names; put them back
imputed_X_train.columns = X_train.columns
imputed_X_valid.columns = X_valid.columns
```
使用`插补`的方法，对比`删除缺失值的列`，通常能够生成更准确的模型。

## 3) 插补扩展
`插补`估算值可能系统地高于或低于其实际值（未在数据集中收集）。
或者，具有缺失值的行可能以其他方式是唯一的。
在这种情况下，您的模型将通过考虑最初丢失的值来做出更好的预测。
![[An Extension To Imputation.png]]
```python
# cols_with_missing = [col for col in X_train.columns
#                      if X_train[col].isnull().any()]

# Make new columns indicating what will be imputed
for col in cols_with_missing:
    X_train_plus[col + '_was_missing'] = X_train_plus[col].isnull()
    X_valid_plus[col + '_was_missing'] = X_valid_plus[col].isnull()

# Imputation
my_imputer = SimpleImputer()
imputed_X_train_plus = pd.DataFrame(my_imputer.fit_transform(X_train_plus))
imputed_X_valid_plus = pd.DataFrame(my_imputer.transform(X_valid_plus))

# Imputation removed column names; put them back
imputed_X_train_plus.columns = X_train_plus.columns
imputed_X_valid_plus.columns = X_valid_plus.columns
```
在这种方法中，我们像以前一样估算缺失值。
此外，对于原始数据集中缺少条目的每一列，我们添加一个新列来显示估算条目的位置。