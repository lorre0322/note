---
title: 学习Typescript-13 (symbol类型)
date: 2020-01-01 10:33
category: study
tag: 
	- Typescript
---
### 自ECMAScript 2015起，`symbol`成为了一种新的原生类型，就像`number`和`string`一样。

`symbol`类型的值是通过`Symbol`构造函数创建的。
可以传递参做为唯一标识 只支持 string 和 number类型的参数
```ts
let sym1 = Symbol();
let sym2 = Symbol("key"); // 可选的字符串key
```

## Symbol的值是唯一的
```ts
const s1 = Symbol()const s2 = Symbol()// s1 === s2 =>false
```

## 用作对象属性的键
```ts
let sym = Symbol(); let obj = {    [sym]: "value"}; console.log(obj[sym]); // "value"
```

## 使用symbol定义的属性，是不能通过如下方式遍历拿到的
```ts
const symbol1 = Symbol('666')
const symbol2 = Symbol('777')
const obj1= {
   [symbol1]: '小明',
   [symbol2]: '二蛋',
   age: 18,
   sex: '男'
}
// 1 for in 遍历
for (const key in obj1) {
   // 注意在console看key,是不是没有遍历到symbol1
   console.log(key)
}
// 2 Object.keys 遍历
Object.keys(obj1)
console.log(Object.keys(obj1))
// 3 getOwnPropertyNames
console.log(Object.getOwnPropertyNames(obj1))
// 4 JSON.stringfy
console.log(JSON.stringify(obj1))
```

*如何拿到*
```ts
// 1 拿到具体的symbol 属性,对象中有几个就会拿到几个
Object.getOwnPropertySymbols(obj1)
console.log(Object.getOwnPropertySymbols(obj1))
// 2 es6 的 Reflect 拿到对象的所有属性
Reflect.ownKeys(obj1)
console.log(Reflect.ownKeys(obj1))
```

## Symbol.iterator 迭代器 和 生成器 for of
支持遍历大部分类型迭代器 arr nodeList argumetns set map 等
```ts
var arr = [1,2,3,4];
let iterator = arr[Symbol.iterator]();

console.log(iterator.next());  //{ value: 1, done: false }
console.log(iterator.next());  //{ value: 2, done: false }
console.log(iterator.next());  //{ value: 3, done: false }
console.log(iterator.next());  //{ value: 4, done: false }
console.log(iterator.next());  //{ value: undefined, done: true }
```

*测试用例*
```ts
interface Item {
    age: number,
    name: string
}
 
const array: Array<Item> = [{ age: 123, name: "1" }, { age: 123, name: "2" }, { age: 123, name: "3" }]
 
type mapTypes = string | number
const map:Map<mapTypes,mapTypes> = new Map()
 
map.set('1','王爷')
map.set('2','陆北')
 
const obj = {
    aaa:123,
    bbb:456
}
 
let set:Set<number> = new Set([1,2,3,4,5,6])
// let it:Iterator<Item> = array[Symbol.iterator]()
const gen = (erg:any): void => {
    let it: Iterator<any> = erg[Symbol.iterator]()
    let next:any= { done: false }
    while (!next.done) {
        next =  it.next()
        if (!next.done) {
            console.log(next.value)
        }
    }
}
gen(array)
```

以下为这些symbols的列表：

***Symbol.hasInstance***
方法，会被instanceof运算符调用。构造器对象用来识别一个对象是否是其实例。

***Symbol.isConcatSpreadable***
布尔值，表示当在一个对象上调用Array.prototype.concat时，这个对象的数组元素是否可展开。

***Symbol.iterator***
方法，被for-of语句调用。返回对象的默认迭代器。

***Symbol.match***
方法，被String.prototype.match调用。正则表达式用来匹配字符串。

***Symbol.replace***
方法，被String.prototype.replace调用。正则表达式用来替换字符串中匹配的子串。

***Symbol.search***
方法，被String.prototype.search调用。正则表达式返回被匹配部分在字符串中的索引。

***Symbol.species***
函数值，为一个构造函数。用来创建派生对象。

***Symbol.split***
方法，被String.prototype.split调用。正则表达式来用分割字符串。

***Symbol.toPrimitive***
方法，被ToPrimitive抽象操作调用。把对象转换为相应的原始值。

***Symbol.toStringTag***
方法，被内置方法Object.prototype.toString调用。返回创建对象时默认的字符串描述。

***Symbol.unscopables***
对象，它自己拥有的属性会被with作用域排除在外。