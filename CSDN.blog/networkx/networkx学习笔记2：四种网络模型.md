
    四种网络模型：规则图，ER随机图，WS小世界网络，BA无标度网络

```
"""
    规则图：
    random_graphs.random_regular_graph(d, n)方法可以生成一个含有n个节点，每个节点有d个邻居节点的规则图
"""
RG = nx.random_graphs.random_regular_graph(3, 20)  # 随机生成20个节点，每个节点的度都是3，构成一个网络图
pos = nx.spectral_layout(RG)  # 图形样式，这里是根据图的拉普拉斯特征向量排列节点的
nx.draw(RG, pos, with_labels=False, node_size=30)  # 绘制图形
plt.show()

"""
    ER随机图：以概率p连接N个节点中的每一对节点。
    用random_graphs.erdos_renyi_graph(n,p)方法生成一个含有n个节点、以概率p连接的ER随机图
"""
ER = nx.random_graphs.erdos_renyi_graph(20, 0.2)  # 随机生成20个节点，节点间的连接概率都是0.2
pos = nx.shell_layout(ER)  # 图形样式，这里是节点在同心圆上分布
nx.draw(ER, pos, with_labels=False, node_size=30)
plt.show()

"""
    WS小世界网络：
    用random_graphs.watts_strogatz_graph(n, k, p)方法生成一个含有n个节点、每个节点有k个邻居、以概率p随机化重连边的WS小世界网络。
"""
WS = nx.random_graphs.watts_strogatz_graph(20, 4, 0.3)
pos = nx.circular_layout(WS)  # 图形样式，这里是节点在一个圆环上均匀分布
nx.draw(WS, pos, with_labels=False, node_size=30)
plt.show()

"""
    BA无标度网络
    用random_graphs.barabasi_albert_graph(n, m)方法生成一个含有n个节点、每次加入m条边的BA无标度网络
"""
BA = nx.random_graphs.barabasi_albert_graph(20, 1)
pos = nx.spring_layout(BA)  # 图形的布局样式，这里是中心放射状
nx.draw(BA, pos, with_labels=False, node_size=30, node_color='black')
plt.show()
```


    nx.draw()方法，至少接受一个参数：待绘制的网络G

    参数：

    运行样式：
      - `node_size`:  指定节点的尺寸大小(默认是300)
      - `node_color`:  指定节点的颜色 (默认是红色，可以用字符串简单标识颜色，例如'r'为红色，'b'为绿色等)
      - `node_shape`:  节点的形状（默认是圆形，用字符串'o'标识）
      - `alpha`: 透明度 (默认是1.0，不透明，0为完全透明)
      - `width`: 边的宽度 (默认为1.0)
      - `edge_color`: 边的颜色(默认为黑色)
      - `style`: 边的样式(默认为实现，可选： solid|dashed|dotted,dashdot)
      - `with_labels`: 节点是否带标签（默认为True）
      - `font_size`: 节点标签字体大小 (默认为12)
      - `font_color`: 节点标签字体颜色（默认为黑色）

    运用布局：
     circular_layout：节点在一个圆环上均匀分布
     random_layout：节点随机分布
     shell_layout：节点在同心圆上分布
     spring_layout： 用Fruchterman-Reingold算法排列节点（样子类似多中心放射状）
     spectral_layout：根据图的拉普拉斯特征向量排列节点

    添加文本：
    用plt.title()方法可以为图形添加一个标题，该方法接受一个字符串作为参数。
    fontsize参数用来指定标题的大小。例如：plt.title("BA Networks", fontsize = 20)。
    如果要在任意位置添加文本，则可以采用plt.text()方法。

"""

规则图：
![这里写图片描述](http://img.blog.csdn.net/20170227142127715?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQva2V2aW5lbHN0cmk=/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/SouthEast)

ER随机图：
![这里写图片描述](http://img.blog.csdn.net/20170227142145403?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQva2V2aW5lbHN0cmk=/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/SouthEast)
WS小世界网络：
![这里写图片描述](http://img.blog.csdn.net/20170227142157872?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQva2V2aW5lbHN0cmk=/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/SouthEast)
BA无标度网络：
![这里写图片描述](http://img.blog.csdn.net/20170227142230467?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQva2V2aW5lbHN0cmk=/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/SouthEast)