---
title: 【typescript】01常见类型
date: 2023-03-28 16:19:30
tags: typescript
---

> typescript 中“类型”指的是在声明变量和函数的时候 对变量指定 ts 类型，对函数的入参和返回值指定 ts 类型。<br>
> 在 ts 中指定变量，函数的类型，后续的赋值或者函数的返回值，都需要是符合指定类型的值才可以通过 ts 的校验。<br>
> 这一次主要是学习最基本和常见的类型，这些是构建更复杂类型的基础

### 原始类型

`string`,`number`,`boolean`
js 中最常用到的三种原始数据类型，在 ts 中都有对应的类型。用法如下：

```javascript
let str: string = "";
let strNum: number = 0;
let strBol: boolean = false;
```

### 数组类型

```javascript
let arr: number[] = [1, 2]; // 表示指定一个number类型的数组
let arrNew: Array<number> = [1, 2, 3]; // 第二种写法 同样指定一个number类型的数组
```

### any

any 是 ts 中一个特殊的类型，当你不希望一个值导致类型检查错误的时候，就可以设置为 any。

### noImplicitAny

如果你没有指定一个类型，TypeScript 也不能从上下文推断出它的类型，编译器就会默认设置为 any 类型。

如果你总是想避免这种情况，毕竟 TypeScript 对 any 不做类型检查，你可以开启编译项 noImplicitAny，当被隐式推断为 any 时，TypeScript 就会报错。

### 变量上的类型注解

上面针对 ts 类型的使用示例中，在变量后面加上例`:number`，叫做类型注解。也是在进行显式指定变量类型。

> 不过大部分时候，使用类型注解显式指定变量类型不是必须的。因为 ts 会自动推断类型。举个例子，变量的类型可以基于初始值进行推断
