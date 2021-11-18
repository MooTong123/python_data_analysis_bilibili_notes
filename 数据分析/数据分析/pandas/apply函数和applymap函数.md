# apply函数和applymap函数

1. `apply(func,axis)`:将函数`func`应用到一行或一列的一维数组上

   ```python
   #dataframe的apply
   #构造一个dataframe
   df1 = pd.DataFrame({'Tom':{'English':88,'Math':68},
                     'Joke':{'English':68,'Math':98},
                     'Mabuqi':{'English':58,'Math':48},
                     'Ohio':{'English':48,'Math':78}})
   
   df1
   	    Tom	Joke Mabuqi	Ohio
   English	88	 68	  58	  48
   Math	68	 98	  48	  78
   #现在我有两个需求,一个分别求每个学生成绩的平均分,一个是求每科成绩的平均分，想想怎么计算?
   #1.求每个学生的平均分
   f1 = lambda x: x.mean()
   df1.apply(f1)
   Tom       78.0
   Joke      83.0
   Mabuqi    53.0
   Ohio      63.0
   dtype: float64
   #2.求每科的平均分，指定我们的轴axis='columns'或axis=1
   df1.apply(f1,axis='columns')
   English    65.5
   Math       73.0
   dtype: float64
   #dataframe的apply函数，他接收的参数是一个series对象
       
   #Series
   s1 = pd.Series(['Tom','Joke','Mabuqi','Ohio'])
   s1
   0       Tom
   1      Joke
   2    Mabuqi
   3      Ohio
   dtype: object
   #需求，过滤掉名字长度<3的人
   f2 = lambda x: len(x)>3
   s1.apply(f2) #这样我们得到一个布尔类型的series
   0    False
   1     True
   2     True
   3     True
   dtype: bool
       
   s1[s1.apply(f)] #这样我们就过滤掉了名字长度小于3的人
   1      Joke
   2    Mabuqi
   3      Ohio
   dtype: object 
   #series的appl函数，他接收的参数是series里面的各个值
   ```

2. `applymap(func)`将函数应用到`dataframe`每一个元素上

   ```python
   df2 = pd.DataFrame(np.random.rand(4,3))
   df2
   
   	0			1			2
   0	0.386162	0.178801	0.283059
   1	0.386132	0.765665	0.256415
   2	0.829829	0.052328	0.344845
   3	0.849074	0.949973	0.306215
   #需求，这些数据我只要保留两位小数,怎么做？
   f3 = lambda x:'%.2f' % x
   df2.applymap(f2)
   	0		1		2
   0	0.39	0.18	0.28
   1	0.39	0.77	0.26
   2	0.83	0.05	0.34
   3	0.85	0.95	0.31
   ```

3. 总结:

   - DataFrame的`applymap()`和Series的`apply()`方法，都是接收的对象的各个值，进行处理
   - DataFrame的`apply()`接收的是series,DataFrame里面的行或列