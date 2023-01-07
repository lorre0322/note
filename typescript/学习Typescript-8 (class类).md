---
title: 学习Typescript-8 (class类)
date: 2020-12-26 21:45
category: study
tag: 
	- Typescript
---
ES6提供了更接近传统语言的写法，引入了Class（类）这个概念，作为对象的模板。通过class关键字，可以定义类。基本上，ES6的class可以看作只是一个语法糖，它的绝大部分功能，ES5都可以做到，新的class写法只是让对象原型的写法更加清晰、更像面向对象编程的语法而已。上面的代码用ES6的“类”改写，就是下面这样。
```ts
//定义类
class Person {
    constructor () {
    
    }
    run () {
        
    }
}
```

## 1.我们在TS是这样定义类的
```ts
//在TypeScript是不允许直接在constructor 定义变量的 需要在constructor上面先声明
class Person{
//	error
//	constructor(name,age){
//		this.name = name
//	}

//这样引发了第二个问题你如果了定义了变量不用 也会报错 通常是给个默认值 或者 进行赋值
//	age:number = 18
	name:string
	age:number
	constructor(name,age){
		this.name = name
		this.age = age
	}
	run(){
		
	}
}
```

## 2.类的修饰符
### 总共有三个 **public private protected**
![](https://img-blog.csdnimg.cn/2eaca794296640b183cdcdddb221ee68.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBAcXExMTk1NTY2MzEz,size_20,color_FFFFFF,t_70,g_se,x_16)
1. 使用public 修饰符 可以让你定义的变量 内部访问 也可以外部访问 如果不写默认就是public
![](https://img-blog.csdnimg.cn/a4a2499d7600474dac78dc9a3af3afa2.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBAcXExMTk1NTY2MzEz,size_20,color_FFFFFF,t_70,g_se,x_16)
2. 使用  private 修饰符 代表定义的变量私有的只能在内部访问 不能在外部访问
![](https://img-blog.csdnimg.cn/d64333f651ec4a799ca665cae11d0d72.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBAcXExMTk1NTY2MzEz,size_20,color_FFFFFF,t_70,g_se,x_16)
3. 使用  protected 修饰符 代表定义的变量私有的只能在内部和继承的子类中访问 不能在外部访问
![](https://img-blog.csdnimg.cn/5ac43616ad77488284bae4205db3f6c8.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBAcXExMTk1NTY2MzEz,size_20,color_FFFFFF,t_70,g_se,x_16)

## 3. static 静态属性 和 静态方法
![](https://img-blog.csdnimg.cn/dd66b961270146ada29a9525d750feeb.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBAcXExMTk1NTY2MzEz,size_20,color_FFFFFF,t_70,g_se,x_16)
我们用static 定义的属性 不可以通过this 去访问 只能通过类名去调用
![](https://img-blog.csdnimg.cn/0e398a1e6ad7452a8d607821e3969bdf.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBAcXExMTk1NTY2MzEz,size_20,color_FFFFFF,t_70,g_se,x_16)
static 静态函数 同样也是不能通过this 去调用 也是通过类名去调用
![](https://img-blog.csdnimg.cn/77712c790646400ba121cb061994a762.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBAcXExMTk1NTY2MzEz,size_20,color_FFFFFF,t_70,g_se,x_16)

## 4.interface 定义 类
![](https://img-blog.csdnimg.cn/fe05924183054a489cf8613feb579be7.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBAcXExMTk1NTY2MzEz,size_20,color_FFFFFF,t_70,g_se,x_16)
ts interface 定义类使用关键字**implements**,后面跟interface的名字多个用逗号隔开,继承还是用extends。
```ts
 
interface PersonClass {
    get(type: boolean): boolean
}
 
interface PersonClass2{
    set():void,
    asd:string
}
 
class A {
    name: string
    constructor() {
        this.name = "123"
    }
}
 
class Person extends A implements PersonClass,PersonClass2 {
    asd: string
    constructor() {
        super()
        this.asd = '123'
    }
    get(type:boolean) {
        return type
    }
    set () {
 
    }
}
```

## 5.抽象类 
应用场景如果写的类实例化之后毫无用处此时我可以把他定义为抽象类
或者可以把他作为一个基类-> 通过继承一个派生类去实现基类的一些方法

下面这段代码会报错抽象类无法被实例化
```ts
abstract class A {
   public name:string  
}
new A()
```

*例子2*
我们在A类定义了 getName 抽象方法但为实现
我们B类实现了A定义的抽象方法 如不实现就不报错 **我们定义的抽象方法必须在派生类实现**
```ts
abstract class A {
   name: string
   constructor(name: string) {
      this.name = name;
   }
   print(): string {
      return this.name
   }
 
   abstract getName(): string
}
 
class B extends A {
   constructor() {
      super('小满')
   }
   getName(): string {
      return this.name
   }
}
 
let b = new B();
 
console.log(b.getName());
```