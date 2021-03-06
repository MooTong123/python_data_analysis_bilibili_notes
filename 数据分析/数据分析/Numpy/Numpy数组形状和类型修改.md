# Numpy数组形状和类型修改

1. `np.reshape(a,newshape,order='C')`:**原数组size不变的前提下**，改变原数组的形状

   | 参数     | 描述                                                         |
   | -------- | ------------------------------------------------------------ |
   | a        | array_like要重新整形的数组                                   |
   | newshape | `int`或`int的tuple` ，新的形状应该和原始形状兼容如果是整数，则结果将是该长度的1-D数组。一个形状维度可以是`-1`。在这种情况下，从数组的长度和其余维度推断该值 |
   | order    | {'C', 'F', 'A'} 'C' -- 按行，'F' -- 按列，'A' -- 原顺序。    |

   `ndarray.reshape(shape,order='C')`：**原数组size不变的前提下**,返回包含具有新形状的相同数据的数组,与自由函数不同`np.reshape`，此方法`ndarray`允许将shape参数的元素作为单独的参数传递。

   ```python
   #ndarray.reshape方法
   #随机生成一个数组
   arr1 = np.random.rand(3,4)
   """ 
   array([[0.40919593, 0.53439411, 0.17478334, 0.88506119],
          [0.52465668, 0.40275561, 0.85389365, 0.69344744],
          [0.06308938, 0.24195379, 0.43457003, 0.5855962 ]])
   """
   print(arr2.reshape(2,6)) #默认按行
   """
   [[0.40919593 0.53439411 0.17478334 0.88506119 0.52465668 0.40275561]
    [0.85389365 0.69344744 0.06308938 0.24195379 0.43457003 0.5855962 ]]
    """
   print(arr2.reshape(6,2,order='F')) #按列
   """
   [[0.40919593 0.17478334]
    [0.52465668 0.85389365]
    [0.06308938 0.43457003]
    [0.53439411 0.88506119]
    [0.40275561 0.69344744]
    [0.24195379 0.5855962 ]]
   """
   
   # np.reshape函数
   np.reshape(arr2,(-1,3)) # -1从数组的长度和其余维度推断该值
   """
   array([[0.40919593, 0.53439411, 0.17478334],
          [0.88506119, 0.52465668, 0.40275561],
          [0.85389365, 0.69344744, 0.06308938],
          [0.24195379, 0.43457003, 0.5855962 ]])
   """
   #在转换形状的时候，一定要注意元素的个数，不能发生改变！
   ```

2. `np.resize(a,new_shape)`:改变原数组的形状和大小，与`reshape`不同的是可以改变数组的`size`。如果新数组大于原始数组，则新数组将填充*a的*重复副本。

   | 参数      | 描述                       |
   | --------- | -------------------------- |
   | a         | array_like要重新整形的数组 |
   | new_shape | `int`或`int的tuple`        |

   `ndarray.resize(new_shape)`:就地更改数组的形状和大小，会对原值进行修改并且返回的是`None`

   ```python
   #ndarray.resize
   #缩小数组
   a = np.array([[0, 1], [2, 3]])
   a.resize(2,1)
   """
   array([[0],
          [1]])
          """
   #扩展数组 缺少的数据用 0 填充
   b = np.array([[0, 1], [2, 3]])
   b.resize(2,3)
   """
   array([[0, 1, 2],
          [3, 0, 0]])
   """
   
   #np.resize
   #缩小数组
   a=np.array([[0,1],[2,3]])
   np.resize(a(1,2))
   # array([[0, 1]])  a的值没有变化
   
   #扩展数组 缺少的数据将由填充原数组的重复副本
   b=np.array([[0,1],[2,3]])
   np.resize(b,(3,3))
   """
   array([[0, 1, 2],
          [3, 0, 1],
          [2, 3, 0]])
   """
   
   ```

3. .T:将原shape为（n，m）的数组转置为（m，n），把数组的行和列进行互换，一维数组转置不变。

   ```python
   arr3 = np.arange(12).reshape(3,4)
   arr3.T
   """
   array([[ 0,  4,  8],
          [ 1,  5,  9],
          [ 2,  6, 10],
          [ 3,  7, 11]])
   """
   ```

4. `ndarray.astype(type)`:强制转换为指定的类型。

   ```python
   one = np.ones((3,4))
   one
   """
   array([[1., 1., 1., 1.],
          [1., 1., 1., 1.],
          [1., 1., 1., 1.]])
   """
   one.dtype
   #dtype('float64')
   one.astype(np.int64)
   """
   array([[1, 1, 1, 1],
          [1, 1, 1, 1],
          [1, 1, 1, 1]], dtype=int64)
   """
   n1 = np.array(['1','2','3'],dtype=np.string_)
   n1.astype(np.int64)
   #array([1, 2, 3], dtype=int64)
   
   #如果将浮点数转为整数,那么小数部分会被截断
   n2 = np.random.uniform(1,5,size=(3,4))
   n2
   """
   array([[2.54847297, 1.47540363, 3.19716644, 2.88852565],
          [4.35936498, 4.14153717, 4.28468383, 2.98894034],
          [3.34067248, 2.73983194, 4.21287495, 1.30903491]])
   """
   n2.astype(np.int64)
   """
   array([[2, 1, 3, 2],
          [4, 4, 4, 2],
          [3, 2, 4, 1]], dtype=int64)
   """
   ```


