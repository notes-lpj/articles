## 十字链表法（only for 有向图）

#### 为什么

> 有向图：
>
> ​	邻接矩阵法：空间复杂度高：O(|V|^2)
>
> ​	邻接表法：求入度麻烦（找顶点的入边麻烦），需遍历整个邻接表，时间复杂度高
>
> 寻找更合适的 「有向图存储方案」：
>
> ​	希望保持较低的空间复杂度
>
> ​	希望求顶点的入度和出度都方便

#### 是什么 & 怎么做

<img src='https://gitee.com/pj-l/imgs-1/raw/master/screenShot/image-20211123220118723.png' style='float: left;'></img>

<img src='https://gitee.com/pj-l/imgs-1/raw/master/screenShot/image-20211123220217565.png' style='float: left;'></img>

<img src='https://gitee.com/pj-l/imgs-1/raw/master/screenShot/image-20211123220316615.png' style='float: left;'></img>

<img src='https://gitee.com/pj-l/imgs-1/raw/master/screenShot/image-20211123220347905.png' style='float: left;'></img>

#### 性能分析

<img src='https://gitee.com/pj-l/imgs-1/raw/master/screenShot/image-20211123220825049.png' style='float: left;'></img>

#### 回顾与总结

> 其实邻接矩阵法删除顶点，不一定需要移动大量数据元素，更好的做法是将被删除的顶点做个标记，然后清空邻接矩阵中该顶点所在的行和列即可

<img src='https://gitee.com/pj-l/imgs-1/raw/master/screenShot/image-20211124104929051.png' style='float: left;'></img>
