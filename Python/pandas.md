```python
# 数据分析常用引用
import numpy as np
import pandas as pd
from pandas import DataFrame,Series
import matplotlib
import matplotlib.pyplot as plt
from pandasql import sqldf


# pandasql 中 sqldf 的使用 （类似R语言中的sqldf包）
# 普通定义DataFrame
# loveDf = pd.DataFrame([{'name':'wujunwei','age':31},{'name':'wangcaixia','age':29}])
# 定义DataFrame的同时，制定column顺序
loveDf = pd.DataFrame(columns=['name','age'],
                      data=[{'name':'wujunwei','age':31},{'name':'wangcaixia','age':29}])
pysqldf = lambda q: sqldf(q, globals())
pysqldf('select * from loveDf;')
```
