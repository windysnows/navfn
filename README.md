# navfn
navigation路径规划器navfn原理详解  
navfn算法首先根据代价地图生成一个加权无向图，代价地图中的每个栅格代表加权无向图的每个节点，每个栅格的代价值构成加权无向图边的权重．然后根据加权无向图，利用dijkstra算法从起点开始传播到目标点，获取传播过程中到各个节点的最优行走代价值．最后从目标点开始，沿着最优行走代价值梯度下降的方向寻找到起点的最优轨迹．其主要过程如下：  
　　（１）NavFn::setCostmap(const COSTTYPE *cmap, bool isROS, bool allow_unknown)  
　　　　（设置代价地图：将代价地图转换成加权无向图）  
　　（２）NavFn::setupNavFn(bool keepit)  
　　　　（设置potential数组：对于每个新的规划，需要重新设置potential数组为默认值）  
　　　　注：potential数组的值即为起点到各个节点的最优行走代价值  
　　（３）NavFn::propNavFnDijkstra(int cycles, bool atStart)  
　　　　（dijkstra传播函数：通过dijkstra算法以广度优先的方式更新potential数组）  
　　（４）NavFn::calcPath(int n, int *st)  
　　　　（计算轨迹：从目标点开始沿着最优行走代价值梯度下降的方向寻找到起点的最优轨迹）  
