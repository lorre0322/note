---
title: 学习Typescript-18 (声明文件d.ts)
date: 2020-01-01 11:28
category: study
tag: 
	- Typescript
---
#### 声明文件declare
当使用第三方库时，我们需要引用它的声明文件，才能获得对应的代码补全，接口提示等功能。

```ts
declare var 声明全局变量
declare function 声明全局方法
declare class 声明全局类
declare enum 声明全局枚举类型
declare namespace 声明（含有子属性的）全局对象
interface 和 type 声明全局类型
/// <reference /> 三斜线指令
```

例如我们有一个express 和 axios
![](https://img-blog.csdnimg.cn/4846847abe1f4359b777584e7a237c72.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBA5bCP5ruhenM=,size_20,color_FFFFFF,t_70,g_se,x_16)

 发现express 报错了
让我们去下载他的声明文件
`npm install @types/node -D`
那为什么axios 没有报错
我们可以去node_modules 下面去找axios 的package json
![](https://img-blog.csdnimg.cn/56e5d930f9144c3aaf50faf638906976.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBA5bCP5ruhenM=,size_20,color_FFFFFF,t_70,g_se,x_16)

发现axios已经指定了声明文件 所以没有报错可以直接用
通过语法declare 暴露我们声明的axios 对象
`declare  const axios: AxiosStatic;`

如果有一些第三方包确实没有声明文件我们可以自己去定义
名称.d.ts 创建一个文件去声明

例如express.d.ts
declare  const express: ()=> any;
关于这些第三发的声明文件包都收录到了 npm
