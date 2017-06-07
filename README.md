
# 目录
- [解构赋值](#解构赋值)
- [字符串的扩展](#字符串的扩展)
- [Set](#set)
- [WeakSet](#weakset)
- [Map](#map)
- [WeakMap](#weakmap)

# 解构赋值
 >如果已经声明的变量用于解构赋值 必须不将大括号写在行首，避免JavaScript将其解释为代码块({x} = {x: 1});
##  用途
**1. 交换变量的值**

```
let x = 1;
let y = 2;

[x, y] = [y, x];
```

**2. 从函数返回多个值**

```
// 返回一个数组

function example() {
  return [1, 2, 3];
}
let [a, b, c] = example();

// 返回一个对象

function example() {
  return {
    foo: 1,
    bar: 2
  };
}
let { foo, bar } = example();
```

**3. 函数参数的定义**

```
// 参数是一组有次序的值
function f([x, y, z]) { ... }
f([1, 2, 3]);

// 参数是一组无次序的值
function f({x, y, z}) { ... }
f({z: 3, y: 2, x: 1});
```

**4. 提取JSON数据**

**5. 函数参数的默认值**

**6. 遍历Map结构**

```
var map = new Map();
map.set('first', 'hello');
map.set('second', 'world');

for (let [key, value] of map) {
  console.log(key + " is " + value);
}
// first is hello
// second is world
```

**7. 输入模块的指定方法**

```
const { SourceMapConsumer, SourceNode } = require("source-map");
```


##  数组解析
 >只要某种数据结构具有 Iterator 接口，都可以采用数组形式的解构赋值。

```
let [foo, [[bar], baz]] = [1, [[2], 3]];

let [ , , third] = ["foo", "bar", "baz"];

let [x, , y] = [1, 2, 3];

let [head, ...tail] = [1, 2, 3, 4];

let [x, y, ...z] = ['a'];
x // "a"
y // undefined
z // []

let [foo] = [];
foo // undefined
let [bar, foo] = [1];
foo // undefined
```
## 默认值
> 注意，ES6 内部使用严格相等运算符（===），判断一个位置是否有值。所以，如果一个数组成员不严格等于undefined，默认值是不会生效的。

```
let [foo = true] = [];
foo // true

let [x, y = 'b'] = ['a']; // x='a', y='b'
let [x, y = 'b'] = ['a', undefined]; // x='a', y='b'

```
## 对象解构赋值

```
let { foo: baz } = { foo: "aaa", bar: "bbb" };
baz // "aaa"
foo // error: foo is not defined
```
上面代码中，foo是匹配的模式，baz才是变量。真正被赋值的是变量baz，而不是模式foo。

## 字符串的解构解析

```
const [a, b, c, d, e] = 'hello';
a // "h"
b // "e"
c // "l"
d // "l"
e // "o"
//类似数组的对象都有一个length属性，因此还可以对这个属性解构赋值。
let {length : len} = 'hello';
```
## 数值和布尔值的解构赋值
>解构赋值的规则是，只要等号右边的值不是对象或数组，就先将其转为对象。由于undefined和null无法转为对象，所以对它们进行解构赋值，都会报错。
```
let {toString: s} = 123;
s === Number.prototype.toString // true

let {toString: s} = true;
s === Boolean.prototype.toString // true

let { prop: x } = undefined; // TypeError
let { prop: y } = null; // TypeError
```
## 函数参数的解构赋值

```
[[1, 2], [3, 4]].map(([a, b]) => a + b);
// [ 3, 7 ]

function move({x = 0, y = 0} = {}) {
  return [x, y];
}

move({x: 3, y: 8}); // [3, 8]
move({x: 3}); // [3, 0]
move({}); // [0, 0]
move(); // [0, 0]

[1, undefined, ].map((x = 'yes') => x);
// [ 1, 'yes', 'yes' ]
```
## 圆括号
>可以使用圆括号的情况只有一种：赋值语句的非模式部分，可以使用圆括号。

```
[(b)] = [3]; // 正确
({ p: (d) } = {}); // 正确
[(parseInt.prop)] = [3]; // 正确


```
* 变量声明语句中，不能带有圆括号。
* 函数参数中，模式不能带有圆括号。
* 赋值语句中，不能将整个模式，或嵌套模式中的一层，放在圆括号之中。


# 字符串的扩展

* [字符的 Unicode 表示法](http://es6.ruanyifeng.com/#docs/string)

### 查找字符串
* includes(string,startIndex)：返回布尔值，表示是否找到了参数字符串。
* startsWith(string,startIndex)：返回布尔值，表示参数字符串是否在源字符串的头部。
* endsWith(string,startToIndex)：返回布尔值，表示参数字符串是否在源字符串的尾部。

### “字符串翻倍”
* repeat(number)返回一个新字符串，表示将原字符串重复n次。

### 补全长度(ES2017)
#### 用途
1. 为数值补全指定位数。下面代码生成10位的数值字符串。

```
'1'.padStart(10, '0') // "0000000001"
'12'.padStart(10, '0') // "0000000012"
'123456'.padStart(10, '0') // "0000123456"
```

2. 提示字符串格式。

```
'12'.padStart(10, 'YYYY-MM-DD') // "YYYY-MM-12"
'09-12'.padStart(10, 'YYYY-MM-DD') // "YYYY-09-12"
```

#### 语法
* .padStart(length,string)用于头部补全
* .padEnd(length,string)用于尾部补全。

### 模板字符串
>大括号内部可以放入任意的JavaScript表达式，可以进行运算，以及引用对象属性。

模板字符串后面可以调用trim()消除反引号到第一个字符的换行(目前暂不知道这个用处是什么)


```
const tmpl = addrs => `
  <table>
  ${addrs.map(addr => `
    <tr><td>${addr.first}</td></tr>
    <tr><td>${addr.last}</td></tr>
  `).join('')}
  </table>
`;
const data = [
    { first: '<Jane>', last: 'Bond' },
    { first: 'Lars', last: '<Croft>' },
];

console.log(tmpl(data));
// <table>
//
//   <tr><td><Jane></td></tr>
//   <tr><td>Bond</td></tr>
//
//   <tr><td>Lars</td></tr>
//   <tr><td><Croft></td></tr>
//
// </table>
```
**如果需要引用模板字符串本身，在需要时执行，可以像下面这样写**

```
// 写法一
let str = 'return ' + '`Hello ${name}!`';
let func = new Function('name', str);
func('Jack') // "Hello Jack!"

// 写法二
let str = '(name) => `Hello ${name}!`';
let func = eval.call(null, str);
func('Jack') // "Hello Jack!"
```





# Set

>**去重的集合，只能遍历出value值**
* 	.size
* 	.add(value)
* 	.delete(value) 删除成功 ? return ture : return false
* 	.clear()
* 	.has(value)
* 	.values()
*	.keys()
*	.entries()
*	.forEach()

# WeakSet
>**只能存储对象，弱类型引用，不能遍历**
*	没有clear和size
*	其他与 Set 相同


# Map
>键值对的集合，key可以是任何类型


```
const map = new Map([
  ['name', '张三'],
  ['title', 'Author']
]);
```

*	.set(key,value) 返回当前的Map对象
*	.get(key)
*	.has(key)
*   其他与 Set 相同

# WeakMap
>**key只能是对象，弱类型引用，不能遍历**
*	没有clear和size
*   其他与 Map 相同
	
	
	