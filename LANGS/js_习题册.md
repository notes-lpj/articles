## js_习题册

```js
undefined > 0		// false
undefined < 0		// false
undefined == 0	// false

null > 0	// false
null < 0	// false
null == 0	// false

undefined == null // true

NAN == NAN // false
```

```js
// ~~value 的使用
// 对于浮点数，~~value 可以代替 parseInt(value)，而且前者效率更高

parseInt(-2.99);	//-2
~~(-2.99)				//-2
```

```js
// 异步
const one = () => {
    return new Promise((resolve, reject) => {
        setTimeout(() => {
            resolve(1)
        }, 1000);
    })
}

async function myFunc() {
    console.log('In function!');	// 2
    const res = await one();
    console.log(res);							// 4
}

console.log('before function'); 	// 1
myFunc();
console.log('after function');  	// 3
```

```js
/**
 * 构造一棵二叉树，计算其高度
 * 		深度是相对于树上的节点来说的，而高度是相对于树本身来说的；树上所有节点的深度的最大值就是树的高度
 *		空树高度为 0，只有y根节点的树高度为 1
 */

function Node(value) {
    this.value = value;
    this.left = null;
    this.right = null;
}

var a = new Node(1);
var b = new Node(2);
var c = new Node(3);
var d = new Node(4);
var e = new Node(5);
var f = new Node(6);

a.left = b;
b.left = c;
c.right = d;
d.left = e;
d.right = f;

function heightOfTree(node) {
    if (!node) {
        return 0;
    }

    var leftDepth = 0, rightDepth = 0, leftSon = node.left, rightSon = node.right;

    if (leftSon) {
        // 计算左子树的深度
        leftDepth = heightOfTree(leftSon);
    }
    if (rightSon) {
        // 计算右子树的深度
        rightDepth = heightOfTree(rightSon);
    }

    return leftDepth > rightDepth ? leftDepth + 1 : rightDepth + 1;

}

console.log(heightOfTree(a));
```

```js
// for...of 常用于异步的遍历（for，forEach，for...in 是常规的同步遍历）

function muti(num) {
  return new Promise((resolve, reject) => {
    setTimeout(() => {
      resolve(num * num)
    }, 1000)
  })
}

let arr = [1, 2, 3];

arr.forEach(async (i) => {
  const res = await muti(i)
  console.log(res)
})

(async function (){
  for (let i of arr) {
    console.log(await muti(i));
  } 
}())
```

```js
// 手写 instanceof

function myInstanceof(target, origin) {
  if (typeof(target) !== 'object' || target == null) return false 

  // init
  let proto = target.__proto__

  while(true) {
    // 如果已经是原型链的顶端，直接reture false
    if (proto === null) return false
    // 核心代码
    if (proto === origin.prototype) return true 
    // 往上找
    proto = proto.__proto__
  }
}

console.log(myInstanceof([], Array))
```

```js
// for...in

Array.prototype.foo1 = function () { console.log(123) }
Array.prototype.asd = 'qwe';
let arr = [1, 2, 3];

for (let key in arr) {
  console.log(key, arr[key]);
}

// 它竟然把原型链上的K-V也给遍历出来了
```

```js
// 手写字符串 trim 方法

String.prototype.myTrim = function () {
  return this.replace(/^\s+/, '').replace(/\s+$/, '')
}
```

```js
// 一道题

function foo(x) {
  this.x = x; // 1. window.x = 5; 3. window.x = 6;
  return this;
}

var x = foo(5); // 2. window.x = window
var y = foo(6); // 4. window.y = window

console.log(x.x); // window.x.x --> 6.x --> undefined
console.log(y.x); // window.y.x --> window.x --> 6
```

```js
// 数组去重

// 法一：
function unique(arr) {
  let res = []
  arr.forEach(item => {
    // 注意 indexOf 也是一种遍历
    if (res.indexOf(item) < 0) {
      res.push(item)
    }
  })
  return res
}

// 法二：set 的方式更高效
function unique(arr) {
  let set = new Set(arr)
  return [...set]
}
```

```js
/**
 * 数组拍平
 * concat.apply([], arr)只能一次拍平arr最深像[1, [2, 3]]，想想apply传参方式？ 所以得递归！
 */
function flat(arr) {
  // 验证传入的数组是否已经被拍平
  const isDeep = arr.some(item => item instanceof Array)
  // 如果已经被拍平，直接返回
  if (!isDeep) {
    return arr
  }
  // 还没有被拍平，则拍平一层，然后递归
  const res = Array.prototype.concat.apply([], arr)
  return flat(res)
}
```

