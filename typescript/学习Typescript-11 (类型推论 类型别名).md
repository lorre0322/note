---
title: 学习Typescript-11 (类型推论 类型别名)
date: 2020-12-31 11:15
category: study
tag: 
	- Typescript
---
## 什么是类型推论
1. 我声明了一个变量但是没有定义类型
TypeScript会在没有明确的指定类型的时候推测出一个类型，这就是类型推论
```ts
let str = "小明"
//ts会帮我推断出来这是一个string类型
//不能够在赋值给别的类型
//str=123456
```
2. 如果你声明变量没有定义类型也没有赋值这时候TS会推断成any类型可以进行任何操作
```ts
let xiaoming
xiaoming = 123
xiaoming = "小明"
xiaoming = true
```

##  类型别名
type 关键字（可以给一个类型定义一个名字）多用于符合类型

*定义类型别名*
```ts
type str = string
let s:str = "我是小明"
console.log(s);
```

*定义函数别名*
```ts
type str = () => string
let s: str = () => "我是小明"
console.log(s);
```

*定义联合类型别名*
```ts
type str = string | number
let s: str = 123
let s2: str = '123'
console.log(s,s2);
```

*定义值的别名*
```ts
type value = boolean | 0 | '213'
let s:value = true
//变量s的值  只能是上面value定义的值
```