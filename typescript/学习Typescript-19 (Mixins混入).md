---
title: 学习Typescript-19 (Mixins混入)
date: 2020-01-01 11:32
category: study
tag: 
	- Typescript
---
Typescript混入 Mixins 其实vue也有mixins这个东西 你可以把他看作为合并

## 1.对象混入
可以使用es6的Object.assign合并多个对象
此时people会被推断成一个交叉类型Name & Age & sex；
```ts
interface Name {
    name: string
}
interface Age {
    age: number
}
interface Sex {
    sex: number
}
 
let people1: Name = { name: "小明" }
let people2: Age = { age: 18 }
let people3: Sex = { sex: 1 }
 
const people = Object.assign(people1,people2,people3)
```

### 类的混入
首先声明两个mixins类（严格模式要关闭不然编译不过）
```ts
class A {
    type: boolean = false;
    changeType() {
        this.type = !this.type
    }
}
class B {
    name: string = '张三';
    getName(): string {
        return this.name;
    }
}
```

下面创建一个类，结合了这两个mixins
首先应该注意到的是，没使用extends而是使用implements。 把类当成了接口

我们可以这么做来达到目的，为将要mixin进来的属性方法创建出占位属性。 这告诉编译器这些成员在运行时是可用的。 这样就能使用mixin带来的便利，虽说需要提前定义一些占位属性
```ts
class C implements A,B{
    type:boolean
    changeType:()=>void;
    name: string;
    getName:()=> string
}
```

最后，创建这个帮助函数，帮我们做混入操作。 它会遍历mixins上的所有属性，并复制到目标上去，把之前的占位属性替换成真正的实现代码

Object.getOwnPropertyNames()可以获取对象自身的属性，除去他继承来的属性，
对它所有的属性遍历，它是一个数组，遍历一下它所有的属性名
```ts
Mixins(C, [A, B])
function Mixins(curCls: any, itemCls: any[]) {
    itemCls.forEach(item => {
        Object.getOwnPropertyNames(item.prototype).forEach(name => {
            curCls.prototype[name] = item.prototype[name]
        })
    })
}
```
