# Series

1. `Series`:一种一维标记的数组型对象，能够保存任何数据类型(int, str, float, python object...),包含了数据标签,称为索引。

   ![](C:\Users\唐禹\Desktop\数据分析-唐禹\series.png)

2. 创建`Series`的方法：

   1. 数组

   2. python 字典

3. ```python
   # 通过数组创建
   arr1 = np.arange(1,6)
   s1 = pd.Series(arr1)
   s1
   0    1
   1    2
   2    3
   3    4
   4    5
   dtype: int32
   #索引在左边，值在右边，当我们没有为数据指定索引，默认生成索引
   #默认生成的索引是从0到N-1(N是数据的长度)
   
   # values属性和index属性分别获取Series对象的值和索引
   s1.values
   array([1, 2, 3, 4, 5]) #值就是我们的array对象
   
   s1.index
   RangeIndex(start=0, stop=4, step=1) # 和rang(4)类似
   ```

4. 通常我们都是自己需要创建一个索引序列，用标签标示每个数据点。

   ```python
   #索引长度和数据长度必须相同。
   s2 = pd.Series([1,3,-4,8],index=['a','b','c','d'])
   s2
   a    1
   b    3
   c   -4
   d    8
   dtype: int64
     
   pd2.index
   Index(['a', 'b', 'c', 'd'], dtype='object')
   ```

5. python 字典创建Series

   ```python
   dict1 = {'name':'hah','age':18,"city":'cs'}
   s3 = pd.Series(dict1)
   s3
   name    hah
   age      18
   city     cs
   dtype: object
   #通过字典创建,Series的索引就是我们排序好的字典的键
   
   #也可以按照我们自己想要的顺序去指定索引
   s4 = pd.Series(dict1, index=['city','name','age','sex'])
   s4
   city     cs
   name    hah
   age      18
   sex     NaN
   dtype: object
   #前三行按照我们给定的顺序生成，但是sex并没有在字典的key中，它对应的值是NaN,
   # NaN是pandas中标记的缺失值
   ```

6. isnull 和 notnull 检查缺失值

   ```python
   s4.isnull() #判断是否为空,空就是True
   city    False
   name    False
   age     False
   sex      True
   dtype: bool
       
   s4.notnull() # 判断是否不为空,非空就是True
   city     True
   name     True
   age      True
   sex     False
   dtype: bool
   
   #返回一个Series对象
   ```

7. 索引和切片

   ```python
   s5 = pd.Series(np.random.rand(5),index=['a','b','c','d','e'])
   s5
   a    0.968340
   b    0.727041
   c    0.607197
   d    0.134053
   e    0.240239
   dtype: float64
     
   # 下标
   s5[1] #通过下标获取到元素，不能倒着取，和我们python列表不一样, s5[-1]错误的写法
   0.7270408328885498
   
   #通过标签名
   s5['c']
   0.6071966171492978
   
   #选取多个，还是Series
   s5[[1,3]] 或 s5[['b','d']]  # [1,3] 或['b','d']是索引列表
   b    0.727041
   d    0.134053
   dtype: float64
   
   #切片 标签切片包含末端数据（指定了标签）
   s5[1:3]
   b    0.727041
   c    0.607197
   dtype: float64
       
   s5['b':'d']
   b    0.727041
   c    0.607197
   d    0.134053
   dtype: float64
    
   #布尔索引
   s5[s5>0.5] #保留为True的数据
   a    0.968340
   b    0.727041
   c    0.607197
   dtype: float64
   ```

8. name属性

   ```python
   #Series对象本身和其本身索引都具有name属性
   s6 = pd.Series({'apple':7.6,'banana':9.6,'watermelon':6.8,'orange':3.6})
   s6.name = 'fruit_price'  # 设置Series对象的name属性
   s6.index.name = 'fruit'  # 设置索引name属性
   s6
   fruit
   apple         7.6
   banana        9.6
   watermelon    6.8
   orange        3.6
   Name: fruit_price, dtype: float64
           
   #查看索引
   s6.index
   Index(['apple', 'banana', 'watermelon', 'orange'], dtype='object', name='fruit')
   ```
