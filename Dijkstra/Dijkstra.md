

#These code are some algorithms for route planning wrote in scala with spark framework.

But now it still in testing.

---

##图形学类(graphic)：

##传统类(traditional)：

##智能仿生学类(intelligent bionic)：





##其他(others)：

### 1、Dijkstra算法

路径： /src/test/scala/algorithm/others/Dijkstra

步骤：

1. 初始化：初始化路径距离![](http://latex.codecogs.com/gif.latex?\\vec{D}=\\{x_1,x_2,...,x_n\\})，其中n为节点个数，![](http://latex.codecogs.com/gif.latex?x_i)为源点(start)到第![](http://latex.codecogs.com/gif.latex?i)点的距离，初始时![](http://latex.codecogs.com/gif.latex?\\vec{D}=\\vec{infinity}), 同时![](http://latex.codecogs.com/gif.latex?\\vec{D}\\_{start}=0)； 进一步， 初始化节点标记状态![](http://latex.codecogs.com/gif.latex?\\vec{C}=\\{c_1,c_2,···,c_n\\}), 如果一个节点已经找到最终路径, 则标记为true， 否则为false， 初始时![](http://latex.codecogs.com/gif.latex?\vec{C}=\\vec{false})， 最后初始化源点到其他节点最优路径![](http://latex.codecogs.com/gif.latex?\\vec{P}=\\{p_1,p_2,···,p_n\\})， 其中![](http://latex.codecogs.com/gif.latex?p\_i)为源点到第![](http://latex.codecogs.com/gif.latex?i)个节点的路径，初始时pi=[start -> i]。
2. 更新路径距离![](http://latex.codecogs.com/gif.latex?\\vec{D})， 标记状态![](http://latex.codecogs.com/gif.latex?\\vec{C})，最优路径![](http://latex.codecogs.com/gif.latex?\\vec{P})：在![](http://latex.codecogs.com/gif.latex?\\vec{D})中找到数值最小对应的节点，且该节点需满足在![](http://latex.codecogs.com/gif.latex?\\vec{D})中状态为false的，举例，初始化1个6节点的图，且第1个为源点，则有：

|   0.0    |   7.0    |   9.0    | Infinity | Infinity |   14.0   |
| :------: | :------: | :------: | :------: | :------: | :------: |
|   7.0    |   0.0    |   10.0   |   15.0   | Infinity | Infinity |
|   9.0    |   10.0   |   0.0    |   11.0   | Infinity |   2.0    |
| Infinity |   15.0   |   11.0   |   0.0    |   6.0    | Infinity |
| Infinity | Infinity | Infinity |   6.0    |   0.0    |   9.0    |
|   14.0   | Infinity |   2.0    | Infinity |   9.0    |   0.0    |

初始D={0.0, Infinity, Infinity, Infinity,Infinity,Infinity}，且C={false, false, false, false,false,fasle}。

如下图：

![dijkstra](http://i.imgur.com/tCp3Rvx.gif)

第一次迭代找到![](http://latex.codecogs.com/gif.latex?\\vec{D})中数值最小(0.0)对应的节点为1，且该点满足在此时状态为false(该步为初始化步，具体实现时可以预先处理)。

第二次迭代时，找与节点1链接最小值为7，其节点为2，且此时节点2的状态标记为true，则将2加入![](http://latex.codecogs.com/gif.latex?\\vec{P})，P2=[0 -> 2]。

第三次迭代时，以节点2为起点，更新![](http://latex.codecogs.com/gif.latex?\\vec{D})，具体为：![](http://latex.codecogs.com/gif.latex?\\vec{d_i} = min(d\_i, d\_{2}+l\_{2i})), 其中![](http://latex.codecogs.com/gif.latex?l_{2i})为节点2到节点$i$的直接链接距离，如此更新完![](http://latex.codecogs.com/gif.latex?\vec{D})后，重复第二次迭代的步骤，直到所有节点的状态标记为true。

详细迭代过程如下表：

|                    步骤                    |                    P                     | D(2) | D(3) |   D(4)   |   D(5)   | D(6) |
| :--------------------------------------: | :--------------------------------------: | :--: | :--: | :------: | :------: | :--: |
|                   初始化                    |                   {1}                    | 7.0  | 9.0  | Infinity | Infinity | 14.0 |
| 1：第2个点加入P，                     以2为中心更新D  |                 [1 -> 2]                 | 7.0  | 9.0  |   22.0   | Infinity | 14.0 |
| 2：第3个点加入P，                    以3为中心更新D，由于1->2->3比1->3距离远，所以1->3为最短 | [1 -> 2,                                            1 ->3 ] | 7.0  | 9.0  |   20.0   | Infinity | 11.0 |
| 3：第6个点加入P，                     以6为中心更新D  | [1 -> 2,                                             1 ->3,                                               1 ->3 -> 6 ] | 7.0  | 9.0  |   20.0   |   20.0   | 11.0 |
| 4：第5个点加入P，                以5为中心更新D，此处5和4都是20，先选谁无所谓 | [1 -> 2,                                                1 ->3,                                               1 ->3 -> 6,                                                     1 ->3 -> 6 ->5 ] | 7.0  | 9.0  |   20.0   |   20.0   | 11.0 |
|            5：第4个点加入P，全部点遍历完成             | [1 -> 2,                                             1 ->3,                                                 1 ->3 -> 6,                                           1 ->3 -> 6 ->5,                                    1 ->3 ->4 ] | 7.0  | 9.0  |   20.0   |    20    | 11.0 |