# one-hot编码

**虚拟变量：他是人为虚设的变量,又称哑变量,通常取值为0或1.**在研究中有些变量是无法定量度量,如职业，性别

**one-hot编码**：就是将分类变量转换为机器学习算法易于利用的一种形式的过程。

**get_dummies**:*(data,prefix)*:

- data:DataFarame, Series, array_like
- prefix:追加DataFrame列名的字符串

```python
#一般get_dummies和cut等离散化函数结合使用
ages = [18,26,22,35,43,67,7,5,82]
arr1 = pd.Series(ages,index=list('abcdefghi'))
bins = [0,18,30,50,90]
#离散化
c1 = pd.cut(arr1,bins)
#one-hot编码矩阵
df1 = pd.get_dummies(c1)
df1
	(0, 18]		(18, 30]	(30, 50]	(50, 90]
a		1			0			0			0
b		0			1			0			0
c		0			1			0			0
d		0			0			1			0
e		0			0			1			0
f		0			0			0			1
g		1			0			0			0
h		1			0			0			0
i		0			0			0			1

```

