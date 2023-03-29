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

### 函数

在使用 ts 声明一个函数的时候，可以对函数的入参参数类型 和函数的返回值类型 进行类型注解的添加。

#### 参数类型注解

当你声明一个函数的时候，你可以在每个参数后面添加一个类型注解，声明函数可以接受什么类型的参数。参数类型注解跟在参数名字后面：

```javascript
function func1(name: string) {}
```

#### 返回值类型注解

```javascript
function getFavoriteNumber(): number {
  return 26;
}
```

### 匿名函数

匿名函数往往针对参数不需要添加类型注解，因为 ts 会根据上下文推断出参数的类型。

### 对象类型

定义一个对象类型，需要列出他的属性和属性对应的类型即可

```javascript
function printCoord(pt: { x: number, y: number }) {
  console.log("The coordinate's x value is " + pt.x);
  console.log("The coordinate's y value is " + pt.y);
}
printCoord({ x: 3, y: 7 });

// 上方函数 针对参数pt添加一个ts对象类型，类型有两个属性，分别指定了number类型，属性之前可以使用`,`或者`;`分割。最后一个属性可加可不加。
// 每个属性对应的类型是可选的，如果你不指定，默认使用 any 类型。
```

可选属性：在对象类型中，可以指定属性是可选的，需要在属性名后面加一个`?`

```javascript
function printName(obj: { first: string, last?: string }) {
  // ...
}
```

### 联合类型

一个联合类型是由两个或者更多类型组成的类型，表示值可能是这些类型中的任意一个。这其中每个类型都是联合类型的成员（members）。
如下：

```typescript
function printName(name: number | string) {}
```

上方`number | string`这种写法就是定义了一个联合类型，表明这个函数入参类型可以是`number`或者`string`

> 但是在使用联合类型的时候，不能使用一种类型独有的方法。
> 想要使用一种类型独有的方法时：可以采用类型判断的写法进行使用。例如：

```typescript
function printName(name: string[] | string) {
  if (Array.isArray(name)) {
    // 可以使用数组特有的方法
  } else {
    // 可以使用 string类型特有的方法
  }
}
```

> 当联合类型成员 都有的一个共同方法在被调用的时候，则不需要做上述操作

### 类型别名

使用 type 关键字创建类型别名。更多的是用来代替重复使用的对象类型和联合类型。语法使用如下：

```typescript
type Point = {
  x: number;
  y: number;
};

function printCrof(pt: Point) {}

type Id = number | string;
```

> 注意别名是唯一的别名，你不能使用类型别名创建同一个类型的不同版本。当你使用类型别名的时候，它就跟你编写的类型是一样的

### 接口

使用 interface 命名对象类型

```typescript
interface Point {
  x: number;
  y?: number;
}

function printCrof(pt: Point) {}
```

### 类型断言

类型断言 常常用在你明确知道一个值的类型的时候，但是 ts 不知道的时候，使用 as 关键字为该值指定类型，也可以使用尖括号`<T>`(在.tsx 中不能使用)的形式

```typescript
const myCanvas = document.getElementById("main_canvas") as HTMLCanvasElement;
// 或者
const myCanvas = <HTMLCanvasElement>document.getElementById("main_canvas");
```
