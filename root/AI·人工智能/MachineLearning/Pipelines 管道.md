用于打包 数据预处理、建模 等操作。
使用管道可以简化代码。

### 1) 定义预处理步骤
```python
from sklearn.compose import ColumnTransformer
from sklearn.pipeline import Pipeline
from sklearn.impute import SimpleImputer
from sklearn.preprocessing import OneHotEncoder

# Preprocessing for numerical data
# 数值类型数据的缺失值处理，strategy根据实际情况选择
numerical_transformer = SimpleImputer(strategy='constant')

# Preprocessing for categorical data
# 注意 steps 要有先后顺序
categorical_transformer = Pipeline(steps=[
	# 分类变量的缺失值处理，strategy根据实际情况选择
	# (name, transform)
    ('imputer', SimpleImputer(strategy='most_frequent')),
    # one-hot编码
    ('onehot', OneHotEncoder(handle_unknown='ignore'))
])

# Bundle preprocessing for numerical and categorical data
preprocessor = ColumnTransformer(
	# transformer objects 将要应用的 subset
    transformers=[
	    # (name:自定义，可用于标识,transformer:前面定义的transformer,columns:将要应用的数据列)
        ('num', numerical_transformer, numerical_cols),
        ('cat', categorical_transformer, categorical_cols)
    ])
```

### 2) 定义模型
```python
from sklearn.ensemble import RandomForestRegressor

model = RandomForestRegressor(n_estimators=100, random_state=0)
```

### 3) 创建并评估管道
```python
from sklearn.metrics import mean_absolute_error

# Bundle preprocessing and modeling code in a pipeline
my_pipeline = Pipeline(steps=[
			# 前面定义的ColumnTransformer
			  ('preprocessor', preprocessor),
		    # 前面定义的model
			  ('model', model)
                             ])

# Preprocessing of training data, fit model 
my_pipeline.fit(X_train, y_train)

# Preprocessing of validation data, get predictions
preds = my_pipeline.predict(X_valid)

# Evaluate the model
score = mean_absolute_error(y_valid, preds)
print('MAE:', score)
```