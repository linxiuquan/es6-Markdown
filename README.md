
# 目录
- [解构赋值](#解构赋值)
- [Set](#set)
- [WeakSet](#weakset)
- [Map](#map)
- [WeakMap](#weakmap)

## 解构赋值
*	[a,b]=[1,2];数组解析赋值
*	{a,b}={a:1,b:2};对象解析赋值
*	[a,b,c=3]=[1,2];默认值解析

## New Set()

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

## WeakSet()
>**只能存储对象，弱类型引用，不能遍历**
*	没有clear和size
*	其他与 New Set() 相同


## New Map()
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
*   其他与 New Set 相同

## New WeakMap()
>**key只能是对象，弱类型引用，不能遍历**
*	没有clear和size
*   其他与 New Map() 相同
	
	
	