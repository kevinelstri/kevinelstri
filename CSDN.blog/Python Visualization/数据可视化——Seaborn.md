```
# -*-coding:utf-8-*-

import numpy as np
import matplotlib as mpl
import matplotlib.pyplot as plt

np.random.seed(sum(map(ord, 'aesthetics')))


def sinplot(flip=1):
    x = np.linspace(0, 14, 100)
    for i in range(1, 7):
        plt.plot(x, np.sin(x + i * .5) * (7 - i) * flip)


sinplot()
plt.show()

import seaborn as sns

sinplot()
plt.show()
"""
    Seaborn 默认浅灰色背景与白色网格线
    seaborn将matplotlib的参数划分为两个组，第一组控制图表的样式，第二组控制图的度量尺度元素
    控制样式：axes_style()  set_style()  返回一系列的参数
    度量图：plotting_context()  set_context() 设置matplotlib的默认属性
"""
"""
    图样式方法axes_style()和set_style():
        5种seaborn主题形式：darkgrid, whitegrid, dark, white, ticks, 默认为darkgrid
            whitegrid:白色网格
            dark:灰底
            white:白底
            ticks:刻度
    用despline()方法去掉图表中de各种轴：
    with语句临时设置图表样式
"""
# 白色网格
sns.set_style('whitegrid')
sinplot()
plt.show()

# 灰底
sns.set_style('dark')
sinplot()
plt.show()

# 白底
sns.set_style('white')
sinplot()
plt.show()

# 刻度
sns.set_style('ticks')
sinplot()
plt.show()

# 去掉顶部刻度
sinplot()
sns.despine()
plt.show()

# 箱线图
# 去掉y轴
sns.set_style('whitegrid')
data = np.random.normal(size=(20, 6)) + np.arange(6) / 2
sns.boxplot(data=data)
plt.show()

sns.set_style('whitegrid')
sns.boxplot(data=data, palette='deep')
sns.despine(left=True)
plt.show()

# matplotlib中subplot()方法使用
for idx in range(6):
    plt.subplot(321 + idx)
plt.show()

# 两图叠加
with sns.axes_style('darkgrid'):
    plt.subplot(211)
    sinplot()
plt.subplot(212)
sinplot(-1)
plt.show()

"""
    seaborn颜色设置
"""
import numpy as np
import seaborn as sns
import matplotlib.pyplot as plt

sns.set(rc={'figure.figsize': (6, 6)})
np.random.seed(sum(map(ord, 'palettes')))

"""
    无渐变调色板
"""
# 默认分类调色板
current_palette = sns.color_palette()
sns.palplot(current_palette)
plt.show()

# 调色板颜色循环
sns.palplot(sns.color_palette('hls', 8))
plt.show()

# 亮度和饱和度
sns.palplot(sns.hls_palette(8, l=.3, s=.8))
plt.show()

# 人性化的HUSL
sns.palplot(sns.color_palette('husl', 8))
plt.show()

"""
    渐变调色板
"""
# 浅色渐变深色
sns.palplot(sns.color_palette('Blues'))
plt.show()
# 深色渐变浅色
sns.palplot(sns.color_palette('BuGn_r'))
plt.show()


# 定义正弦波函数
# set_palette()方法改变默认调色板
def sinplot(flip=1):
    x = np.linspace(0, 14, 100)
    for i in range(1, 7):
        plt.plot(x, np.sin(x + i * .5) * (7 - i) * flip)

# 使用seaborn的husl系统渲染图
sns.set_palette('husl')
sinplot()
plt.show()

"""
    可视化绘图
    seaborn中最便捷的方式就是构造一个单变量分布使用distplot()方法，默认情况下，它会绘出矩形图（histogram）或核密度估计（KDE）
"""
import numpy as np
import pandas as pd
from scipy import stats, integrate
import matplotlib.pyplot as plt

import seaborn as sns
sns.set(color_codes=True)
np.random.seed(sum(map(ord, 'distributions')))

# 使用np.random.normal随机抽样生成正太分布数据
x = np.random.normal(size=100)
sns.distplot(x)
plt.show()

# 矩形图-直方图
sns.distplot(x, kde=False, rug=True)
plt.show()

sns.distplot(x, bins=20, kde=False, rug=True)
plt.show()

# 核密度估计（KDE）
sns.distplot(x, hist=False, rug=True)
plt.show()

# 绘制二维分布
# 生成多维正态分布数据
mean, cov = [0, 1], [(1, .5), (.5, 1)]
data = np.random.multivariate_normal(mean, cov, 200)
df = pd.DataFrame(data, columns=['x', 'y'])
print df

# 散点图
sns.jointplot(x='x', y='y', data=df)
# 六边形图
x, y= np.random.multivariate_normal(mean, cov, 1000).T
with sns.axes_style('white'):
    sns.jointplot(x=x, y=y, kind='hex', color='k')

# 核密度估计
sns.jointplot(x='x', y='y', data=df, kind='kde')
plt.show()

"""
    可视化的线性关系
"""
# 导入各个模块
import numpy as np
import pandas as pd
import matplotlib as mpl
import matplotlib.pyplot as plt

import seaborn as sns
sns.set(color_codes=True)
np.random.seed(sum(map(ord, 'regression')))

# 导入seaborn自带数据
tips = sns.load_dataset('tips')
print tips

# 绘制线性回归模型函数
# seaborn中有两个方法通过回归用于可视化线性关系：regplot(),lmplot()
"""
    regplot():接受的x和y变量的格式包括简单的numpy arrays, pandas series objects or pandas DataFrame object
    lmplot():必须有参数设置，并且x和y必须是字符串

"""
# 不同种类的模型
# 对tips数据使用regplot()方法进行可视化
sns.regplot(x='total_bill', y='tip', data=tips)
plt.show()

# 对tips数据使用lmplot()方法进行可视化
sns.lmplot(x='total_bill', y='tip', data=tips)
plt.show()

# 线性回归拟合
# 以size为横坐标
sns.lmplot(x='size', y='tip', data=tips)
plt.show()

sns.lmplot(x='size', y='tip', data=tips, x_jitter=.05)
plt.show()

sns.lmplot(x='size', y='tip', data=tips, x_estimator=np.mean)
plt.show()



```