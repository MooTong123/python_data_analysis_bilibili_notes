# Numpy数组广播

1. `广播`:广播描述了算法如何在不同形状的数组之间的运算。

2. `Numpy数组算术`

   ```python
   arr1 = np.random.randint(10,size=(3,4))
   arr1
   """
   array([[2, 1, 0, 0],
          [9, 5, 1, 7],
          [8, 1, 5, 4]])
   """
   
   arr1 * 2  #最简单的广播，标量和数组组合,标量值2，被广播给乘法运算中的所有其他元素
   """
   array([[ 4,  2,  0,  0],
          [18, 10,  2, 14],
          [16,  2, 10,  8]])
   """
   
   arr1 * arr1 #相同尺寸的数组运算
   """
   array([[ 4,  1,  0,  0],
          [81, 25,  1, 49],
          [64,  1, 25, 16]])
   """
   
   #在前面逻辑运算的时候我们已经讲过了，同尺寸的数组可以比较，得到的是一个布尔数组
   ```

3. `广播的规则`:**对于每个结尾维度(从尾部开始),轴的长度都匹配或者相对应的轴一方长度是1，那么则认为可以兼容广播的，广播会在丢失的或在长度为1的轴上进行**。

   ```python
   arr1 = np.arange(12).reshape(4,3)
   arr1
   """
   array([[ 0,  1,  2],
          [ 3,  4,  5],
          [ 6,  7,  8],
          [ 9, 10, 11]])
   """
   
   arr2 = np.array([1,2,3])
   arr2
   """
   array([1, 2, 3])
   """
   
   arr3 = arr1 + arr2
   arr3
   """
   array([[ 1,  3,  5],
          [ 4,  6,  8],
          [ 7,  9, 11],
          [10, 12, 14]])
   """
   
   arr1.shape
   (4,3)
   arr2.shape
   (3,)
   #满足我们广播规则,从尾部开始轴的长度匹配,广播是兼容的,广播在丢失的轴上进行。
   #案例中丢失的是0轴,按'列'进行广播，一维数组沿0轴进行广播
   
   ```

   ```python
   arr4 = np.arange(1,5).reshape(4,1)
   arr4
   """
   array([[1],
          [2],
          [3],
          [4]])
   """
   arr5 = arr1+arr4
   arr5
   """
   array([[ 1,  2,  3],
          [ 5,  6,  7],
          [ 9, 10, 11],
          [13, 14, 15]])
   """
   arr1,shape
   (4,3)
   arr5.shape
   (4,1)
   #满足广播规则,从尾部开始，轴的长度一方为1,广播在缺失的轴上进行广播
   #案例中丢失的是1轴,按'行'进行广播沿着轴1对二维数组进行广播
   ```

   ![](C:\Users\唐禹\Desktop\数据分析-唐禹\广播，沿0轴，列进行广播.png)

![](C:\Users\唐禹\Desktop\数据分析-唐禹\广播。沿1轴，行进行广播.png)

![](C:\Users\唐禹\Desktop\数据分析-唐禹\三维广播沿0轴.png)

**总结**

1. 操作两个数组，先比较数组的shape：`a.维度相等，b.相对应的轴长度为1`

2. 所有输入数组都向其中shape最长的数组看齐，shape中不足的部分都通过在前面加1补齐

3. 输出数组的shape是输入数组shape的各个轴上的最大值




