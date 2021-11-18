# matplotlib图像结构

- *实现一个简单的matplotlib画图*

  ```python
  import numpy as np
  import matplotlib.pyplot as plt
  
  data= np.arange(10)
  plt.plot(data) #折线图函数
  plt.show()#输出图像
  ```

  ![](C:\Users\唐禹\Desktop\数据分析-唐禹\matplotlib\图\图1.png)

- **Part of a Figure**

  - *matplotlib绘制的图位于 （Figure）对象中*

    ![](C:\Users\唐禹\Desktop\数据分析-唐禹\matplotlib\图\绘图区域.jpg)

  - *Figure*:*整个图形（可以改变大小和分辨率），想象为画画的画布，可以有任意数量的 Axes,至少要有一个有用*

    ```python
    #创建一个画布
    fig = plt.figure()
    """
    参数：
    figsize:画布大小，默认None,(width,height)整数元组
    dpi:图像分辨率,默认None,整数
    facecolor:背景颜色
    """
    ```

  - *Axes*：*坐标系，数据绘图的区域*

  - *Axis*：*坐标轴（大小限制，刻度，刻度标签），坐标系中的一条轴*

- 辅助显示层

  *辅助显示层为Axes(绘图区)内的除了根据数据绘制出的图像以外的内容，主要包括Axes外观(facecolor)、边框线(spines)、坐标轴(axis)、坐标轴名称(axis label)、坐标轴刻度(tick)、坐标轴刻度标签(tick label)、网格线(grid)、图例(legend)、标题(title)等内容。*

  ![](C:\Users\唐禹\Desktop\数据分析-唐禹\matplotlib\图\图像结构.webp)

- 图像层

  *图像层指Axes内通过plot、scatter、bar、histogram、pie等函数根据数据绘制出的图像。*

  ![](C:\Users\唐禹\Desktop\数据分析-唐禹\matplotlib\图\图像层.jpeg)
