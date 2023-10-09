交叉列表取值

示例：
![[crosstab01.png]]
```python
pd.crosstab(df.Nationality, df.Handedness)
```
输出：
![[crosstab02.png]]

crosstab 第一个参数是列，第二个参数是行。还可以添加第三个参数:
```python
pd.crosstab(df.Sex, df.Handedness, margins = True)
```
输出：
![[crosstab03.png]]