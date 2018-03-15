---
title: 构造函数
date: 2018-03-15 22:07:16
tags:
---

## 构造函数

> 惯例：
>
> 构造函数始终应该以一个大写字母开头（借鉴自其他OO语言，因为JavaScript不是一个面向对象（oo）的语言，它只是基于对象（bo）。


####  构造函数本身也是函数，只不过可以创建对象而已。
####  构造函数和普通函数没有什么区别，只不过是用new来调用；使用new操作符会经历一下4步：


> （1）创建一个新对象；
>
> （2）将构造函数作用域赋给新对象（所以this就指向了这个新对象）；
>
> （3）执行构造函数中的代码（为这个新对象添加属性）
>
> （4）返回新对象


```
function People() {
this.age = 12;
    this.sex = "男";
    this.name = "likai"
}

var people1 = new People()
var people2 = new People()

console.log(people1)      //{age: 12, sex: "男", name: "likai"}
 console.log(people1.age) //12
console.log(people2)      //{age: 12, sex: "男", name: "likai"}
console.log(people2.age)  //12
```
> JS中没有类的概念，我们这里只是和Java、C++、C#做一个类比，JS中只有构造函数而没有类！当一个函数被new操作符调用的时候，它总能返回一类的具有相同属性群的对象，感觉在“构造东西”，所以我们称为构造函数。这个函数很神奇，像一个模子，在制作类似的对象。

####  判断函数是否为构造函数

>   是否被new操作符调用

```
function Test(a,b){
    this.a = a;
    this.b = b
}
var test = Test(1,2);
var test1 = new Test(3,4)
console.log( test1.a )      //3
console.log( test.a )       //报错
```

####  如果构造函数里写了return情况

>  1. 如果return这个基本类型值，则无视这个return，该return什么还是return什么，但是return阻止了构造函数的执行；


```
function Test(a, b, c) {
    this.a = a;
    this.b = b;
    return
    this.c = c;
}

var test = new Test(1, 2, 3)
console.log(test)    //{a: 1, b: 2}
```

>  2. 如果return了引用类型值，则返回你return的这个，原有return被覆盖。(new四步走就失效了)

```
function Test(a, b, c) {
    this.a = a;
    this.b = b;
    return {"g":1, "h": 2}
    this.c = c;
}

var test = new Test(1, 2, 3)
console.log(test)    //{g: 1, h: 2}
```

## 原型链

#### 1. prototype

>  每一个函数天生都有prototype属性，指向一个空对象。也就是说，我们不需要定义这个prototype属性，任何一个函数只要写出来，它就拥有了prototype属性。
>
>  当这个构造函数被new的时候，它的每一个实例的__proto__属性，也指向这个对象

```
function Test(a,b,c) {
    this.a = a;
    this.b = b;
    this.c = c;
}
var test = new Test()
console.log(Test.prototype === test.__proto__) //true
```
> 我们称Test.prototype是Test构造函数的“原型”，Test.prototype是test的“原型对象”

#### 2. \_\_propto__

> 有原型链查找功能。当实例身上没有某个属性的时候，系统会沿着__proto__去寻找它的原型对象身上有没有这个属性。

```
function Test(a, b, c) {
    this.a = a;
    this.b = b;
    this.c = c;
}
Test.prototype.init = function () {
    console.log(this.a)
}

var test = new Test(1, 2, 3)
console.log(Test.prototype.init === test.__proto__.init)  //true
test.init()  //1
```

#### 3.方法的定义在原型上

> 我们刚才知道如果把函数写在构造函数里面，就相当于定义在了对象身上，此时函数会产生多个不同副本，影响程序效率。此时可以把函数定义在构造函数的原型上，这样所有new出的东西，__proto__就会指向这个对象，从而能够使用这个方法

```
function People(name, age, sex) {
    this.name = name;
    this.age = age;
    this.sex = sex;
}
People.prototype.sayHello = function () {
    console.log("你好我是" + this.name + "！我的年龄是" + this.age);
}

// 实例化两个对象
var h1 = new People("小明", 19, "男");
var h2 = new People("小红", 12, "女");

// 对象打点调用他们的方法
xiaoming.sayHello();   //你好我是小明！我的年龄是19
xiaohong.sayHello();   //你好我是小红！我的年龄是12

console.log(h1.sayHello === h2.sayHello); //true
```

#### 4. hasOwnProperty()方法

> 可以检测一个属性是存在于实例中，还是存在于原型中。这个方法(不 要忘了它是从 Object 继承来的)只在给定属性存在于对象实例中时，才会返回 true。

```
function Person() {

}
Person.prototype.name = "Nicholas"; Person.prototype.age = 29;
Person.prototype.job = "Software Engineer";
Person.prototype.sayName = function () {
    console.log(this.name);
}

var person1 = new Person();
var person2 = new Person();
console.log(person1.hasOwnProperty("name"));  //false
person1.name = "Greg";
console.log(person1.name); //"Greg"——来自实例
console.log(person1.hasOwnProperty("name")); //true
console.log(person2.name); //"Nicholas"——来自原型
console.log(person2.hasOwnProperty("name")); //false
delete person1.name;
console.log(person1.name); //"Nicholas"——来自原型
console.log(person1.hasOwnProperty("name")); //false
```

## 面向对象
1. [为圆选坑](https://github.com/Alley23/javascript_demo_list/tree/master/%E9%9D%A2%E5%90%91%E5%AF%B9%E8%B1%A1/%E4%B8%BA%E5%9C%86%E9%80%89%E5%9D%91)
2. [carousel-图文轮播](https://github.com/Alley23/javascript_demo_list/tree/master/%E9%9D%A2%E5%90%91%E5%AF%B9%E8%B1%A1/carousel-%E5%9B%BE%E6%96%87%E8%BD%AE%E6%92%AD)
