# senborn散点图关联变量

- **散点图**：*散点图是统计可视化的支柱。它使用点云描述两个变量的联合分布，其中每个点表示数据集中的一个值。这种描述很直观推断出大量的信息，关于它们之间是否有任何有意义的关系。*

- **seaborn.scatterplot**:*(x, y, hue, hue, style, size,data, palette)*

- *在matplotlib中，我们已经讲解了散点图，散点图探究两个变量之间的关系, 在我们 tips数据集中，我们观察 total_bill 和 tip两个变量之间的关系*

  ```python
  import numpy as np
  import pandas as pd
  import matplotlib.pyplot as plt
  import seaborn as sns
  
  tips = pd.read_csv('d:/test_data/tips.csv')
  
  fig,ax= plt.subplots(figsize=(16,9),dpi=100)
  #seaborn中我们会在散点图使用 scatterplot
  sns.scatterplot(x='total_bill',y='tip',data=tips)
  plt.show()
  ```

  ![](C:\Users\唐禹\Desktop\数据分析-唐禹\matplotlib\图\可视化统计散点图1.png)

  - *在上面我们探究两个变量直接的关系，现在我们需要在图中很直白的看出哪个时间段*

    ```python
    sns.scatterplot(x='total_bill',y='tip',hue='time',data=tips)
    #hue:不同颜色的点变量进行分组
    #size:不同大小的点的变量进行分组
    #style:具有不同标记的点的变量进行分组
    #这里我们可以指定hue,或size或style来进行分组，也可以同时指定
    ```

    ![](C:\Users\唐禹\Desktop\数据分析-唐禹\matplotlib\图\可视化统计散点图2.png)

  - *不同的颜色和标记来显示分组变量*

    ```python
    sns.scatterplot(x='total_bill',y='tip',hue='time',style='smoker',data=tips)
    #当然我们也可以指定size
    ```

    ![](C:\Users\唐禹\Desktop\数据分析-唐禹\matplotlib\图\可视化统计散点图3.png)

  - *大家可以思考一下，如果 hue 传入 size列，会有什么变化？*


