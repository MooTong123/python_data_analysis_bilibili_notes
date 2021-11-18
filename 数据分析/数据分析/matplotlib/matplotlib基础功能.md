# matplotlib基础功能

- *在前面我们已经知道了matplotlib图的结构,下面我们着重于matplotlib的辅助显示，颜色，标记，线类型，刻度，标签，图例，以及图片保存*

- *模拟股票10分钟的变化趋势*

  -  *画出股票趋势图*

    ```python
    import numpy as np
    import pandas as pd 
    import matplotlib.pyplot as plt
    
    #1)准备数据
    x = range(1,11) #股票10分钟
    y = np.random.normal(size=10) #正态分布随机生成10个数据
    
    #2)创建画布
    fig = plt.figure(figsize=(16,6),dpi=100) #设置大小，设置dpi
    
    #3)绘制折线图
    plt.plot(x,y)
    
    #4)显示图像
    plt.show() #show方法会释放figure资源
    ```

    ![](C:\Users\唐禹\Desktop\数据分析-唐禹\matplotlib\图\基础1.png)

  - 设置刻度标签，设置刻度值

    *plt.xticks(x，**kwargs)*:*x:显示的刻度值*

    *plt.yticks(y，**kwargs)*:*y:显示的刻度值*

    ```python
    #构造刻度标签
    x_ticks_label = ['10点{}分'.format(i) for i in x]
    
    plt.xticks(x,x_ticks_label,rotation=45) #rotation:将刻度标签旋转多少度
    ```

    ![](C:\Users\唐禹\Desktop\数据分析-唐禹\matplotlib\图\基础2.png)

  - 设置轴标签，标题

    ```python
    #设置x,y轴标签
    plt.xlabel('时间') 
    plt.ylabel('涨幅')
    
    #设置图像标题
    plt.title('股票10分中的涨幅')
    ```

    ![](C:\Users\唐禹\Desktop\数据分析-唐禹\matplotlib\图\基础3.png)

  - 设置颜色，标记和线类型

    ```python
    #设置颜色color
    #设置线类型linestyle
    #设置标记marker
    plt.plot(x,y,color='r',linestyle='--',marker='o')
    ```

    ![](C:\Users\唐禹\Desktop\数据分析-唐禹\matplotlib\图\基础.png)

  - 显示图例

    *可能我们在一个绘图区，需要绘制多个图形，多次plot就可以解决*

    ```python
    #在添加一条数据
    y_B = np.random.normal(size=10)
    
    #进行绘制
    #plt.plot(x,y_B,color='b',marker='o')
    
    #添加图例
    #显示图例我们需要先加上label标签
    plt.plot(x,y,color='r',linestyle='--',marker='o',label='A')
    plt.plot(x,y_B,color='b',marker='o',label='B')
    plt.legend(loc='best')
    
    #添加网格显示
    plt.grid(True,linestyle='--',alpha=1) #appha：透明度
    ```

    ![](C:\Users\唐禹\Desktop\数据分析-唐禹\matplotlib\图\图5.png)

- *常见颜色*

  | 标识 | 描述 |
  | :--: | :--: |
  |  r   | 红色 |
  |  g   | 绿色 |
  |  b   | 蓝色 |
  |  w   | 白色 |
  |  c   | 青色 |
  |  m   | 洋红 |
  |  y   | 黄色 |
  |  k   | 黑色 |

- *常见线类型*

  | 标识 |  描述  |
  | :--: | :----: |
  |  -   |  实线  |
  |  --  |  虚线  |
  |  -.  | 点划线 |
  |  ：  | 点虚线 |
  |  ‘’  |  空格  |

- *常见标记*

  | 标识 |         描述          |
  | :--: | :-------------------: |
  | '.'  |     point marker      |
  | ','  |     pixel marker      |
  | 'o'  |     circle marker     |
  | 'v'  | triangle_down marker  |
  | '^'  |  triangle_up marker   |
  | '<'  | triangle_left marker  |
  | '>'  | triangle_right marker |
  | '1'  |    tri_down marker    |
  | '2'  |     tri_up marker     |
  | '3'  |    tri_left marker    |
  | '4'  |   tri_right marker    |
  | 's'  |     square marker     |
  | 'p'  |    pentagon marker    |
  | '*'  |      star marker      |
  | 'h'  |    hexagon1 marker    |
  | 'H'  |    hexagon2 marker    |
  | '+'  |      plus marker      |
  | 'x'  |       x marker        |
  | 'D'  |    diamond marker     |
  | 'd'  |  thin_diamond marker  |
  | '\|' |     vline marker      |
  | '_'  |     hline marker      |

- *显示图例位置*

  | 位置的字符串 | 位置的标识 |
  | :----------: | :--------: |
  |     best     |     0      |
  | upper right  |     1      |
  |  upper left  |     2      |
  |  lower left  |     3      |
  | lower right  |     4      |
  |    right     |     5      |
  | center left  |     6      |
  | center right |     7      |
  | lower center |     8      |
  | upper center |     9      |
  |    center    |     10     |


