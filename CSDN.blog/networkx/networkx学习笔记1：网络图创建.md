创建一个无标度网络G，随机生成节点：
```
# -*-coding:utf-8-*-

import networkx as nx
import matplotlib.pyplot as plt

G = nx.random_graphs.barabasi_albert_graph(100, 1)  # 生成一个BA无标度网络G
nx.draw(G)  # 绘制网络G
plt.savefig("ba.png")  # 输出方式1: 将图像存为一个png格式的图片文件
plt.show()

G = nx.Graph()
G.add_node(1)  # 添加节点
G.add_edge(2, 3)  # 添加边
G.add_edge(3, 2)
print G.nodes()  # 输出所有的节点
print G.edges()  # 输出所有的边
print G.number_of_edges()  # 边的条数，只有一条边，就是（2，3）

G.add_weighted_edges_from([(0, 1, 3.0), (1, 2, 7.5)])  # 增加边的权重
print G.get_edge_data(1, 2)

path = nx.all_pairs_shortest_path(G)
print path[0][2]  # 计算最短路径
print '---------------------------------------------------------'

G = nx.random_graphs.barabasi_albert_graph(1000, 3)
print G.degree(0)
print G.degree()  # 返回节点的度
print nx.degree_histogram(G)  # 返回所有节点的分布序列

degree = nx.degree_histogram(G)
x = range(len(degree))
y = [z/float(sum(degree)) for z in degree]
plt.loglog(x, y, color='blue', linewidth=2)
plt.show()

print 'average clustering coefficient is', nx.average_clustering(G)
print "every node's clustering coefficient is ", nx.clustering(G)

print 'Diameter of G is ', nx.diameter(G)
print "all nodes' average shortest path length is", nx.average_shortest_path_length(G)
```