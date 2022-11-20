## 邻接多重表法（only for 无向图）

#### 为什么

> 无向图：
>
> ​	邻接矩阵法：空间复杂度高：O(|V|^2)
>
> ​	邻接表法：边结点有一倍冗余，对于（删除边、删除顶点）的操作，时间复杂度高（就像下图）
>
> 寻找更合适的 「无向图存储方案」：
>
> ​	希望保持较低的空间复杂度
>
> ​	希望避免数据冗余，让删除操作更方便

<img src='https://gitee.com/pj-l/imgs-1/raw/master/screenShot/image-20211124101742992.png' style='float: left; height: 350px'></img>

#### 是什么 & 怎么做

<img src='https://gitee.com/pj-l/imgs-1/raw/master/screenShot/image-20211124101947566.png' style='float: left;'></img>

<img src='https://gitee.com/pj-l/imgs-1/raw/master/screenShot/image-20211124102058491.png' style='float: left;'></img>

<img src='https://gitee.com/pj-l/imgs-1/raw/master/screenShot/image-20211124102234656.png' style='float: left;'></img>

<img src='https://gitee.com/pj-l/imgs-1/raw/master/screenShot/image-20211124102303590.png' style='float: left;'></img>

#### 删除操作

- 删除边结点贼拉方便，就跟单链表删结点一模一样

<img src='https://gitee.com/pj-l/imgs-1/raw/master/screenShot/image-20211124103108974.png' style='float: left;'></img>

<img src='https://gitee.com/pj-l/imgs-1/raw/master/screenShot/image-20211124103156078.png' style='float: left;'></img>

- 删除一个顶点也方便，比如删除 E 顶点

<img src='https://gitee.com/pj-l/imgs-1/raw/master/screenShot/image-20211124103325866.png' style='float: left;'></img>

<img src='https://gitee.com/pj-l/imgs-1/raw/master/screenShot/image-20211124103539700.png' style='float: left;'></img>

<img src='https://gitee.com/pj-l/imgs-1/raw/master/screenShot/image-20211124103857133.png' style='float: left;'></img>

#### 小结

> 邻接多重表法（only for 无向图）：
>
> ​	保持了较低的空间复杂度
>
> ​	无数据冗余，删除操作方便

<img src='https://gitee.com/pj-l/imgs-1/raw/master/screenShot/image-20211124104113654.png' style='float: left;'></img>
