## 字符串操作方法
- String 对象是 String
- 原始类型的对象表示法，它是以下方式创建的：

```
var str1 = new String("hello world!");
//普通写法
var str2 = "hello world!"
```
1. length属性
    * 返回值：返回字符串个数（每个空格也算一个）

```
var str = "wwww"
console.log(str.length)   // 4
```

2. valueOf() 方法和 toString() 方法
    * 返回值：stringObject 的原始字符串值

```
var str = "hello world!"
str.valueOf()  //"hello world!"
str.toString() //"hello world!"
console.log(str.valueOf() == str.toString()) //true
```
3. charAt() 和 charCodeAt() 方法
    * charAt() 返回的是指定位置的字符串
    * charCodeAt() 返回在指定的位置的字符的 Unicode 编码
    * 访问的是单个字符串的单个字符，这样两个方法都有一个参数（要操作字符的位置）

```
var str = "qwerty"
console.log( str.charAt(1) )  //w
console.log( str.charCodeAt(1) ) //119
```

4. concat() 方法
    * 连接字符串

```
var str = "ss"
var str2 = "ww"
console.log( str.concat("vv") )  //"ssvv"
console.log( str.concat(str2) )   // "ssww"
```

5. indexOf() 和 lastIndexOf() 方法
    * indexOf() 和 lastIndexOf() 方法返回的都是指定的子串在另一个字符串中的位置，如果没有找不到子串，则返回 -1。
    * 区别：indexOf() 方法是从字符串的开头（位置 0）开始检索字符串，而 lastIndexOf() 方法则是从字符串的结尾开始检索子串。

```
var str = "hello world!"
console.log( str.indexOf("d") )  // 10
console.log( str.lastIndexOf("d") )  // 1
```

6. slice() 和 substring()
    * 返回值： 一个新的字符串数
    * 参数： 接受一个或者两个参数，一个参数表示从该参数位置截取到最后，两个参数表示从第一个参数位置开始截取第二个参数的位置
    * 如果参数为负数，slice()表示从反方向截取; substring()会将负数解释为0，还会将小的数字作为起始位置;

```
var str = "hello world!"
console.log( str.slice(3) )         //输出 "lo world"
console.log( str.substring(3) )     //输出 "lo world"
console.log( str.slice(3, 7) )      //输出 "lo w"
console.log( str.substring(3, 7) )  //输出 "lo w"

//如果参数为负数，slice()表示从反方向截取; substring()会将负数解释为0，还会将小的数字作为起始位置;

var str = "hello world!"
console.log( str.slice(-3) )         //输出 "rld"
console.log( str.substring(-3) )     //解释为substring(0); 输出 "hello world"
console.log( str.slice(3, -4) )      //输出 "lo w"
console.log( str.substring(3, -4) )  //解释为substring(0, 3); 输出 "hel"
```

7. split()方法
    * 用于把一个字符串分割成字符串数组
    * 返回值： 一个字符串数组

```
var str = "hello world!"

console.log( str.split(" ") )  //["hello", "world!"]
console.log( str.split(" ") )  //["hello", "world!"]
```
8. toLowerCase()、toLocaleLowerCase()、toUpperCase() 和 toLocaleUpperCase()
    * 执行大小写转换
    * 返回值：一个新的字符串

```
var str = "hello world!"
console.log( str.toLocaleUpperCase() ) //输出 "HELLO WORLD!"
console.log( str.toUpperCase() )		//输出 "HELLO WORLD!"
console.log( str.toLocaleLowerCase() )	//输出 "hello world!"
console.log( str.toLowerCase() )		//输出 "hello world!"
```

9. match()
    * 字符串内检索指定的值，或找到一个或多个正则表达式的匹配
    * 但是它返回指定的值，而不是字符串的位置
    * 返回值： 存放匹配结果的数组

```
var str="1 plus 2 equal 3"
console.log( str.match(/plus/g) )   // ["plus"]
console.log( str.match(/\d+/g) )    //["1", "2", "3"]
```
10. search()
    * 返回第一个与 regexp 相匹配的子串的起始位置。
    * 如果没有找到任何匹配的子串，则返回 -1。

```
var str = "hello world!"
console.log( str.search(/world/) )  //6
console.log( str.search(/sds/) )    // -1
```
11. replace()
    * 返回一个新的字符串
    * 在字符串中用一些字符替换另一些字符，或替换一个与正则表达式匹配的子串


```
var newStr = str1.replace("hello", "你好")   //你好 world!
var newStr = str.replace(/l/g, "K")          //heKKo worKd!
```


```
//第一个参数是正则，第二个参数是带$符的字符串
var str3 = '这是一段原始文本,"3c这要替换4d"!';
var newStr = str3.replace( /([0-9])([a-z])/g,"$1" );
console.log( newStr );    //输出：    这是一段原始文本,"3这要替换4"!';
```
- 上面的例子，$1表示regexp中的第一个子表示即（[0-9]）匹配单个数字，同理若是$2则表示第二个子表示即（[a-z]）；所以，’3c’这个匹配到的整体被第一个子表示说表示的’3’替换，’4d’被第一个子表示匹配的数字’4’所替换。其他几个同理可得：

- （/([0-9])([a-z])/g,”$2″）—>////输出： 这是一段原始文本,”c这要替换d”!'; (3c和4d被相应的第二个子表示匹配出来的c和d替换)
- （/([0-9])([a-z])/g,”$'”）—>////输出： 这是一段原始文本,”这要替换d”!这要替换”!”!'; (3c被3c右侧文本替换，4d右侧是”!替换，所以出现俩次)


```
// 第一个参数是正则，第二个参数函数
var str4 = '这是一段原始文本，需要替换的内容"aa这要bbb替换ccccc"！';
var newStr = str4.replace( /[a-z]+/g,function ($0){
    var str = '';
    for (var i = 0; i < $0.length; i++) {
        str += '*';
    };
    return str;
} );
console.log( newStr );   //这是一段原始文本，需要替换的内容"**这要***替换*****"！
```
- 上面的例子函数的第一个参数为匹配的regexp的整体，根据长度函数返回值为相应替换的文本；




[查看更多文章](https://alley23.github.io/)