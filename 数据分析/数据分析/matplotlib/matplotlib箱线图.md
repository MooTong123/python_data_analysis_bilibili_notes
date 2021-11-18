# matplotlib箱线图

- **箱线图**：*是一种直观简洁的方式去呈现一组数据的分布. 因其形状如箱子而得名. 箱线图广泛用于各个数据分析领域.  它能非常简单明了地显示一组数据中5个重要数值, 最大值 (Maximum Value), 最小值 (Minimum Value), 中位数 (Median Value), 下四分位数 (First Quartile), 上四分位数 (Third Quartile). 箱线图还能发现一组数据中的存在的异常值 (Outliers).*

  *分位数*：*把所有数值由小到大排列并分成四等份，处于三个分割点位置的数值就是四分位数。*

  ![](C:\Users\唐禹\Desktop\数据分析-唐禹\matplotlib\图\箱线图6.jpg)

- *查看投资数据的异常值*

  ```python
  # 
  data.plot(kind='box',figsize=(16,9))
  plt.show()
  
  #高于上边缘的值，为异常值,我们可以用于查看异常值
  ```

  ![](C:\Users\唐禹\Desktop\数据分析-唐禹\matplotlib\图\箱线图.png)


