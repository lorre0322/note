---
title: 学习Typescript-16 (namespace命名空间)
date: 2020-01-01 11:05
category: study
tag: 
	- Typescript
---
我们在工作中无法避免全局变量造成的污染，TypeScript提供了namespace 避免这个问题出现
-   内部模块，主要用于组织代码，避免命名冲突。
-   命名空间内的类默认私有
-   通过 `export` 暴露
-   通过 `namespace` 关键字定义

##### TypeScript与ECMAScript 2015一样，任何包含顶级`import`或者`export`的文件都被当成一个模块。相反地，如果一个文件不带有顶级的`import`或者`export`声明，那么它的内容被视为全局可见的（因此对模块也是可见的）

命名空间中通过`export`将想要暴露的部分导出
如果不用export 导出是无法读取其值的
```ts
namespace a {
    export const Time: number = 1000
    export const fn = <T>(arg: T): T => {
        return arg
    }
    fn(Time)
}
namespace b {
     export const Time: number = 1000
     export const fn = <T>(arg: T): T => {
        return arg
    }
    fn(Time)
}
a.Time
b.Time
```

*嵌套命名空间*
```ts
namespace a {
    export namespace b {
        export class Vue {
            parameters: string
            constructor(parameters: string) {
                this.parameters = parameters
            }
        }
    }
}
let v = a.b.Vue
new v('1')
```

##### 抽离命名空间
```ts
//a.ts
export namespace V {
    export const a = 1
}

//b.ts
import {V} from '../observer/index'
console.log(V);

//{a:1}
```

合并命名空间
重名的命名空间会合并
![](https://img-blog.csdnimg.cn/bf816965597949c69329ad5f17e0efd5.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBA5bCP5ruhenM=,size_20,color_FFFFFF,t_70,g_se,x_16)
