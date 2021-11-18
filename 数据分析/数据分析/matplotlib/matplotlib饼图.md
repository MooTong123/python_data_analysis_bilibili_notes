# matplotlib饼图

- **饼图**：*用于表示不同分类的占比情况，通过弧度大小来对比各种分类。饼图通过将一个圆饼按照分类的占比划分成多个区块，整个圆饼代表数据的总量，每个区块（圆弧）表示该分类占总体的比例大小，所有区块（圆弧）的加和等于 100%。*

  *应用场景：分类占比*

- *每个省份投资额占比*

  ```python
  #由于分类过多，截取前5组数据进行绘图
  
  # y 为dataframe列名，或者列名列表,当绘制多列数据,指定subplots=True，绘制在不同的子图中
  # autopct:在图中显示百分比
  #shadow:布尔值,为饼图增加阴影效果
  # explode:为饼图增加破裂效果，值越大，破裂越大
  #startangle:饼图旋转角度，从X轴逆时针旋转
  data[0:5].plot(kind='pie',y='投资额',figsize=(16,9),autopct="%1.2f%%",shadow=True,explode=(0,0,0.3,0,0),startangle=90)
  
  #让饼图保持正圆形
  plt.axis('equal')
  plt.show()
  ```

  ![](C:\Users\唐禹\Desktop\数据分析-唐禹\matplotlib\图\饼图.png)
