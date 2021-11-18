# matplotlib散点图

- **散点图**：*用两组数据构成多个坐标点，考察坐标点的分布，判断两变量之间是否存在某种关联或总结坐标点的分布模式。散点图将序列显示为一组点。值由点在图表中的位置表示。*

  *应用场景：判断两个变量之间是否存在关联，判断异常值*

- *探究 投资额和住宅投资的关系*

  ```python
  import pandas as pd
  import numpy as np
  import matplotlib.pyplot as plt
  
  data = pd.read_csv('d:/test_data/房地产投资金额.csv',engine='python',index_col=0)
  
  data.plot(kind='scatter',x='投资额',y='住宅',figsize=(16,9),color='r')
  #dataframe绘制散点图,需要指定x,y为 dataframe中的列,同样可以给图像添加样式,如指定color,alpha,marker
  plt.show()
  
  #从图中我们可以看出,投资额和住宅成正比关系
  ```

  ![](C:\Users\唐禹\Desktop\数据分析-唐禹\matplotlib\图\散点图.png)
