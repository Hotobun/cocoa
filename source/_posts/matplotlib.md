---
title: Matplotlib
date: 2020-1-06 23:01:01
tags: 
- Matplotlib
categories:
cover: /img/matplotlib.jpg
---

## 第一个Matplotlib程序
``` python
import matplotlib.pyplot as plt 
 
plt.plot([3,1,4,5,2])   
plt.ylabel("Grade")     # 标签名
plt.savefig("test",dpi=600) 
```
* savefig 参数:
  * filename : 保存的文件名 默认是png 也可以指定格式保存
  * dpi: 输出文件的质量 每一英尺空间中包含点的数量
可以查看输出的`test.png`图像
![matplotlib1](/img/archive_img/matplotlib1.png)


#### 输入多个列表
``` python
import matplotlib.pyplot as plt 
 
plt.plot([0,2,4,6,8],[3,1,4,5,2])   
plt.ylabel("Grade")     # 标签名
plt.axis([-1,10,0,6])
plt.savefig("test1",dpi=600)
```
* plot参数：
  * 当有多个列表时 分别对应x轴与y轴的点
  * XY: (0,3) (2,1) (4,4) (6,5) (8,2)
* axis参数:
  *  需要4个变量的列表 对应画图区域
  *  x轴起始于-1 终止与10
  *  y轴起始于0 终止与6
![matplotlib2](/img/archive_img/matplotlib2.png)

*** 
## pyplot的绘图区域
分隔绘图区域使用函数subplot
* plt.subplot(nrows, ncols, plot_number)
  * 3个参数都是int类型
  * nrows: 横轴数量
  * ncols: 纵轴数量
  * plot_number: 绘图子区域编号 所有绘图都在这个子区域进行
  * 由于全是数字可以简写一个参数 plt.subplot(3,2,4) 可以简写为 plt.subplot(324)


``` python 
import matplotlib.pyplot as plt 
import numpy as np 
 
def f(t):
    return np.exp(-t) * np.cos(2*np.pi*t)
 
if __name__ == "__main__":
    a = np.arange(0.0, 5.0, 0.02)
    plt.subplot(211)        # 将绘图区域分为2行1列 选择第一块
    plt.plot(a, f(a))
 
    plt.subplot(2,1,2)      # 将绘图区域选择为2行1列的第二块
    plt.plot(a, np.cos(2*np.pi*a), 'r--') # r-- 表示虚线绘制
    plt.show()
```
![matplotlib3](/img/archive_img/matplotlib3.png)

*** 
## plot函数
* plt.plot(x, y, fromat_string, **kwargs)
  * x : X轴数据, 列表或数组, 可选。
  * y : Y轴数据, 列表或数组.
  * format_string : 控制曲线的格式字符串, 可选。
  * **kwargs : 第二组或更多(x, y, fromat_string) 
  * 当绘制多条曲线时, x不能省略

尝试画4条曲线
```python
import matplotlib.pyplot as plt 
import numpy as np 
 
if __name__ == "__main__":
    a = np.arange(10)
    plt.plot(a, a*1.5,a, a*2.5, a, a*3.5, a, a*4.5) # 注意这里是8个参数 每两个一组
    plt.show()
```

![matplotlib4](/img/archive_img/matplotlib4.png)

format_string 参数由颜色字符、风格字符和标记字符组成  
如果不选择颜色 Matplotlib会为不同曲线选择唯一的颜色区分

颜色字符|说明|颜色字符|说明 
:--|:--|:--|:--
'b'|蓝色|'m'|洋红色magenta
'g'|绿色|'y'|黄色
'r'|红色|'k'|黑色
'c'|青绿色|'w'|白色
'#123321'|用户控制颜色|0.8|灰度值字符串


风格字符|说明 
:--|:--
'\-'|实线
'\-\-'|破折线
'-.'|点划线
':'|虚线
''|无线条

标记字符|说明 |标记字符|说明 |标记字符|说明 |
:--|:--|:--|:--|:--|:--
'.'|点标记|'1'|下花三角标记|'h'|竖六边形标记
','|像素点标记(极小)|'2'|上花三角标记|'H'|横六边形标记
'o'|实心圈标记|'3'|左花三角标记|'+'|十字标记
'v'|倒三角标记|'4'|右花三角标记|'x'|x标记
'^'|上三角标记|'s'|实心方形标记|'D'|棱形标记
'>'|右三角标记|'p'|实心五角标记|'d'|廋棱形标记
'<'|左三角标记|'*'|星型标记|'\|'|竖线标记

![matplotlib5](/img/archive_img/matplotlib5.png)

下面遍历一次所有标记符号的样式
``` python
import matplotlib.pyplot as plt 
import numpy as np 
  
def main():
    color = 'bgrcmyk'
    line = ['-','--','-.',':']
    markers = '.,ov^><1234sp*hH+xDd|_'
    for i in range(len(markers)): 
        format_string = '{}{}{}'.format(color[i%len(color)], line[i%len(line)], markers[i])
        print("y -> format_string: {:>2d} -> {:4s} ".format(i+1,format_string) \
            if i%2 == 0 else "{:>5d} -> {} \n".format(i+1,format_string), end='')
        plt.plot(np.arange(len(markers)), np.full(len(markers),i+1), format_string)
    plt.axis([0,len(markers),0,len(markers)+1])
    plt.show()
 
if __name__ == "__main__":
    main()
 
""" out  # 无线条和白色线没有入队 因为看不到啊
y -> format_string:  1 -> b-.      2 -> g--,
y -> format_string:  3 -> r-.o     4 -> c:v
y -> format_string:  5 -> m-^      6 -> y-->
y -> format_string:  7 -> k-.<     8 -> b:1
y -> format_string:  9 -> g-2     10 -> r--3
y -> format_string: 11 -> c-.4    12 -> m:s
y -> format_string: 13 -> y-p     14 -> k--*
y -> format_string: 15 -> b-.h    16 -> g:H
y -> format_string: 17 -> r-+     18 -> c--x
y -> format_string: 19 -> m-.D    20 -> y:d
y -> format_string: 21 -> k-|     22 -> b--_
"""
```
 
![matplotlib6](/img/archive_img/matplotlib6.png)