### 1) 删除分类变量
只有当分类变量不包含有用信息时才这么做。
```python
# exclude=['object'] 表示排除'object'类型的列，即删除分类变量
drop_X_train = X_train.select_dtypes(exclude=['object'])
```

### 2) 序数编码 ### Ordinal Encoding
序数编码将每个唯一值分配给不同的整数。
![[Ordinal_Encoding.png]]
```python
from sklearn.preprocessing import OrdinalEncoder

# Get list of categorical variables
# s = (X_train.dtypes == 'object')
# object_cols = list(s[s].index)

# Make copy to avoid changing original data 
# label_X_train = X_train.copy()
# label_X_valid = X_valid.copy()

# Apply ordinal encoder to each column with categorical data
ordinal_encoder = OrdinalEncoder()
label_X_train[object_cols] = ordinal_encoder.fit_transform(X_train[object_cols])
label_X_valid[object_cols] = ordinal_encoder.transform(X_valid[object_cols])
```
当训练集和验证集中的分类不是完全相同时，需要预处理(删除有问题的列)
```python
# Categorical columns in the training data
object_cols = [col for col in X_train.columns if X_train[col].dtype == "object"]

# Columns that can be safely ordinal encoded
good_label_cols = [col for col in object_cols if 
                   set(X_valid[col]).issubset(set(X_train[col]))]
        
# Problematic columns that will be dropped from the dataset
bad_label_cols = list(set(object_cols)-set(good_label_cols))

# Drop categorical columns that will not be encoded
label_X_train = X_train.drop(bad_label_cols, axis=1)
label_X_valid = X_valid.drop(bad_label_cols, axis=1)

```
**注意：**使用序数编码需要保证变量有明确的排序
例如，"Never" (0) < "Rarely" (1) < "Most days" (2) < "Every day" (3).
### 3) 单热编码 One-Hot Encoding
One-hot 编码创建新列，使用0、1来表示原数据中的值是否存在
![[one_hot.png]]
```python
from sklearn.preprocessing import OneHotEncoder

# Get list of categorical variables
# s = (X_train.dtypes == 'object')
# object_cols = list(s[s].index)

# Apply one-hot encoder to each column with categorical data
# handle_unknown='ignore' : 避免报错：验证集(valid) 中出现 训练集（train）里没有的分类会报错
# sparse=False ： 确保编码列作为 numpy 数组（而不是稀疏矩阵sparse matrix）返回。
OH_encoder = OneHotEncoder(handle_unknown='ignore', sparse=False)
OH_cols_train = pd.DataFrame(OH_encoder.fit_transform(X_train[object_cols]))
OH_cols_valid = pd.DataFrame(OH_encoder.transform(X_valid[object_cols]))

# One-hot encoding removed index; put it back
OH_cols_train.index = X_train.index
OH_cols_valid.index = X_valid.index

# Remove categorical columns (will replace with one-hot encoding)
num_X_train = X_train.drop(object_cols, axis=1)
num_X_valid = X_valid.drop(object_cols, axis=1)

# Add one-hot encoded columns to numerical features
OH_X_train = pd.concat([num_X_train, OH_cols_train], axis=1)
OH_X_valid = pd.concat([num_X_valid, OH_cols_valid], axis=1)

# Ensure all columns have string type
OH_X_train.columns = OH_X_train.columns.astype(str)
OH_X_valid.columns = OH_X_valid.columns.astype(str)
```
one-hot 编码不假设类别的顺序。
因此，如果分类数据没有明确的顺序，可以使用这种方法。


