## SimpleImputer
导入方法
```python
from sklearn.impute import SimpleImputer
```
### 作用
用来填充数据里面的缺失值。
### 参数
```python
sklearn.impute.SimpleImputer(*, missing_values=nan, strategy='mean', fill_value=None, copy=True, add_indicator=False, keep_empty_features=False)
```
* **missing_value**s: 缺失值是什么，一般情况下缺失值当然就是空值啦，也就是np.nan
* **strategy**:也就是你采取什么样的策略去填充空值，总共有4种选择。分别是`mean`,`median`, `most_frequent`,以及`constant`，这是对于每一列来说的，如果是
	* mean: 该列由该列的 *均值* 填充。
	* median: 该列由该列的 *中位数* 填充。
	* most_frequent: 该列由该列的 *众数* 填充。
	* constant: 该列由 *自定义数值* 填充。可以将空值填充为`fill_value`的值
* **fill_value**: 如果`strategy='constant'`,则填充fill_value的值。
* **copy**:则表示对原来没有填充的数据的拷贝。
* **add_indicator**:如果该参数为True，则会在数据后面加入n列由0和1构成的同样大小的数据，0表示所在位置非空，1表示所在位置为空。相当于一种判断是否为空的索引。
* **keep_empty_features**: 如果为 True，则调用 `fit` 时仅包含缺失值的特征将在调用 `transform` 时在结果中返回。估算值始终为 `0` ，除非 `strategy="constant"` ，在这种情况下将使用 `fill_value` 。

