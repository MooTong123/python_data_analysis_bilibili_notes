# seaborn分类散点图

- **分类散点图**:*散点图中属于一个类别的所有点将沿着与分类变量对应的轴落在相同位置，在seaborn中有两种不同的分类散点图。*

- *思考*：

  - *在我们的 tips 数据集中，我们如何通过 day 来观察 total_bill 数据集中在哪些值区间？*

- **seaborn.stripplot** *(x,y,h,data,order,hur_order,jitter,dodge=False,ax, palette)*

- **seaborn.swarmplot**  *(x,y,h,data,order,hur_order,dodge=False,ax, palette)*

  - *通过 day 来观察 total_bill 数据集中在哪些值区间*

  ```python
  import pandas as pd
  import numpy as np
  import matplotlib.pyplot as plt
  import seaborn as sns
  
  tips = pd.read_csv('d:/test_data/tips.csv')
  
  fig,axs = plt.subplots(figsize=(16,9),dpi=100)
  
  # data: DataFrame, array, 或 list of arrays,
  # x,y,hue:数据或者数据中的名称
  #jitter:抖动的大小,默认True,指定False来禁用抖动，同时也可以指定抖动的量,如：jitter=0.1
  sns.stripplot(y='total_bill',x='day',data=tips)
  plt.show()
  #从图中可以发现什么？
  ```

  ![](C:\Users\唐禹\Desktop\数据分析-唐禹\matplotlib\图\分类散点图1.png)

  - *从上图中可以发现，周末比工作日消费的要多，现在我们需要判断主要在哪个时间进行消费？*

    ```python
    #在原来的基础上，我们需要在增加一个维度
    #hue:向分类图中添加另一个维度
    #order:指定排序
    sns.stripplot(y='total_bill',x='day',hue='time',data=tips,order=['Thur','Fri','Sat','Sun'])
    
    ```

    ![](C:\Users\唐禹\Desktop\数据分析-唐禹\matplotlib\图\分类散点图2.png)

  - *现在我们需要把 时间段进行拆分*

    ```python
    # doge:在设用 hue增加维度的时候,设置为Ture,将沿着分类轴分离不同色调级别的条带。否则，每个级别的点将绘制在一起，默认False
    #palette：设置调色盘
    sns.swarmplot(y='total_bill',x='day',hue='time',data=tips,order=['Thur','Fri','Sat','Sun'],
                  dodge=True,palette='bright')
    ```

    ![](C:\Users\唐禹\Desktop\数据分析-唐禹\matplotlib\图\分类散点图3.png)


- *第二种方法，swarmplot()，防止他们沿着分类轴进行重叠，参数用法都是一样*

  - *探究 吸烟和不吸烟者给小费的情况*

    ```python
    fig,axs = plt.subplots(2,1,figsize=(16,18),dpi=100)
    
    #ax:指定绘图区axes
    #linewidth:构图元素的灰线的宽度
    #size:标记的直径
    sns.swarmplot(y='tip',x='smoker',data=tips,palette='bright',ax=axs[0]，linewidth=1,size=10)
    sns.stripplot(y='tip',x='smoker',data=tips,palette='bright',ax=axs[1],linewidth=1)
    plt.show()
    ```

    ![](C:\Users\唐禹\Desktop\数据分析-唐禹\matplotlib\图\分类散点图4.png)

  - *更换分类轴,特别是当类别名称相对较长或有许多类别时，像我们前面的柱形图，省份过多，我们将分类名显示在y轴上*

    ```python
    #我们只需要将变量赋值都轴上
    sns.swarmplot(y='day',x='total_bill',hue='time',data=tips,order=['Thur','Fri','Sat','Sun'],
                  dodge=True,palette='bright',
                 )
    ```

    ![](C:\Users\唐禹\Desktop\数据分析-唐禹\matplotlib\图\分类散点图5.png)
