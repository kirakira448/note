
# KMeans算法介绍

K-Means是聚类算法中最常用的一种，是一种迭代求解的聚类分析算法；
聚类是一种无监督学习，事先并不知道分类标签是什么，它能够将具有相似特征的对象划分到同一个集合（簇）中。
簇内的对象越相似，聚类算法的效果越好。
![[KMeans算法.png]]

## KMeans算法原理

1. 从样本中随机选择K个点——聚类中心（也可以随机生成K个并不存在于原始数据中的样   
    本点作为初始聚类中心）
    
2. 簇分配：遍历每个样本，然后根据每一个点是与红色聚类中心更近，还是与蓝色聚类中心更近，来将每个数据点分配给K个聚类中心之一
    
3. 根据聚类结果，重新计算k个簇各自的平均值（Means）位置,将该平均值位置作为该簇新的聚类中心
    
4. 不断重复迭代上述的（2）与（3）两个步骤，直到聚类中心点的变化很小，或者达到指定的迭代次数

## KMeans损失函数

$$
J(c^{(1)},...,c^{(m)},\mu_1,...,\mu_k)=\frac{1}{m}\sum_{i=1}^{m} ||x^{(i)} - \mu_j||^2
$$

- KMeans损失函数是每个数据点与其所关联的聚类中心点之间的平均距离
- 最小化损失函数可以帮助k-means找到更好的簇

>**注意：**
>
>对于聚类数量的选择（参数K的选择），没有一个统一的选择方法，可以根据业务需要选择

## sklearn使用KMeans算法
```python
from sklearn.cluster import KMeans
km = KMeans(n_clusters=2,random_state=666) # 聚成两类
km.fit(X)
y_predict = km.predict(X) # 预测
```

## KMeans的衡量指标

CH指标：
	同时考虑了各个簇之间的分离程度与簇内部的分离程度，来衡量聚类效果。
	CH分数越高，说明聚类效果越好
```python
from sklearn.metrics import calinski_harabasz_score
# 分数越高，聚类效果越好
calinski_harabasz_score(X,y_pred)
```