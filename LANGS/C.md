## C 语言

> 有的编译器会给 int 型变量设置初始值 0，有的编译器则不会

#### 格式化输入的字符串，类似于 es6 的解构赋值

![image-20211123085117936](https://aliyun-oss-lpj.oss-cn-qingdao.aliyuncs.com/images/by-picgo/image-20211123085117936.png)

#### 如何将被调函数中的局部变量返回给主调函数 ？

- 法一：return

- 法二：

  - 指针型 * 参数 for C

  - 引用型 & 参数 for C++

#### 枚举类型

> 相比于只使用数字，合理地使用枚举类型可使代码的可读性变好～

```c
typedef enum { red = 1, green, blue } COLOR;
COLOR color;

printf("请挑选一个数字输入，你会得到一个好看的颜色: (1，2，3)：");
scanf("%u", &color);

switch (color) {
  case red:
    printf("你选中的颜色是红色!\n"); break;
  case green:
    printf("你选中的颜色是绿色!\n"); break;
  case blue:
    printf("你选中的颜色是蓝色!\n"); break;
  default:
    printf("你没选任何颜色\n"); break;
}
```

#### 获取二维数组的 row、col

```c
int arr[4][5] = {
  { 2, -1, 7, -4, 8 },
  { 0, -6, -2, 8, 0 },
  { -7, -1, 9, 4, -1 },
  { 2, 2, -9, -9, 7 },
};

printf("row = %d\n", sizeof(arr) / sizeof(arr[0]));
printf("col = %d\n", sizeof(arr[0]) / sizeof(arr[0][0]));
printf("total = %d\n", sizeof(arr) / sizeof(arr[0][0])); // 另：total == row * col
```

#### 表示形如 10^5 这样的指数

```c
// 法一
1e+5

// 法二
#include <math.h>
pow(10, 5);
```

#### ! 和 ～

![image-20211124092501360](https://aliyun-oss-lpj.oss-cn-qingdao.aliyuncs.com/images/by-picgo/image-20211124092501360.png)

#### 关于 double 的输入/输出格式

![image-20211124092352380](https://aliyun-oss-lpj.oss-cn-qingdao.aliyuncs.com/images/by-picgo/image-20211124092352380.png)

#### 任何变量在 「赋值」 的时候，最好考虑下 「变量类型的取值范围，是否会“溢出”」

- 比如 「判断回文数」 时，由于 int 的取值范围是 [ -2^31, 2^31 - 1 ]
- 而 2^31 - 1 == 2147483647 <--反转--> 7463847412
- 这就“溢出”了整数的取值范围
- 所以对于判断回文数是采用了 「反转后一半」，然后与得到的前一半进行对比

#### C 语言无布尔类型

> C++ 有布尔类型，但布尔类型确实能让代码可读性更高，所以在 C 中模拟布尔类型

```c
// 方法一
typedef enum { false = 0, true } bool;

// 方法二
typedef int bool;
#define true 1
#define false 0
```

#### 结构体的定义中不允许赋初始值

因为一个结构体的定义就相当于是在定义一种新的数据类型

#### 无论如何看见野指针赶紧置 NULL

避免野指针

#### free 掉某个结点可能会造成野指针，需特别注意！

```c
free(*list);
(*list) = NULL; // 一定得加这一行，否则出现野指针
```

#### 无论如何看见新开辟的内存空间（比如用 malloc 申请的，或是刚定义的一个数组），都应合理擦洗内存（处理内存脏数据的问题）

- 最简单可靠的方式就是遍历赋初值，当然也可用库函数 [fill](https://zh.cppreference.com/w/cpp/algorithm/fill)

- 注意：[memset](https://zh.cppreference.com/w/cpp/string/byte/memset) 不能用于擦洗内存

```c
for (int i = 0; i < maxSize; i ++) {
  list.data[i] = 0;
}
```

#### 结构体中静态数组的长度必须用 「常量」，而不能用 「只读变量」

- 「只读变量」 是在内存中开辟一个地方来存放它的值，只不过这个值由编译器限定不允许被修改，关键字 const 就是用来限定一个变量不允许被改变的修饰符（Qualifier）

- ANSI-C 规定：数组定义时长度必须是 「常量」

```c
// 定义顺序表（静态分配方式）
#define maxSize 10 // 不能用 const int maxSize = 10;
typedef struct {
  int data[maxSize];
  int length;
} SqList;
```

#### 封装函数应认真思考返回值的类型，应尽量避免避免不加思考直接写 void

- 确保代码的健壮性

#### 以线性表为例，如果不涉及结点的增删，只是单纯的 「读」 性质的操作，比如打印操作，参数的传递传 「镜像」 即可

- 避免误操作致使原对象结构被破坏

- 「镜像」 可理解为 「克隆」 「拷贝」，与 C 的传指针或 C++ 的传引用相异

#### 内存回收相关

- 变量声明申请的内存，内存回收工作由系统负责

- malloc 申请的内存属于堆内存，需开发者手动调用 free 函数进行内存释放回收

即，malloc 和 free 必成对使用！

#### 区分`*a++`和`*++a`

```cpp
#include <iostream>
using namespace std;

int main() {

  int arr[4] = { 100, 200, 300, 400 };
  int* p = arr;

  cout << *p++ << endl; // 100
  cout << *p << endl;   // 200
  cout << *++p << endl; // 300
  cout << *p << endl;   // 300

  return 0;
}
```
```cpp
#include <iostream>
using namespace std;

void test(int* a, int* b);

int main() {
  int c = 2, d = 3;                // 这里声明并初始化的两个变量在内存中是连续存放的（1 int == 4 byte）
  cout << &c << " " << &d << endl; // 0x7ffd030354b8 0x7ffd030354bc

  int* p = &c;
  test(p, &d);

  cout << c << " " << d << endl; // 2 2
  return 0;
}

void test(int* a, int* b) {
  cout << *a << " " << *b << endl; // 2 3

  *a++;        // 这里只是取到值之后又挪了一下指针，然后俩指针重合了，这俩指针又都是局部变量
  *b = *b - 1; // 这里就改变了变量 d 所指向的内存区域

  cout << *a << " " << *b << endl; // 2 2
}
```

#### 输入二维数组

https://www.zhihu.com/question/493924763/answer/2185167589/

#### 顺序栈 vs 链栈

- 顺序栈应注意考虑「栈溢出」的问题，即栈的容量是否够用
- 实际开发多使用链栈，因为扩容方便

#### 取模运算（%）可以将无限的整数域，映射到有限的整数集合上

- 比如自然数 0 1 2 3... 都对 5 取模
  - 结果为：{ 0, 1, 2, 3, 4 }

- 比如 3 4 5 6... 都对 8 取模
  - 结果为：{ 3, 4, 5, 6, 7, 1, 2, 0 }

- 无限的整数对 N 取模
  - 结果为：{ 0, 1, 2, 3, ..., N-1 }

#### 判断变量是字符还是数字

> https://zh.wikipedia.org/wiki/ASCII

![image-20211029164632667](https://aliyun-oss-lpj.oss-cn-qingdao.aliyuncs.com/images/by-picgo/image-20211029164632667.png)

![image-20211029164948797](https://aliyun-oss-lpj.oss-cn-qingdao.aliyuncs.com/images/by-picgo/image-20211029164948797.png)

- itoa => integer to ascii
- atoi => ascii to integer

> The [isdigit()](https://www.programiz.com/c-programming/library-function/ctype.h/isdigit) function checks whether a character is numeric character (0-9) or not.

![image-20211029165144995](https://aliyun-oss-lpj.oss-cn-qingdao.aliyuncs.com/images/by-picgo/image-20211029165144995.png)
