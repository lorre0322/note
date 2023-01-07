---
title: 学习Typescript-1（基础类型） 
date: 2020-12-24 10:56
category: 
tag: 
	- 
---

**基础类型：Boolean、Number、String、null、undefined 以及 ES6 的  Symbol 和 ES10 的 BigInt。**

## 1.字符串类型
字符串是使用string定义的。
```ts
//普通声明
let a: string = '123'
//也可以使用es6的字符串模板
let str: string = `dddd${a}`
```

## 2.数字类型
支持十六进制、十进制、八进制和二进制。
```ts
let notANumber: number = NaN;//Nan
let num: number = 123;//普通数字
let infinityNumber: number = Infinity;//无穷大
let decimal: number = 6;//十进制
let hex: number = 0xf00d;//十六进制
let binary: number = 0b1010;//二进制
let octal: number = 0o744;//八进制s
```

## 3.布尔类型
注意，使用构造函数 Boolean 创造的对象不是布尔值
```ts
let createdBoolean: boolean = new Boolean(1)
//这样会报错 应为事实上 new Boolean() 返回的是一个 Boolean 对象 
```
事实上 new Boolean() 返回的是一个 Boolean 对象 需要改成
```ts
let createdBoolean: Boolean = new Boolean(1)

let booleand: boolean = true //可以直接使用布尔值
let booleand2: boolean = Boolean(1) //也可以通过函数返回布尔值
```

## 4.空值类型
JavaScript 没有空值（Void）的概念，在 TypeScript 中，可以用 void 表示没有任何返回值的函数
```ts
function voidFn(): void {
    console.log('test void')
}
```
void 类型的用法，主要是用在我们不希望调用者关心函数返回值的情况下，比如通常的异步回调函数。
void也可以定义undefined 和 null类型。
```ts
let u: void = undefined
let n: void = null;
```

## 5.Null和undefined类型
```ts
let u: undefined = undefined;//定义undefined
let n: null = null;//定义null
```
**void 和 undefined 和 null 最大的区别**

与 void 的区别是，undefined 和 null 是所有类型的子类型。也就是说 undefined 类型的变量，可以赋值给 string 类型的变量：
```ts
//这样写会报错 void类型不可以分给其他类型
let test: void = undefined
let num2: string = "1"
num2 = test

//这样是没问题的
let test: null = null
let num2: string = "1"
num2 = test
 
//或者这样的
let test: undefined = undefined
let num2: string = "1"
num2 = test
```
### ⭐Tips
如果你配置了tsconfig.json 开启了严格模式,null 不能 赋予 void 类型
```js
//tsconfig.json
{
  "compilerOptions":{
    "strict": true
  }
}
//app.ts 报错
let n:void = null
```