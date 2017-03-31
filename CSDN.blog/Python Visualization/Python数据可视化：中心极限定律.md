**中心极限定理**是研究独立随机变量和的极限分布为正态分布的问题。

设随机变量序列![这里写图片描述](http://img.blog.csdn.net/20160927135906792)  相互独立，均具有相同的数学期望与方差，即![这里写图片描述](http://img.blog.csdn.net/20160927135922339)  
令：![这里写图片描述](http://img.blog.csdn.net/20160927135936022)
则称随机变量![这里写图片描述](http://img.blog.csdn.net/20160927135949870)为随机变量序列![X1，X2,、、、，Xn](http://img.blog.csdn.net/20160927140002167)的规范和。

**中心极限定理：**设从均值为![μ](http://img.blog.csdn.net/20160927140015726)、方差为![σ^2](http://img.blog.csdn.net/20160927140024413);（有限）的任意一个总体中抽取样本量为n的样本，当n充分大时，样本均值的抽样分布近似服从均值为![μ](http://img.blog.csdn.net/20160927140036339)、方差为![σ^2/n](http://img.blog.csdn.net/20160927140124071) 的正态分布。

**【定理1】：(独立同分布的中心极限定理)** 设随机变量![这里写图片描述](http://img.blog.csdn.net/20160927141233517) 相互独立，具有相同的分布, ![这里写图片描述](http://img.blog.csdn.net/20160927141259932) 记：![这里写图片描述](http://img.blog.csdn.net/20160927141428924)
**【定理2】：**均值为![这里写图片描述](http://img.blog.csdn.net/20160927141446846) ，方差为![这里写图片描述](http://img.blog.csdn.net/20160927141457232) 的独立同分布的随机变量![这里写图片描述](http://img.blog.csdn.net/20160927141513170) 的和![这里写图片描述](http://img.blog.csdn.net/20160927141532409) 的标准化变量的分布函数，当![这里写图片描述](http://img.blog.csdn.net/20160927141619988) 充分大时，有![这里写图片描述](http://img.blog.csdn.net/20160927141645425)

代码实现：
```
	# Python
	# 中心极限定理
    u = 0  # 均值μ
    sig = math.sqrt(0.5)  # 标准差δ
    t = 10000
    a = np.zeros(1000)
    for i in range(t):
        a += np.random.uniform(-5, 5, 1000)  # random:返回随机的浮点数，在半开区间 [0.0, 1.0),uniform:均匀分布
    a = (a - u)/(sig/math.sqrt(t))
    plt.hist(a, bins=30, color='g', alpha=0.75)  # hist:绘制直方图
    plt.grid()
    plt.show()
```

![这里写图片描述](http://img.blog.csdn.net/20160927141828113)