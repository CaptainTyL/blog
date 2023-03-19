---
title: Es6-Class
date: 2023-02-27 22:21:12
tags: Es6-Class
---
## class

#### 1.基本含义，以及使用注意

##### class声明类的简单示例

```javascript
class Point{
	constructor(x,y){
		this.x=x;
		this.y=y
	}
	toString(){
		return '('+ this.x +','+ this.y +')'
	}
}
const p = new Point(1,2)
```

##### class声明类的注意点

1.类中this关键字代表的是实例对象 即this===p

2.在class里面声明方法不需要在前面加上function，并且方法与方法之前不需要加逗号分隔，加了会报错

3.class声明的类 类型是function，并且类本身就是指向constructor

4.类本身是指向构造函数的，所以构造函数的prototype属性还是继续存在，并且实际上所有在类里面定义的方法都是定义在prototype上的，因此 在实例上调用方法，实际上是在调用原型上的方法

5.类中定义的所有方法都是不可枚举的

#### 2.constructor()方法

1.一个类一定会有一个constructor方法，如果没有的话，会自动默认添加一个空的constructor方法

2.constructor会默认返回实例对象 即this，也可以手动设置返回一个全新的对象

3.类必须使用new关键字来调用，因为类的实际类型也是Function，但与普通函数的区别就是 普通函数不需要new关键字来调用

#### 3.类的实例

```javascript
class Point	{
	//...
}
// 类的实例使用new关键字进行生成
const point=new Point()
// 直接调用 Point() 会报错
```

1.类的属性和方法 除非显式定义在其本身(即在this对象上，类的实例上)，否则都是定义在其原型上(即定义在class上)

```javascript
class Point {
	constructor(x,y){
		this.x=x //显式定义 
		this.y=y
	}
	// 下面方法为定义到原型上
	toString(){
		return '('+this.x+','+this.y+')'
	}
}

const p1=new Point(1,2)
const p2=new Point(3,4)
// 类的所有实例都是共享一个原型对象的
p1._proto_ === p2._proto_ //true
// 上述代码因为p1和p2都是类Point的实例 所以他们的原型都是Point.prototype 所以_proto_属性是相等的
```

2.实例属性的新写法

新写法就是可以将原本写在constructor()方法中this上面的属性，写到类的最顶层

```javascript
class Point	{
	_count=0; // 新写法，不需要加this，依然是定义到类的实例上
}
```

3.取值函数(getter)和存值函数(setter)

在类的内部 对某个属性使用get 和 set 关键字，可以对该属性进行取值和存值行为的拦截

```javascript
class Point	{
	constructor(){}
	get prop(){
    // 对prop属性进行 取值操作拦截
		return 'getter'
	}
	set prop(value){
    // 对prop属性进行 存值操作拦截
		return 'setter'+value
	}
}
const p1=new Point()
console.log((p1.prop='123')) // 'setter123'
console.log(p1.prop) // 'getter'
```

4.属性表达式

类中定义属性的，可以采用表达式的形式

#### 4.静态方法

