# 函数this（上下文）总结


> 函数的this是什么，取决于函数怎么调用！！而不是函数如何定义！！
> 函数的this是函数的调用时表现的性质，不是函数定义的时候写死的性质！！

### 1. 函数使用圆括号调用，函数的this就是window对象
```
function() {
    var a = 10;
    console.log(this.a)  //实际上访问的是window.a
}
var a = 20;
fun()   //20
```
- 函数function fun() {}的this不要看他怎么定义，要看他怎么调用； 此时函数是fun() 函数名加圆括号直接调用，此时this就是window对象。

### 2. 函数作为一个对象的方法，对象打点调用，函数的this就是这个对象
> 对象.函数()

```
function() {
    console.log(this.a);
}
var obj = {
    "a" : 10,
    "b" : 20,
    "c" : fn   //对象方法值为函数
}
obj.c()   //10
```
- 我们要看清楚函数执行的时候，是怎么执行的！！
- 现在不是圆括号直接执行！！而是一个对象打点调用这个函数执行，所以函数的上下文是obj对象！！！

### 3. 函数是事件处理函数，函数的this就是触发这个事件的对象
```
//定义了一个btnEvent，然后把这个btnEvent当做了2个DOM元素的事件处理函数：
function btnEvent() {
    this.style.background = "#999";
}

var box1 = document.getElementById("box1");
var box2 = document.getElementById("box2");

//把同一个函数绑定给不同的对象
box1.onclick = btnEvent;
box2.onclick = btnEvent;

//函数不会执行，直到用户点击了某一个div标签。此时点击谁，this就是谁。
```

### 4. 定时器调用函数，上下文是window对象

```
function fun() {
    console.log(this.a);
}
var a = 99;
setInterval(fun, 1000)

//函数fun被定时器调用，此时函数的this就是window对象。每秒钟打印出99.

```

```
//定时器在事件中使用


//错误的写法
var box1 = document.getElementById("box1");
box1.onclick = function(){
    setTimeout(function(){
        this.style.background = "red";
    },2000);
}
//定时器里面的函数调用者是定时器，所以this上下文就是window对象
//解决办法： 备份this


//正确的写法
var box1 = document.getElementById("box1");

box1.onclick = function(){
    var self = this;        //备份this，定时器里面的this就是我们的box1了
    setTimeout(function(){
        self.style.background = "red";
    },2000);
}
```

### 5. 数组中存放的函数，被数组索引之后加圆括号调用，this就是这个数组

```
function fun() {
    console.log(this == arr)  //true
    console.log(this.length)  //3
}
var arr = [fun, "w", "e"]

arr[0]()

//此时这个函数是从数组中枚举出来然后加圆括号执行的，所以最终调用者可以认为是这个数组，上下文就是这个数组。
```

### 6. call()和apply()

- 这两个函数都是函数的方法，只有函数能够打点调用call()、apply()，表示用指定的上下文执行这个函数。
- 语法： 函数.call(上下文) || 函数.apply(上下文)
- 区别： 体现在参数上。此时我们要执行的fun函数可以接受参数，apply需要用数组体现这些参数，而call必须用逗号隔开，罗列所有参数：


```
function fun(a,b,c){
    console.log(a+b+c);
    console.log(this.age);
}

var obj = {
    "name" : "小明",
    "age" : 12
}

fun.call(obj,6,7,8);  // 21  12
fun.apply(obj,[6,7,8]);  // 21  12
```

### 函数的arguments
- 首先说说什么是arguments.callee。在函数内部，如果想得到函数自身，用this是不可能的。我们必须使用arguments.callee
```
function fun(){
    console.log(arguments.callee === fun);  //true
}

fun();  //true，因为arguments.callee就是fun自己
```
```
function fun(a,b,c,d,e,f){
    console.log(arguments.callee.length);  //6
    console.log(arguments.length);         //3
}

fun(88,66,44);
```
> 函数的length是形参列表的长度，就是函数定义的时候写在fun()圆括号里面的字母个数。无视你的实参个数！也就是说：
> arguments.callee.length   形参列表的个数。
> arguments.length          实参个数，就是调用函数的时候传进来的实参个数。

### 用new运算符来调用函数(构造函数说明)
