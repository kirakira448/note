导入要用到的包
```python
# 处理数据
import pandas as pd
# 创建 RandomForestRegressor 模型
from sklearn.ensemble import RandomForestRegressor
# 检查误差
from sklearn.metrics import mean_absolute_error
# 分割训练集和验证集
from sklearn.model_selection import train_test_split
```
加载数据
```python
# Load the data, and separate the target
# 数据路径
iowa_file_path = '../input/train.csv'
# 导入数据
home_data = pd.read_csv(iowa_file_path)
# 有时需要做数据清洗，移除空值。
#`axis`：  
# 0: 行操作（默认）  
# 1: 列操作
# home_data=home_data.dropna(axis=0)

# 选择目标值（监督值）
y = home_data.SalePrice

# 选择特征
features = ['LotArea', 'YearBuilt', '1stFlrSF', '2ndFlrSF', 'FullBath', 'BedroomAbvGr', 'TotRmsAbvGrd']
X = home_data[features]
# X.head()  # 观察数据
```
拆分数据
```python
# 将数据分为训练集和验证集
# train_size 和 test_size 可以不写
train_X, val_X, train_y, val_y = train_test_split(X, y, train_size=0.8, test_size=0.2,
                                                      random_state=1)
```
定义一个 `RandomForestRegressor` 模型
```python
# 声明模型
# n_estimators : tree的数量，默认值100
rf_model = RandomForestRegressor(n_estimators=50,random_state=1)
# 拟合训练集
rf_model.fit(train_X, train_y)
# 对验证集数据进行预测
rf_val_predictions = rf_model.predict(val_X)
# 比较 预测值与真实值 ，计算误差
rf_val_mae = mean_absolute_error(rf_val_predictions, val_y)
```
`mean_absolute_error`的误差越小，说明拟合程度越高，但需要注意过拟合问题。