# seaborn分类分布图

- **分类分布图**：*随着数据集大小的增长，分类散点图所能提供的关于每个类别中值分布的信息就会受到限制。当这种情况发生时，有几种方法可以以便于跨类别级别进行简单比较的方式总结分布信息*

- **boxplot** *(x, y, hue, data, order, hue_order, palette, dodge=True, linewidth, ax, fliersize, width)*

  *显示了定量数据的分布，这种分布有助于在变量之间或分类变量的不同级别之间进行比较。该框显示数据集的四分位数，使用四分位数范围内函数的方法确定为“离群值”的点:异常值。*

  - *同样散点图一样的问题，我们使用箱线图进行绘制*

    ```python
    import numpy as np
    import pandas as pd
    import matplotlib.pyplot as plt
    import seaborn as sns
    
    tips = pd.read_csv('d:/test_data/tips.csv')
    fig,ax = plt.subplots(figsize=(16,9),dpi=100)
    sns.boxplot(x='day',y='total_bill',data=tips)
    plt.show()
    ```

    ![](C:\Users\唐禹\Desktop\数据分析-唐禹\matplotlib\图\分类分布箱线图1.png)

  - *这次我们研究，吸烟者他们的消费*

    ```python
    #同样我们使用hue,添加一个维度 smoker
    #在箱线图中，dodge默认为True,我们可以设置为False来禁用
    sns.boxplot(x='day',y='total_bill',hue='smoker',data=tips)
    ```

    ![](C:\Users\唐禹\Desktop\数据分析-唐禹\matplotlib\图\分类分布箱线图2.png)

  - *箱线图和分类散点图结合*

    ```python
    #width:元素宽度
    #fliersize:异常值标记的大小
    #color：指定元素颜色
    sns.boxplot(x='day',y='total_bill',data=tips,width=0.2,fliersize=12)
    sns.swarmplot(x='day',y='total_bill',data=tips,color='r')
    ```

    ![](C:\Users\唐禹\Desktop\数据分析-唐禹\matplotlib\图\分类分布箱线图3.png)

- **violinplot** *(x, y, hue, data, order, hue_order, inner，dodge=True, split, palette, scale, linewidth, ax))*

  *小提琴图：箱线图和核密度估计的组合,它显示了一个（或多个）分类变量的几个级别的定量数据的分布，从而可以比较这些分布。与箱线图不同，箱线图所有绘图组件都对应于实际数据点，小提琴绘图具有底层分布的核密度估计。估计过程受样本大小的影响，而相对较小样本的小提琴可能看起来误导平滑。*

  - *我们看一下小提琴图，箱线图展示了分位数的位置，小提琴图展示了任意位置的密度，我们可以通过小提琴密度可以很直接的看出哪些位置的密度高*

    ```python
    # 小提琴图和箱线图比较
    fig,axs = plt.subplots(2,1,figsize=(16,18),dpi=100)
    sns.violinplot(x='day',y='total_bill',data=tips,ax=axs[0])
    sns.boxplot(x='day',y='total_bill',data=tips,ax=axs[1])
    plt.show()
    ```

    ![](C:\Users\唐禹\Desktop\数据分析-唐禹\matplotlib\图\分类分布小提琴图1.png)

    在上图小提琴图中，白点代表的是中位数,黑色盒型的范围是下四分位点到上四分位点，外部形状为核密度估计

  - *接下来我们看两个参数*

    ```python
    fig,axs = plt.subplots(2,1,figsize=(16,18),dpi=100)
    #设置inner
    sns.violinplot(x='day',y='total_bill',data=tips,inner='stick',ax=axs[0],order=['Thur','Fri','Sat','Sun'])
    #设置scale
    sns.violinplot(x='day',y='total_bill',data=tips,scale='count',ax=axs[1],order=['Thur','Fri','Sat','Sun'])
    plt.show()
    
    #inner:“box”，“quartile”，“point”，“stick”，None,小提琴内部的数据点的表示。box，绘制一个微型箱图。quartiles，绘制分布的四分位数。point或stick，则显示每个基础数据点。None：内部什么都没有显示
    
    #scale：“area”，“count”，“width”，用于缩放每个小提琴宽度的方法。area:每把小提琴都有相同的面积。count:小提琴的宽度将按该箱中的观察次数进行缩放。width，每把小提琴都有相同的宽度。
    ```

    ![](C:\Users\唐禹\Desktop\数据分析-唐禹\matplotlib\图\分类分布小提琴2.png)

  - *添加 hue维度,同时拆分小提琴，这样有利于利用空间*

    ```python
    fig,axs = plt.subplots(figsize=(16,18),dpi=100)
    #区分splite和dodge的区别
    sns.violinplot(x='day',y='total_bill',hue='smoker',data=tips,inner='stick',order=['Thur','Fri','Sat','Sun'],split=True)
    plt.show()
    ```

    ![](C:\Users\唐禹\Desktop\数据分析-唐禹\matplotlib\图\分类分布小提琴3.png)

  - *小提琴图和分类散点图结合*

    ```python
    fig,ax = plt.subplots(figsize=(16,18),dpi=100)
    sns.violinplot(x='day',y='total_bill',data=tips,inner=None,order=['Thur','Fri','Sat','Sun'],split=True)
    sns.swarmplot(x='day',y='total_bill',data=tips,color='k',order=['Thur','Fri','Sat','Sun'])
    plt.show()
    ```

    ![](C:\Users\唐禹\Desktop\数据分析-唐禹\matplotlib\图\分类分布小提琴4.png)

- **boxenplot** *(x, y, hue, data, order, hue_order, palette, dodge=True, linewidth, ax, width)*

  *字母值图：这种类型的图最初被称为“字母值”图，因为它显示了大量被定义为“字母值”的分位数。它类似于在绘制分布的非参数表示时的箱形图，其中所有特征都对应于实际观测值。通过绘制更多的分位数，它提供了关于分布形状的更多信息，特别是在尾部。*

  - *绘制的图表和箱线图类似，但是它经过优化，可以显示更多关于分布的信息，适合更大的数据集*

    ```python
    #参数使用基本一样，boxenplot不能设置异常值大小
    sns.boxenplot(x='day',y='total_bill',data=tips)
    ```

    ![](C:\Users\唐禹\Desktop\数据分析-唐禹\matplotlib\图\分类分布箱线图4.png)

  - *boxenplot和boxplot比较*

    ```python
    fig,axs = plt.subplots(2,1,figsize=(16,18),dpi=100)
    sns.boxenplot(x='day',y='total_bill',hue='smoker',data=tips,ax=axs[0])
    sns.boxplot(x='day',y='total_bill',hue='smoker',data=tips,ax=axs[1])
    plt.show()
    #从图中我们可以看出boxenplot显示的信息更多
    ```

    ![](C:\Users\唐禹\Desktop\数据分析-唐禹\matplotlib\图\分类分布箱线图5.png)


