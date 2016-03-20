#可用的算法和思路  

##floyd-warshall较简单，可作为初步模型。dijkstra是单源最短路

##suitable case: Kruskal算法适用于边稀疏的情形
-  kruskal算法的思想是找最小边，且每次找到的边不会和以找出来的边形成环路，利用一个一维数组group存放当前顶点所在连通图标示（每条最小边，属于一个连通图），直到顶点都找完  

##suitable case: Prim算法适用于边稠密的情形，形成树结构
-  任何时候都只有两个集合，一个是已处理顶点集合，一个是未处理  
-  [example](http://www.cnblogs.com/Veegin/archive/2011/04/29/2032388.html)

##bellman-ford队列优化，可与dijkstra比较选择其一

##KSP算法，遗传算法，动态规划等模型可作优化

##A * 算法是DFS的父集[教程](http://blog.csdn.net/feixiaoxing/article/details/6982932/)

###[计网相关](http://www.mat.uc.pt/~eqvm/links/cursos.html)

##suitable case: dijkstra可找到原点到其他所有点的最小值（同时为最小）不会形成树结构  
-  可用邻接表替代邻接矩阵优化时间复杂度

'''
Dijkstra算法、A*算法、SPFA算法、Bellman-Ford算法和Floyd-Warshall算法，本文主要介绍其中的三种。
最短路径问题是图论研究中的一个经典算法问题，旨在寻找图（由结点和路径组成的）中两结点之间的最短路
径。

算法具体的形式包括：
确定起点的最短路径问题：即已知起始结点，求最短路径的问题。
确定终点的最短路径问题：与确定起点的问题相反，该问题是已知终结结点，求最短路径的问题。在无向图中
该问题与确定起点的问题完全等同，在有向图中该问题等同于把所有路径方向反转的确定起点的问题。
确定起点终点的最短路径问题：即已知起点和终点，求两结点之间的最短路径。
全局最短路径问题：求图中所有的最短路径。

Floyd
求多源、无负权边的最短路。用矩阵记录图。时效性较差，时间复杂度O(V^3)。
Floyd-Warshall算法（Floyd-Warshall algorithm）是解决任意两点间的最短路径的一种算法，可以正确处理
有向图或负权的最短路径问题。
Floyd-Warshall算法的时间复杂度为O(N^3)，空间复杂度为O(N^2)。
Floyd-Warshall的原理是动态规划：
设Di,j,k为从i到j的只以(1..k)集合中的节点为中间节点的最短路径的长度。
若最短路径经过点k，则Di,j,k = Di,k,k-1 + Dk,j,k-1；
若最短路径不经过点k，则Di,j,k = Di,j,k-1。
因此，Di,j,k = min(Di,k,k-1 + Dk,j,k-1 , Di,j,k-1)。
在实际算法中，为了节约空间，可以直接在原来空间上进行迭代，这样空间可降至二维。

Floyd-Warshall算法的描述如下：
for k ← 1 to n do 
for i ← 1 to n do 
for j ← 1 to n do 
if (Di,k + Dk,j < Di,j) then  
Di,j ← Di,k + Dk,j; 

其中Di,j表示由点i到点j的代价，当Di,j为 ∞ 表示两点之间没有任何连接。


Dijkstra
求单源、无负权的最短路。时效性较好，时间复杂度为O（V*V+E）,可以用优先队列进行优化，优化后时间复杂
度变为0（v*lgn）。
源点可达的话，O（V*lgV+E*lgV）=>O（E*lgV）。
当是稀疏图的情况时，此时E=V*V/lgV，所以算法的时间复杂度可为O（V^2） 。可以用优先队列进行优化，优
化后时间复杂度变为0（v*lgn）。
Bellman-Ford
求单源最短路，可以判断有无负权回路（若有，则不存在最短路），时效性较好，时间复杂度O（VE）。
Bellman-Ford算法是求解单源最短路径问题的一种算法。
单源点的最短路径问题是指：给定一个加权有向图G和源点s，对于图G中的任意一点v，求从s到v的最短路径。
与Dijkstra算法不同的是，在Bellman-Ford算法中，边的权值可以为负数。设想从我们可以从图中找到一个环
路（即从v出发，经过若干个点之后又回到v）且这个环路中所有边的权值之和为负。那么通过这个环路，环路
中任意两点的最短路径就可以无穷小下去。如果不处理这个负环路，程序就会永远运行下去。 而Bellman-Ford
算法具有分辨这种负环路的能力。

SPFA
是Bellman-Ford的队列优化，时效性相对好，时间复杂度O（kE）。（k< 与Bellman-ford算法类似，SPFA算法采用一系列的松弛操作以得到从某一个节点出发到达图中其它所有节点的
最短路径。所不同的是，SPFA算法通过维护一个队列，使得一个节点的当前最短路径被更新之后没有必要立刻
去更新其他的节点，从而大大减少了重复的操作次数。
SPFA算法可以用于存在负数边权的图，这与dijkstra算法是不同的。
与Dijkstra算法与Bellman-ford算法都不同，SPFA的算法时间效率是不稳定的，即它对于不同的图所需要的时
间有很大的差别。
在最好情形下，每一个节点都只入队一次，则算法实际上变为广度优先遍历，其时间复杂度仅为O(E)。另一方
面，存在这样的例子，使得每一个节点都被入队(V-1)次，此时算法退化为Bellman-ford算法，其时间复杂度为
O(VE)。
SPFA算法在负边权图上可以完全取代Bellman-ford算法，另外在稀疏图中也表现良好。但是在非负边权图中，


为了避免最坏情况的出现，通常使用效率更加稳定的Dijkstra算法，以及它的使用堆优化的版本。通常的SPFA
'''
