**正态分布（Normal distribution）又成为高斯分布（Gaussian distribution）**

若随机变量X服从一个数学期望为![这里写图片描述](http://img.blog.csdn.net/20160927105015395)、标准方差为![这里写图片描述](http://img.blog.csdn.net/20160927104934079)的高斯分布，记为：
![这里写图片描述](http://img.blog.csdn.net/20160927105127270)

则其概率密度函数为：
![这里写图片描述](http://img.blog.csdn.net/20160927105045846)

正态分布的期望值![这里写图片描述](http://img.blog.csdn.net/20160927105015395)决定了其位置，其标准差![这里写图片描述](http://img.blog.csdn.net/20160927105256239)决定了分布的幅度。因其曲线呈钟形，因此人们又经常称之为钟形曲线。我们通常所说的标准正态分布是![这里写图片描述](http://img.blog.csdn.net/20160927105212191)的正态分布：
![这里写图片描述](http://img.blog.csdn.net/20160927104815566)

###概率密度函数
![这里写图片描述](http://img.blog.csdn.net/20160927111150497)
![这里写图片描述](http://img.blog.csdn.net/20160927111639270)
代码实现：
```
	# Python实现正态分布
	# 绘制正态分布概率密度函数
    u = 0   # 均值μ
    u01 = -2
    sig = math.sqrt(0.2)  # 标准差δ
    sig01 = math.sqrt(1)
    sig02 = math.sqrt(5)
    sig_u01 = math.sqrt(0.5)
    x = np.linspace(u - 3*sig, u + 3*sig, 50)
    x_01 = np.linspace(u - 6 * sig, u + 6 * sig, 50)
    x_02 = np.linspace(u - 10 * sig, u + 10 * sig, 50)
    x_u01 = np.linspace(u - 10 * sig, u + 1 * sig, 50)
    y_sig = np.exp(-(x - u) ** 2 /(2* sig **2))/(math.sqrt(2*math.pi)*sig)
    y_sig01 = np.exp(-(x_01 - u) ** 2 /(2* sig01 **2))/(math.sqrt(2*math.pi)*sig01)
    y_sig02 = np.exp(-(x_02 - u) ** 2 / (2 * sig02 ** 2)) / (math.sqrt(2 * math.pi) * sig02)
    y_sig_u01 = np.exp(-(x_u01 - u01) ** 2 / (2 * sig_u01 ** 2)) / (math.sqrt(2 * math.pi) * sig_u01)
    plt.plot(x, y_sig, "r-", linewidth=2)
    plt.plot(x_01, y_sig01, "g-", linewidth=2)
    plt.plot(x_02, y_sig02, "b-", linewidth=2)
    plt.plot(x_u01, y_sig_u01, "m-", linewidth=2)
    # plt.plot(x, y, 'r-', x, y, 'go', linewidth=2,markersize=8)
    plt.grid(True)
    plt.show()
```