```js
// 将 URL 查询参数转化为 js 对象

// 法一
function parseURLToObj() {
  let resObj = {}
  strParam = location.search.substr(1)

  strParam.split('&').forEach(param => {
    let arr = param.split('=')
    key = arr[0]
    val = arr[1]
    resObj[key] = val
  })

  return resObj
}

// 法二
function parseURLToObj() {
  let resObj = {}
  const pList = new URLSearchParams(location.search)
  pList.forEach((val, key) => {
    resObj[key] = val
  })
  return resObj
}
```

```js
// 用 promise 的方式手写加载图片

const url1 = 'http://p8.qhimg.com/bdr/__85/t01fdcd6377a309b28b.jpg'
const url2 = 'http://p1.qhimg.com/bdm/1600_900_85/t0134dbb70e2ab3ec6b.jpg'

function getPic(src) {
  return new Promise((resolve, reject) => {
    var oImg = document.createElement('img')
    oImg.onload = function () {
      resolve(img)
    }
    oImg.onerror = function () {
      const err = new Error(`图片加载失败 ${src}`)
      reject(err)
    }
    oImg.src = src					// 触发图片加载
  })
}

getPic(url1)
  .then((data) => {
    console.log(data);
    return data;						// 普通对象
  })
  .then((data) => {
    console.log(data);
  })
  .catch((err) => {
    console.error(err);
  })

getPic(url1)
  .then((data) => {
    console.log(data);
    return getPic(url2);		// Promise 实例
  })
  .then((data) => {
    console.log(data);
  })
  .catch((err) => {
    console.error(err);
  })
```

```js
// callback hell && promise

const url1 = '/data1.json'
const url2 = '/data2.json'
const url3 = '/data3.json'

// callbackHell
$.get(url1, () => {
  // ...
  $.get(url2, () => {
    // ...
    $.get(url3, () => {
      // ...
    })
  })
})

// Promise
function getData(url) {
  return new Promise((resolve, reject) => {
    $.ajax({
      url,
      success(data) {
        resolve(data)
      },
      error(err) {
        reject(err)
      }
    })
  })
}

// 将callbackHell扁平化
getData(url1)
  .then((data1) => {
    // ...
    return getData(url2)
  })
  .then((data2) => {
    // ...
    return getData(url3)
  })
  .then((data3) => {
    // ...
  })
  .catch((err) => {
    // ...
  })
```

```js
// jQuery的插件机制 & 扩展性
	// 插件机制: 在原型上添加属性 & 方法
	// 扩展性: ( 体现了 extends & super() 的价值 )

// 新轮子
class myjQuery extends jQuery {
  constructor(selector) {
    super(selector)
  }
  // 扩展自己的方法...
}
```

```js
// falsely & truly 变量

// 以下是 falsely 变量，除此以外都是 truly 变量
!!false === false
!!undefined === false
!!null === false
!!0 === false
!!'' === false
!!NaN === false
```

```js
// 何时使用===，何时使用==? （考点：强制类型转换）

除了 == null 之外，其他一律用 ===

	obj.a == null 相当于 obj.a === null || obj.a === undefined

考点：强制类型转换

	字符串拼接

  if 语句 和 逻辑运算

  ==：比如 100 == '100'、0 == ''、0 == false、'' == false、null == undefined 都是 true
```

```js
// map 方法

const res = [1, 2, 3].map(parseInt)

// 执行结果竟然有NaN ? 看下面就明白了

[1, 2, 3].map((item, index) => {
	parseInt(item, index)
})
```

```js
// push & pop & unshift & shift 这几个API注意返回值，且都改变原数组

// push
let arr = [1, 2, 3]
let res = arr.push(4)
console.log(res, arr)

// pop
let arr = [1, 2, 3]
let res = arr.pop()
console.log(res, arr)

// unshift
let arr = [1, 2, 3]
let res = arr.unshift(4)
console.log(res, arr)

// shift
let arr = [1, 2, 3]
let res = arr.shift()
console.log(res, arr)
```

```js
// 判断空对象

// 法一：JSON.stringify(data) == "{}"
var data = {};
var b = (JSON.stringify(data) == "{}");
alert(b);

// 法二：for in 循环

// 法三：使用 ES6 的 Object.keys() 方法
var data = {};
var arr = Object.keys(data);
alert(arr.length == 0);
```
