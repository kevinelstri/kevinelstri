```
# -*-coding:utf-8-*-

import numpy as np
import pandas as pd
"""
    Series
"""

"""
    Series
    它是一个一维的标记阵列，可以容纳任何的数据类型（整型、字符串、浮点数、python对象），
    轴标签统称为索引，轴就是纵向的。
    最基本的创建Series序列：s = pd.Series(data, index=index)
    data可以表示许多不同的事：a python dict,an ndarray, a scalar value(标量数值，如5)
    索引就是轴标签的一个列表，如果data是一个ndarray，index的长度也必须和data长度相等。
"""
"""
    Series from ndarray
    如果data是一个ndarray，index的长度也必须和data长度相等
"""
s = pd.Series(np.random.randn(5), index=['a', 'b', 'c', 'd', 'e'])  # 指定索引为[a,b,c,d,e]
print s
print s.index
print pd.Series(np.random.randn(5))  # 未指定索引，自动添加索引为[0,1,...len(data)-1]
"""
    Series from dict
    如果data是一个dict
"""
d = {'a': 0., 'b': 1., 'c': 2.}
print pd.Series(d)
print pd.Series(d, index=['b', 'c', 'e', 'a', 'd'])
"""
    在pandas中，NaN是标准缺失数据
"""
"""
    Series from scalar
    如果data是一个scalar，index必须要提供，scalar值将会重复匹配到index索引的长度
"""
s = pd.Series(5., index=['b', 'c', 'e', 'a', 'd'])
print s
"""
    Series is ndarray-like
    Series行为与ndarray非常相似，可以有效的使用numpy的功能，同时，也可以进行切片索引
"""
s = pd.Series(np.random.randn(5), index=['a', 'b', 'c', 'd', 'e'])
print s[0]
print s[:3]
print s[s > s.median()]
print s[[4, 3, 2]]
print np.exp(s)
print '-----------------------------------'
"""
    Series is dict-like
    一个Series就像一个固定大小的词典，可以通过index标签来获取和设置值。
"""
print s['a']
s['e'] = 12
print s
print 'e' in s
print 'f' in s
print s.get('f')  # 使用get()方法来获取Series中某个标签的值，若标签不存在，返回None
print s.get('e')
print '-----------------------------------'

"""
    Vectorized operations and label alignment with Series
    矢量化操作和序列标签对齐
    数据分析过程中，原生的numpy数组遍历序列值的功能通常是不必要的，Series就可以实现numpy的大多数功能。
"""
print s+s
print s*2
print np.exp(s)
print s[1:]+s[:-1]
print '----------------------------------------------'
"""
    Series和numpy之间的关键区别就是：Series的自动化对齐操作是基于标签的数据。
    因此，你可以进行计算，而不需要考虑Series是否有相同的标签。
"""

"""
    Name attribute 名称属性
    Series也可以有名字属性
    Series的名字在许多案例中可以自动被设置，特别是DataFrame操作的是一维数据。
"""
s = pd.Series(np.random.randn(5), name='something')
print s
print s.name
"""
    pandas.Series.rename()方法
"""
s2 = s.rename('different')
print s2.name

```