# seaborn分面绘图

- **catplot**:*可以绘制不同的分类图，只需要传入参数 kind 就可以绘制不同 的分类图, api 一样，对它们进行统一的高级访问*

- 不同的分类图类型，三个不同的族

  - 分类散点图
    - *stripplot()*  *(kind="strip",默认)*
    - *swarmplot()  (kind="swarm")*
  - 分类分布图
    - *boxplot()  (kind='box')*
    - *violinplot()  (kind='violin')*
    - *boxenplot()  (kind='boxen')*
  - *分类估计图*
    - *pointplot()  (kind='point')*
    - *barplt()  (kind='bar')*
    - *countplot()  (kind='count')*

- *大家思考个问题：在我们 tips中，按 day进行分类，显示 total_bill 数据，使用 hue增加 smoker维度，如果说我需要在此基础上，按 time再次进行分组？*  多种分组变量对数据进行可视化

  ```python
  import pandas as pd
  import numpy as np
  import matplotlib.pyplot as plt
  import seaborn as sns
  
  tips = pd.read_csv('d:/test_data/tips.csv')
  sns.catplot(kind='bar',x='day',y='total_bill',hue='smoker',col='time',data=tips)
  plt.show()
  ```

  ![](C:\Users\唐禹\Desktop\数据分析-唐禹\matplotlib\图\分类汇总1.png)

- 
