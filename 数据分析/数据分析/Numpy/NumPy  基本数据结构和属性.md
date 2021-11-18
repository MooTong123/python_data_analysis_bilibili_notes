# NumPy  基本数据结构和属性

1. `Numpy`是`Python`科学计算库,用于快速处理任意维度的数组

2. `NumPy`提供一个**N维数组类型ndarray**，它描述了**相同类型**的“items”的集合。

3. `ndarray`支持向量化运算

4. `NumPy`使用c语言写的，底部解除了`GIL`，其对数组的操作速度不在受`python`解释器限制

5. **ndarray**属性

   | 属性             | 描述                     |
   | ---------------- | ------------------------ |
   | ndarray.shape    | 数组维度的元组           |
   | ndarray.ndim     | 数组维数                 |
   | ndarray.size     | 数组中的元素数量         |
   | ndarray.itemsize | 一个数组元素的长度(字节) |
   | ndarray.dtype    | 数组元素的类型           |

6. ```python
   import numpy as np
   
   a = np.array([1,2,3])
   b = np.array([[1,2,3],[4,5,6]])
   c = np.array([[[1,2],[3,4]], [[5,6],[7,8]]])
   #shape表示数组的形状
   #a.shape ---> (3,) 一维数组
   #b.shape --->(2,3)二维数组 2行3列
   #c.shape --->(2,2,2)三维数组
   
   #ndim表示数组的维度
   #a.ndim ---> 1
   #b.ndim ---> 2
   #c.ndim ---> 3
   
   #size表示数组中的元素数量
   #a.size ---> 3
   #b.size ---> 6
   #c.size ---> 8
   
   #dtype表示元组元素的类型
   #a.dtype ---> dtype('int32')
   #b.dtype ---> dtype('int32')
   #c.dtype ---> dtype('int32')
   ```

7. `ndarray`元素数据类型

   `ndarray.dtype`查看数组元素的数据类型,`NumPy`支持比`Python`更多的数值类型

   | 数据类型   | 描述                                                        | 唯一标识符 |
   | ---------- | ----------------------------------------------------------- | ---------- |
   | bool       | 用一个字节存储的布尔类型（True或False）                     | 'b'        |
   | int8       | 一个字节大小，-128 至 127                                   | 'i'        |
   | int16      | 整数，16 位整数(-32768 ~ 32767)                             | 'i2'       |
   | int32      | 整数，32 位整数(-2147483648 ~ 2147483647)                   | 'i4'       |
   | int64      | 整数，64 位整数(-9223372036854775808 ~ 9223372036854775807) | 'i8'       |
   | uint8      | 无符号整数，0 至 255                                        | 'u'        |
   | uint16     | 无符号整数，0 至 65535                                      | 'u2'       |
   | uint32     | 无符号整数，0 至 2 ** 32 - 1                                | 'u4'       |
   | uint64     | 无符号整数，0 至 2 ** 64 - 1                                | 'u8'       |
   | float16    | 半精度浮点数：16位，正负号1位，指数5位，精度10位            | 'f2'       |
   | float32    | 单精度浮点数：32位，正负号1位，指数8位，精度23位            | 'f4'       |
   | float64    | 双精度浮点数：64位，正负号1位，指数11位，精度52位           | 'f8'       |
   | complex64  | 复数，分别用两个32位浮点数表示实部和虚部                    | 'c8'       |
   | complex128 | 复数，分别用两个64位浮点数表示实部和虚部                    | 'c16'      |
   | object_    | python对象                                                  | 'O'        |
   | string_    | 字符串                                                      | 'S'        |
   | unicode_   | unicode类型                                                 | 'U'        |

   `NumPy`的数值类型实际上是 `dtype `对象的实例，并对应唯一的字符，包括 `np.bool_`，`np.int32`，`np.float32`，等等。

   ```python
   import numpy as np
   d = np.dtype(np.int32)
   print(d) ---> int32
   ```

   ```python 
   # 创建数组指定数据类型
   e = np.array([[1,2],[3,4]],dtype=np.float32)
   e ---> array([[1., 2.],
          [3., 4.]], dtype=float32)
   
   f = np.array([[1,2],[3,4]],dtype=np.dtype('f4'))
   f ---> array([[1., 2.],
          [3., 4.]], dtype=float32)
   
   
   ```

   ```python
   # 创建结构化数据类型
   
   # 1. 创建数据类型
   dt = np.dtype([('price','f4')]) # price 类型的字段名，自定义, 'f4'数据类型 float32
   
   # 2. 将数据类型应用到 ndarray对象
   nd = np.array([(10),(25.8),(36.6)], dtype=dt)
   nd ---> array([(10. ,), (25.8,), (36.6,)], dtype=[('price', '<f4')])
   #创建数组中不同的数据类型数组
   dt = np.dtype([('name','S20'), ('price', 'f4'),
                  ('weight', 'i1')])
   nd = np.array([('meat', 15.6, 2),('apple', 6, 2)],dtype=dt)
   ```


