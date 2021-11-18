# DateFrame

1. `DateFrame`:一个二维标记数据结构，具有可能不同类型的列，每一列可以是不同值类型(数值，字符串，布尔值)，既有行索引也有列索引。我们可以把它看作为excel表格，或者SQL表，或Series对象的字典。

2. 构建`DateFrame`的方法:

   字典类：数组、列表或元组构成的字典构造dataframe，Series构成的字典构造dataframe， 字典构成的字典构造dataframe

   列表类:2D ndarray 构造dataframe，字典构成的列表构造dataframe，Series构成的列表构造dataframe

3. 查看数据 `head()`，`tail()`

   ```python
   pd5 = pd.DataFrame(np.arange(20).reshape(10,2))
   pd5
   	0	1
   0	0	1
   1	2	3
   2	4	5
   3	6	7
   4	8	9
   5	10	11
   6	12	13
   7	14	15
   8	16	17
   9	18	19
   
   # head()默认查看前5行，输入参数N，就查看前N行
   pd5.head()
   	0	1
   0	0	1
   1	2	3
   2	4	5
   3	6	7
   4	8	9
   
   #tail()默认查看后5行,输入参数N，就查看后N行
   pd5.tail()
   	0	1
   5	10	11
   6	12	13
   7	14	15
   8	16	17
   9	18	19
   ```

4. .T

   ```python
   #和Numpy一样，进行转置
   pd6 = pd.DataFrame(np.arange(4).reshape(2,2),index=['a','b'],columns=['A','B'])
   pd6
   	A	B
   a	0	1
   b	2	3
   
   pd6.T #行和列进行转置
   	a	b
   A	0	2
   B	1	3
   ```

5. 数组、列表或元组构成的字典构造dataframe

   ```python
   #构造一个字典
   data = {'a':[1,2,3,4],
           'b':(5,6,7,8),
           'c':np.arange(9,13)}
   #构造dataframe
   frame = pd.DataFrame(data)
   frame
   	a	b	c
   0	1	5	9
   1	2	6	10
   2	3	7	11
   3	4	8	12	
   
   #index属性查看行索引
   frame.index
   RangeIndex(start=0, stop=4, step=1)
   #columns属性查看列索引
   frame.columns
   Index(['a', 'b', 'c'], dtype='object')
   #values属性查看值
   frame.values
   array([[ 1,  5,  9],
          [ 2,  6, 10],
          [ 3,  7, 11],
          [ 4,  8, 12]], dtype=int64)
   # 每个序列是DateFrame的一列，所有的序列长度必须相等，columns为字典的key,index为默认的数字标签，我们可以通过index属性进行修改
   
   #指定index
   frame = pd.DataFrame(data,index=['A','B','C','D'])
   frame
   	a	b	c
   A	1	5	9
   B	2	6	10
   C	3	7	11
   D	4	8	12
   
   #指定columns，显示所指定列的数据，并按指定的顺序进行排序,当没有数据中没有该列('e')，那么就会用NaN来填充
   frame = pd.DataFrame(data,index=['A','B','C','D'],columns=['a','b','c','e'])
   frame
   	a	b	c	e
   A	1	5	9	NaN
   B	2	6	10	NaN
   C	3	7	11	NaN
   D	4	8	12	NaN
   ```

6. 2D ndarray 构造dataframe

   ```python
   #构造二维数组对象
   arr1 = np.arange(12).reshape(4,3)
   #构造dateframe
   frame1 = pd.DataFrame(arr1)
   frame1
   	0	1	2
   0	0	1	2
   1	3	4	5
   2	6	7	8
   3	9	10	11
   #我们通过二维数组对象创建dataframe，行索引和列索引都是可选参数，指定index和columns必须和原数组长度一致，默认0到N-1
   frame2 = pd.DataFrame(arr1,index=['a','b','c','d'],columns=['A','B','C'])
   frame2
   	A	B	C
   a	0	1	2
   b	3	4	5
   c	6	7	8
   d	9	10	11
   ```

7. Series构成的字典构造dataframe

   ```python
   pd1 = pd.DataFrame({'a':pd.Series(np.arange(3)),
                      'b':pd.Series(np.arange(3,5)), 
                      })
   pd1
   	a	b	
   0	0	4	
   1	1	5	
   2	2	NaN	
   
   #设置index,
   pd1 = pd.DataFrame({'a':pd.Series(np.arange(3),index=['a','b','c']),
                      'b':pd.Series(np.arange(3,5),index=['a','b']),
                      })
   pd1
   	a	b
   a	0	3.0
   b	1	4.0
   c	2	NaN
   #我们用Series构成的字典创建dataframe，指定索引我们需要在Series里面指定索引,index为Series的标签，Series长度可以不一样，会以NaN填充
   ```

8. 字典构成的字典构造dataframe

   ```python
   #字典嵌套
   data = {
       'a':{'apple':3.6,'banana':5.6},
       'b':{'apple':3,'banana':5},
       'c':{'apple':3.2}
   }
   #构造dataframe
   pd2 = pd.DataFrame(data3)
   pd2
   		a	b	c
   apple	3.6	3	3.2
   banana	5.6	5	NaN
   #内部字典是一列,内部字典的key是行索引index,外部字典的key是列索引columns,
   ```

9. 字典构成的列表构造dataframe

   ```python
   l1 = [{'apple':3.6,'banana':5.6},{'apple':3,'banana':5},{'apple':3.2}]
   pd3 = pd.DataFrame(l1)
   pd3
   	apple	banana
   0	3.6		5.6
   1	3.0		5.0
   2	3.2		NaN
   #列表中的每一个元素是一行,字典的key是列索引columns
   
   #指定行索引index,必须和数据长度一致
   pd3 = pd.DataFrame(l1,index=['a','b','c'])
   pd3
   	apple	banana
   a	3.6		5.6
   b	3.0		5.0
   c	3.2		NaN
   ```

10. Series构成的列表构造dataframe

    ```python
    l2 = [pd.Series(np.random.rand(3)),pd.Series(np.random.rand(2))]
    pd4=pd.DataFrame(l2)
    pd4
    	0			1			2
    0	0.482106	0.025374	0.020586
    1	0.912417	0.229153	NaN
    #列表中的每一个元素是一行
    #设置行索引index,和原数组长度一致
    pd4=pd.DataFrame(l2,index=['a','b'])
    pd4
    	0			1			2
    a	0.482106	0.025374	0.020586
    b	0.912417	0.229153	NaN
    #设置列索引columns,我们需要在series对象设置index
    l2 = [pd.Series(np.random.rand(3),index=['A','B','C']),pd.Series(np.random.rand(2),index=['A','B'])]
    
    pd4=pd.DataFrame(l2,index=['a','b'])
    pd4
    
    	  A			  B			 C
    a	0.999713	0.507880	0.091274
    b	0.798486	0.268391	NaN
    ```


