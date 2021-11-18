# Numpy逻辑操作和np.where

1. 逻辑运算

   1. 比较运算符 `>, >=, <, <=, ==, !=` ，比较运算符，返回的是一个布尔数组。

   2. 逻辑运算符`与:&, 或:|,非:~`

   3. 二元通用函数`与:logical_and, 或:logical_or, 非:lodical_not`

      ```python
      #比较运算符
      #向量化
      arr1 = np.random.randn(4,3)
      arr1
      """
      array([[-0.11644283,  0.26881624, -0.636891  ],
             [ 0.41491463,  0.75958032, -0.79139132],
             [-0.65056162, -1.65086047,  0.30840633],
             [ 0.44048015,  2.60792486, -1.2136428 ]])
      """
      arr1 < 1
      """
      array([[ True,  True,  True],
             [ True,  True,  True],
             [ True,  True,  True],
             [ True, False,  True]])
      """
      #数组与数组比较
      arr2 = np.random.randn(4,3)
      arr2
      """
      array([[ 1.07975731,  0.48405982,  0.83102948],
             [ 0.25161364, -0.84813959,  0.30692867],
             [ 0.67593645,  2.11885395,  0.52587073],
             [-0.82323498,  0.87254439, -0.55737282]])
      """
      arr1 > arr2
      """
      array([[False, False, False],
             [ True,  True, False],
             [False, False, False],
             [ True,  True, False]])
      """
      ```

      ```python
      #逻辑运算符
      (arr1>-0.5) & (arr1<0.5)
      """
      array([[ True,  True, False],
             [ True, False, False],
             [False, False,  True],
             [ True, False, False]])
      """
      (arr1>-0.5) | (arr1<0.5)
      """
      array([[ True,  True,  True],
             [ True,  True,  True],
             [ True,  True,  True],
             [ True,  True,  True]])
      """
      ~(arr1>0)
      """
      array([[ True, False,  True],
             [False, False,  True],
             [ True,  True, False],
             [False, False,  True]])
      """
      ```

      ```python
      #二元通用函数
      np.logical_and(arr1>-0.5 , arr1<0.5)
      """
      array([[ True,  True, False],
             [ True, False, False],
             [False, False,  True],
             [ True, False, False]])
      """
      np.logical_or(arr1>-0.5 , arr1<0.5)
      """
      array([[ True,  True,  True],
             [ True,  True,  True],
             [ True,  True,  True],
             [ True,  True,  True]])
      """
      np.logical_not(arr1>-0.5)
      """
      array([[False, False,  True],
             [False, False,  True],
             [ True,  True, False],
             [False, False,  True]])
      """
      ```

2. `np.where(condition, x, y)`:是三元表达式 x if condition else y的向量化。如果是True,输出x,相反,False，输出y。传递给np.where的数组可以是同等大小的数组，也可以是标量。

   ```python
   #1.
   np.where([[True,False], [True,True]],   #condition
                [[1,2], [3,4]],            #x
                [[9,8], [7,6]])            #y
   """
   array([[1, 8],
          [3, 4]])
   """
   # 2.
   np.where(arr1>0) #只有条件 (condition)，没有x和y，则输出满足条件 (即非0) 元素的坐标。这里的坐标以tuple的形式给出，通常原数组有多少维，输出的tuple中就包含几个数组，分别对应符合条件元素的各维坐标。
   """
   (array([0, 1, 1, 2, 3, 3], dtype=int64),
    array([1, 0, 1, 2, 0, 1], dtype=int64))
   """
   # 3. 典型用法,标量和数组联合，进行值的替换
   np.where(arr1>0,1,-1)
   """
   array([[-1,  1, -1],
          [ 1,  1, -1],
          [-1, -1,  1],
          [ 1,  1, -1]])
   """
   ```

3. `any(),all()方法`: 这两个方法可以快速检查布尔数组,`any()`:检查数组中是否至少有一个True, `all()`:检查是否每个值都为True.

   ```python 
   (arr1 <1).sum() # True的个数
   11
   
   (arr1<1).any()
   True
   
   np.all((arr1<1))
   False
   # 这两个方法同时也可以适用于非布尔数组，非0的 元素就会按True处理
   ```

