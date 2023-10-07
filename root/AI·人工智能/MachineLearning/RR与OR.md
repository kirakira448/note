### RR(Relative Risk)——相对危险度
- 表示两种情况下发病密度或者说发病概率之比
    
    - $P_t$：实验组人群反应阳性概率，a：实验组阳性，$n_t$：实验组总人数。        
    - $P_c$：对照组人群反应阳性概率，c：对照组阳性，$n_c$：对照组总人数。        
        $$
    RR=\frac{P_t}{P_c}=\frac{a/n_t}{c/n_c}   
	$$
        
- 如果RR > 1，说明相应的自变量取值增加，会导致个体发病/死亡风险增加若干倍，例如：吸烟者的发病概率是非吸烟者的5倍    

- RR在医学中得到了极为广泛的应用    
- RR的计算条件比较苛刻（观察周期长）

### OR(Odds Ratio)——优势比
- 为下列两种比例之比
    
    - 反应阳性人群中实验因素有无的比例 a/b
    - 反应阴性人群中实验因素有无的比例 c/d   
    $$
  OR=\frac{a/b}{c/d}  
  $$
    
    例如：某疾病病例中吸烟(a)/非吸烟者(b)的比例是非病例中吸烟(c)/非吸烟者(d)比例的3倍
    
- OR可以间接反映关联强度，但是理解上比较困难    
- 发病概率较低时，OR往往近似的在按照RR的含义进行解释和使用

**代码实现：**
- scipy的实现方式

scipy.stats.fisher_exact()中可以计算OR值，相应的检验P值则是确切概率法的P值
```python
OR, P = ss.fisher_exact(pd.crosstab(home.Ts9, home.O1))
```

- statsmodels的实现方式
```python
import numpy as np
import statsmodels.stats.contingency_tables as tbl

# 这里必须使用np.array函数进行数组转换，否则后续计算会出问题
table = tbl.Table2x2(np.array(pd.crosstab(home.Ts9, home.O1)))

print(table.oddsratio) # OR值
print(table.summary()) # 汇总信息
```