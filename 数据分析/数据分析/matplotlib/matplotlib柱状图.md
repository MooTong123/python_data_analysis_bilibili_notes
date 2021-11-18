# matplotlib柱状图

- **柱状图**：*一种以长方形的长度为变量的表达图形的统计报告图，由一系列高度不等的纵向条纹表示数据分布的情况，用来比较两个或以上的价值（不同时间或者不同条件），只有一个变量，通常利用于较小的数据集分析*

  - 柱状图：*柱形图、堆积柱形图、百分比堆积柱形图等。*
  - *适用场景*
    1. 适合分析分类数据字段、或者连续的数据字段，利用柱子的高度来反映数据的数值差异。、
    2. 适合分析对比组内各项数据
    3. 堆积柱：可以形象的展示一个大分类包含的每个小分类的数据，以及小分类的占比情况，显示的是单个项目与整体之间的关系
    4. 百分比堆积柱形图：矩形高度表示每子项占当前项的百分比

- **案例**

  ```python
  import numpy as np
  import pandas as pd
  import matplotlib.pyplot as plt
  
  data = pd.read_csv('d:/test_data/房地产投资金额.csv',index_col='地区',engine='python')
  data1 = data[0:5]
  data1.plot.bar(figsize=(16,9))
  #data1.plot(kind=bar,figsize=(16,9))
  plt.show()
  
  #在柱状图中，每一行的值进行分组，我们可以看出北京是一组，天津是一组，河北是一组
  ```

  ![](C:\Users\唐禹\Desktop\数据分析-唐禹\matplotlib\图\柱状图1.png)

  *条形图：维度分类较多或维度名称比较长的时候使用横向树状图（条形图）*

  ```python
  data.plot(kind='barh',figsize(16,9))
  plt.show()
  ```

  ![](C:\Users\唐禹\Desktop\数据分析-唐禹\matplotlib\图\条形图.png)

  *堆积图：更直观对比整体的数据，可以更清晰的看出各种类别的占比情况*

  ```python
  data.plot(kind='barh',stacked=True,figsize=(16,9)) #传递参数stacked=True来生成堆积树状图
  plt.show()
  ```

![](C:\Users\唐禹\Desktop\数据分析-唐禹\matplotlib\图\堆积图.png)

​	*百分比堆积树状图：展示的占比的情况*

```python
data.div(data.sum(1),axis=0).plot(kind='barh',figsize=(16,9),stacked=True)
plt.show()
```

![](C:\Users\唐禹\Desktop\数据分析-唐禹\matplotlib\图\百分比.png)

- *大家可以使用面向对象方法绘制，可以自己定制图形展示*

