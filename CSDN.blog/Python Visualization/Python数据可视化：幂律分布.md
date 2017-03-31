1、公式推导
对幂律分布公式：
![这里写图片描述](http://img.blog.csdn.net/20160927232416780)
对公式两边同时取以10为底的对数：
![这里写图片描述](http://img.blog.csdn.net/20160927232431577)
令![这里写图片描述](http://img.blog.csdn.net/20160927232440905)，且![这里写图片描述](http://img.blog.csdn.net/20160927232450171)为常数，所以公式变为：![这里写图片描述](http://img.blog.csdn.net/20160927232500699)
所以对于幂律公式，对X,Y取对数后，在坐标轴上为线性方程。

2、可视化
从图形上来说，幂律分布及其拟合效果：
![这里写图片描述](http://img.blog.csdn.net/20160927232603015)
对X轴与Y轴取以10为底的对数。效果上就是X轴上1与10，与10与100的距离是一样的。
![这里写图片描述](http://img.blog.csdn.net/20160927232628669)
对XY取双对数后，坐标轴上点可以很好用直线拟合。所以，判定数据是否符合幂律分布，只需要对XY取双对数，判断能否用一个直线很好拟合就行。常见的直线拟合效果评估标准有拟合误差平方和、R平方。

3、代码实现

```
#!/usr/bin/env python
# -*-coding:utf-8 -*-

import matplotlib.pyplot as plt
import numpy as np
from sklearn import linear_model
from scipy.stats import norm

def DataGenerate():
    X = np.arange(10, 1010, 10)  # 0-1，每隔着0.02一个数据  0处取对数,会时负无穷  生成100个数据点
    noise=norm.rvs(0, size=100, scale=0.2)  # 生成50个正态分布  scale=0.1控制噪声强度
    Y=[]
    for i in range(len(X)):
       Y.append(10.8*pow(X[i],-0.3)+noise[i])  # 得到Y=10.8*x^-0.3+noise

    # plot raw data
    Y=np.array(Y)
    plt.title("Raw data")
    plt.scatter(X, Y,  color='black')
    plt.show()

    X=np.log10(X)  # 对X，Y取双对数
    Y=np.log10(Y)
    return X,Y

def DataFitAndVisualization(X,Y):
    # 模型数据准备
    X_parameter=[]
    Y_parameter=[]
    for single_square_feet ,single_price_value in zip(X,Y):
       X_parameter.append([float(single_square_feet)])
       Y_parameter.append(float(single_price_value))

    # 模型拟合
    regr = linear_model.LinearRegression()
    regr.fit(X_parameter, Y_parameter)
    # 模型结果与得分
    print('Coefficients: \n', regr.coef_,)
    print("Intercept:\n",regr.intercept_)
    # The mean square error
    print("Residual sum of squares: %.8f"
      % np.mean((regr.predict(X_parameter) - Y_parameter) ** 2))  # 残差平方和

    # 可视化
    plt.title("Log Data")
    plt.scatter(X_parameter, Y_parameter,  color='black')
    plt.plot(X_parameter, regr.predict(X_parameter), color='blue',linewidth=3)

    # plt.xticks(())
    # plt.yticks(())
    plt.show()

if __name__=="__main__":
    X,Y=DataGenerate()
    DataFitAndVisualization(X,Y)
```
![这里写图片描述](http://img.blog.csdn.net/20160927232749405)

![这里写图片描述](http://img.blog.csdn.net/20160927232757719)