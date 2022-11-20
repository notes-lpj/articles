## 平衡的二叉排序树（AVL树）

#### 为啥要让二叉排序树 「平衡」 ？

> 尽可能地让二叉排序树保持平衡，就能获得更高效的二叉排序树~

#### 啥叫 「平衡」 ？

> 任意结点的左右子树深度之差都不超过 1 => 就叫做 「平衡」
>
> 如下图两棵树都是二叉排序树，但只有左边这棵树是平衡的

<img src='https://gitee.com/pj-l/imgs-1/raw/master/screenShot/image-20211105172817700.png' style='float: left;'></img>

#### 啥叫 「结点的平衡因子」 ？

> 结点的`平衡因子` = 该结点的左子树高 - 该结点的右子树高

<img src='https://gitee.com/pj-l/imgs-1/raw/master/screenShot/image-20211114094537851.png' style='float: left; height: 300px;'></img>

#### AVL树

> 平衡的二叉排序树 => AVL树（`A`delson-`V`elsky and `L`andis Tree）

<img src='https://gitee.com/pj-l/imgs-1/raw/master/screenShot/image-20211114092013219.png' style='float: left; height: 200px;'></img>

```c
/*-- 定义 AVL 树 --*/
struct Node {
  char data;
  struct Node * lChild;
  struct Node * rChild;
  int balance; // 结点的平衡因子
};

typedef struct Node AVL_Node;
typedef struct Node * AVL_Tree;
/*-- 定义 AVL 树 --*/
```

#### AVL树插入新结点，如何保持平衡 ？

> 给出结论：
>
> ​	由于`插入操作会导致 「最小不平衡子树」 高度+1`，所以`只需将最小不平衡子树调成平衡`，就能让其他祖先结点都恢复平衡，也就让整棵树恢复了平衡

<img src='https://gitee.com/pj-l/imgs-1/raw/master/screenShot/image-20211115083504231.png' style='float: left;'></img>

> 调整结果如下

<img src='https://gitee.com/pj-l/imgs-1/raw/master/screenShot/image-20211114095849335.png' style='float: left;'></img>

#### 「如何调整」 最小不平衡子树 ？

##### 调整目标

1. 恢复平衡
2. 保持二叉排序树的特性：左子树结点的值 < 根结点的值 < 右子树结点的值

##### 大致思路

1. `插入`新结点
2. `从下往上看`新结点到根结点的`路径上的`结点的`平衡因子`，`找最小不平衡子树`（< -1 或 > 1 就不平衡啦~）
3. `看插入方式`是（LL、RR、LR、RL）中的哪一种，进而`选择合适的策略调整`最小不平衡子树
4. `检查`调整完毕的整棵树是否恢复成了一棵平衡二叉排序树（`AVL`树）

##### LL（右旋）

> 在子树的 「左孩子」 的 「左子树」 中插入导致子树不平衡

<img src='https://gitee.com/pj-l/imgs-1/raw/master/screenShot/image-20211114101932530.png' style='float: left; height: 260px;'></img>

> 处理方式：
>
> ​	`将最小不平衡子树 => 右旋（右单旋转）`（最小不平衡子树顺时针旋转一下）

<img src='https://gitee.com/pj-l/imgs-1/raw/master/screenShot/image-20211114103524241.png' style='float: left;'></img>

> 验证：
>
> 1. 恢复平衡 ？=> yes
> 2. 保持二叉排序树的特性 ? => yes
> 
> 代码思路如下：

<img src='https://gitee.com/pj-l/imgs-1/raw/master/screenShot/image-20211115091315402.png' style='float: left;'></img>

##### RR（左旋，与 LL 同理）

> 在子树的 「右孩子」 的 「右子树」 中插入导致子树不平衡

<img src='https://gitee.com/pj-l/imgs-1/raw/master/screenShot/image-20211114104609950.png' style='float: left;'></img>

> 验证：
>
> 1. 恢复平衡 ？=> yes
> 2. 保持二叉排序树的特性 ? => yes
>
> 代码思路如下：

<img src='https://gitee.com/pj-l/imgs-1/raw/master/screenShot/image-20211115091625722.png' style='float: left;'></img>

##### LR

> 在子树的 「左孩子」 的 「右子树」 中插入导致子树不平衡

先左旋，再右旋

##### RL

> 在子树的 「右孩子」 的 「左子树」 中插入导致子树不平衡

先右旋，再左旋

#### 练习题

1. `插入`新结点 ====>`（57）`
2. `从下往上看`新结点到根结点的`路径上的`结点的`平衡因子`，`找最小不平衡子树`（< -1 或 > 1 就不平衡啦~）====>`（整棵树）`
3. `看插入方式`是（LL、RR、LR、RL）中的哪一种，进而`选择合适的策略调整`最小不平衡子树 ====>`（LR => 先左旋，再右旋）`
4. `检查`调整完毕的整棵树是否恢复成了一棵平衡二叉排序树（`AVL`树）====>`（yes）`

<img src='https://gitee.com/pj-l/imgs-1/raw/master/screenShot/image-20211115101321294.png' style='float: left;'></img>

#### 不忘初心：分析 AVL 树的查找效率

> 我们构建 AVL 树（让二叉排序树变平衡）就是为了让二叉排序树尽可能高效啊
>
> 平衡之后有多高效呢 ？那就来分析下 AVL 树的查找效率吧~



- 对于高度为 h 的二叉排序树来说，查找一个关键字 「最多」 需要对比 h 次 => 即查找操作的时间复杂度不可能超过 O(h)

  ​													     => 或者说平均查找长度 ASL 不会超过 O(h) 这个量级

- `所以我们只需要分析平衡二叉树的树高`



- 设高度为 h 的平衡二叉树含有的最少结点数为 n_h
  - n_0 = 0;
  - n_1 = 1;
  - n_2 = 2;
  - n_3 = 4;
  - ...

<img src='https://gitee.com/pj-l/imgs-1/raw/master/screenShot/image-20211115110202721.png' style='float: left;'></img>

- 所以
  - n_4 = 7;
  - n_5 = 12;
  - ...
- 举个例子，当给出 9 个结点，因为 7 < `9` < 12
- 所以这 9 个结点能形成高度为 4 的平衡二叉树，平均查找长度 ASL 不会超过 4

<img src='https://gitee.com/pj-l/imgs-1/raw/master/screenShot/image-20211115110850140.png' style='float: left;'></img>

- 所以

<img src='https://gitee.com/pj-l/imgs-1/raw/master/screenShot/image-20211115111003431.png' style='float: left;'></img>

- 证明过程使用了有一定复杂性的数学知识，对于考研不重要，故略，感兴趣则自行查看 1962 年 AVL 树的作者发表的论文

<img src='https://gitee.com/pj-l/imgs-1/raw/master/screenShot/image-20211115111401219.png' style='float: left;'></img>
