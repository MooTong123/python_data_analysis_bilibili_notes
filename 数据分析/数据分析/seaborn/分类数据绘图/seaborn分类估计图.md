# seaborn分类估计图

- **分类分布图**：*显示值的集中趋势 (数据的中心位置) 估计,api基本相同，集中趋势是用来描述舆论现象的重要统计分析指标，常用的有平均数、中位数和众数等，它们在不同类型的分布数列中有不同的测定方法（根据情况而定）。*

- **barplot**: *(x, y, hue, hue, data, order, estimator=<function mean>, ci=95, capsize,ax, dpdge=True)*

  *绘制条形图，并使用函数来获得估计值（默认均值）。条形图表示具有每个矩形的高度的数值变量的集中趋势的估计，并且使用误差条提供围绕该估计的不确定性的一些指示。条线图只显示平均值（或其他估计值），如果需要显示更多值分布的信息，使用箱线图或小提琴图更合适。*

  - *我们可以思考一下，我们通过 day 来 绘制一下 关于 total_bill 的平均值的条形图？*

    ```python
    #pandas 和seaborn 绘制条形图对比
    
    fig,axs = plt.subplots(2,1,figsize=(16,18),dpi=100)
    #使用seaborn
    sns.barplot(x='day',y='total_bill',data=tips,ax=axs[0],order=['Fri','Sat','Sun','Thur'])
    #使用pandas
    tips.groupby('day')['total_bill'].mean().plot(kind='bar', ax=axs[1])
    
    plt.show()
    ```

    ![](C:\Users\唐禹\Desktop\数据分析-唐禹\matplotlib\图\分类估计图1.png)

    从两图中，我们可以进行对比, Seaborn 对 day列先进行分组归类, 然后按照 **estimator**参数的方法计算值，就是条形图所显示的值，细长的黑线，称为误差棒, 表示各类的数值相对于条形图所显示的误差

  - *在上图中，我们使用 estimator 的默认函数 mean, 我们也可以使用其他的函数*

    ```python
    # 使用中位数作为集中趋势的估计
    fig,axs = plt.subplots(figsize=(16,18),dpi=100)
    #estimator:估计器，用于每个分类箱内估计的统计函数
    sns.barplot(x='day',y='total_bill',data=tips,estimator=np.median)
    plt.show()
    ```

    ![](C:\Users\唐禹\Desktop\数据分析-唐禹\matplotlib\图\分布分类条形图2.png)

  - *在估计值附近绘制误差区间的大小，以及设置误差棒的帽条的宽度（上下两条横线）*

    ```python
    fig,ax = plt.subplots(figsize=(16,18),dpi=100)
    sns.barplot(x='day',y='tip',data=tips,ci='sd',capsize=0.3)
    plt.show()
    
    # ci: 设置误差范围,(0 - 100), sd,使用标准偏差， None：不显示误差棒
    # capsize : 设置误差棒的帽条宽度
    ```

    ![](C:\Users\唐禹\Desktop\数据分析-唐禹\matplotlib\图\分类估计图条形图3.png)

- **pointplot**: *(x, y, hue, hue, data, order, estimator=<function mean>, ci=95, capsize,ax, dodge=False, join=True, markers='o', linestyle='-')*

  *点图表示通过散点图点的位置估计数值变量的集中趋势，并使用误差条提供围绕该估计的不确定性的一些指示。*

  *点图可以比条形图更有用，**用于聚焦一个或多个分类变量的不同级别之间的比较**。他们特别善于交互作用：**一个分类变量的层次之间的关系如何在第二个分类变量的层次之间变化**。从相同`hue` 水平连接每个点的线允许通过斜率的差异来判断相互作用，这对于眼睛比比较几组点或条的高度更容易。*

  - *绘制一组分类变量分组的点图*

    ```python
    fig,ax = plt.subplots(figsize=(16,9),dpi=100)
    sns.pointplot(x='day',y='total_bill',data=data,order=['Thur','Fri','Sat','Sun'])
    plt.show()
    ```

    ![](C:\Users\唐禹\Desktop\数据分析-唐禹\matplotlib\图\分类估计点图.png)

    上图中，点为这组数据的平均值点，竖线为误差棒, 默认均值点会相连

  - *绘制每天吸烟和不吸烟 total_bill的总和*

    ```python
    sns.pointplot(x='day',y='total_bill',hue='smoker',data=data,order=['Thur','Fri','Sat','Sun'],estimator=np.sum)
    #通过 hue，增加维度
    #通过 estimator,指定值的统计方法
    ```

    ![](C:\Users\唐禹\Desktop\数据分析-唐禹\matplotlib\图\分类估计图点图2.png)

  - *绘制不同的标记和线条样式*

    ```python
    sns.pointplot(x='day',y='total_bill',hue='smoker',data=data,order=['Thur','Fri','Sat','Sun'],estimator=np.sum,
     markers=['o','D'], linestyle=['-','--'])
    
    # markers:设置标记样式
    # linestyle:设置线条样式
    ```

    ![](C:\Users\唐禹\Desktop\数据分析-唐禹\matplotlib\图\分类估计图点图3.png)

  - *取消点的连接线,并沿分类轴进行分离*

    ```python
    sns.pointplot(x='day',y='total_bill',hue='smoker',data=data,order=['Thur','Fri','Sat','Sun'],
                  estimator=np.sum,markers=['o','D'],join=False,dodge=True)
    ```

    ![](C:\Users\唐禹\Desktop\数据分析-唐禹\matplotlib\图\分类估计图点图4.png)

  - 其他参数基本和 barplot 一样

- **countplot**: *(x, y, hue, hue, data, order, ax)*

  *条形图的特例, 显示每个类别中的数据数量，而不是计算数据的统计值，称为计数图。*

  - *绘制 通过day 的每个类别的值计数*

    ```python
    fig, ax = plt.subplots(figsize=(16,9),dpi=100)
    sns.countplot(x='day',data=tips)
    #同 tips.groupby('day')['total_bill'].count().plot(kind='bar')
    plt.show()
    ```

    ![](C:\Users\唐禹\Desktop\数据分析-唐禹\matplotlib\图\分类估计计数图1.png)

  - *显示两个分类变量的值计数*

    ```python
    sns.countplot(x='day',hue='smoker',data=tips)
    ```

    ![](C:\Users\唐禹\Desktop\数据分析-唐禹\matplotlib\图\分类分布估计图2.png)


