# 数组的操作方法（Array）

#### 一. Arry 对象属性
1. length ：设置或返回数组中元素的数目

    ```
    var arr = [1,2,3,4,5,6]
    console.log(arr.length) //6
    ```
#### 二. Array 方法

##### 1. concat()
- 连接两个或更多的数组，并返回结果
    ```
    var arr = [1,2,3]
    var arr1 = ["w"]
    console.log(arr.concat("s", arr1)) //[1,2,3,"s"]
    //
    ```
#####  2. join()
- 把数组的所有元素放入一个字符串。元素通过指定的分隔符进行分隔。
    ```
    var arr = ["q","w","e"]
    console.log( arr.join() ) //q,w,e
    console.log( arr.join("*") ) //q*w*e
    ```


##### 3. toString()
- 把数组转换为字符串，并返回结果。
    ```
    var arr = ["q","w","e"]
    console.log(arr.toString()) //q,w,e
    ```

##### 4. pop()
- 删除并返回数组的最后一个元素

    ```
    var arr = ["q","w","e"]
    console.log(arr.pop()) // e
    ```
##### 5. push()
- 向数组的末尾添加一个或更多元素，并返回新的长度。
    ```
    var arr = ["q","w","e"]
    console.log(arr.push("r"))   // 4
    console.log(arr)             // [q", "w", "e", "r"]
    //
    ```
##### 6. shift()
- 删除并返回数组的第一个元素
    ```
    var arr = ["q","w","e"]
    console.log(arr.shift()) // q
    ```


##### 7. unshift()
- 向数组的开头添加一个或更多元素，并返回新的长度。
    ```
    var arr = ["q","w","e"]
    console.log(arr.unshift("t")) // 4
    console.log(arr)              // ["t", "q", "w", "e"]
    //
    ```

##### 8. slice()
- 从某个已有的数组返回选定的元素
- arr.slice(start,end)
- 只有一个参数：
- 1）为正：从为该参数的下表一直截取到最后；
    ```
    var arr = ["q","w","e","r","t"]
    console.log(arr.slice(2))         //["e", "r", "t"]
    //
    ```
- 2）为负：从倒数第几个元素截取到最后
    ```
    var arr = ["q","w","e","r","t"]
    console.log(arr.slice(-2))        //["r", "t"]
    ```
- 两个参数
- 1）为正：表示表示从第一个为第一个参数的下标截取到为最后一个参数下标
    ```
    var arr = ["q","w","e","r","t"]
    console.log(arr.slice(2,4))      //["e", "r"]
    ```
- 2）一正一负：表示表示从第一个为第一个参数的下标截取到从倒数为第二个参数的地方；
    ```
    var arr = ["q","w","e","r","t"]
    console.log(arr.slice(1, -1))    //["w", "e", "r"]
    ```
- 3）两个都为负：从倒数第一个参数绝对值的位置截取到第二个参数绝对值的位置（第二个参数的绝对值不小于第一个参数的绝对值）
    ```
    var arr = ["q","w","e","r","t"]
    console.log(arr.slice(-2, -1))       //["r"]
    ```
##### 9. reverse()
    * 颠倒数组中元素的顺序。
    ```
    var arr = ["q","w","e","r","t"]
    console.log(arr.reverse())     //["t", "r", "e", "w", "q"]
    ```
##### 10. sort()
- 对数组的元素进行排序
- 1）如果没有参数，将按字母顺序对数组中的元素进行排序，说得更精确点，是按照字符编码的顺序进行排序。（把数组的元素都转换成字符串）
    ```
    var arr = [0, 10, 2, 4, 3, 6]
    console.log(arr.sort()) //[0, 10, 2, 3, 4, 6]


    var arr = ["a", "b", "d", "e", "c"]
    console.log(arr.sort()) //["a", "b", "c", "d", "e"]
    ```
- 2)如果想按照其他标准进行排序，就需要提供比较函数，该函数要比较两个值，然后返回一个用于说明这两个值的相对顺序的数字。比较函数应该具有两个参数 a 和 b，其返回值如下：
    ```
    // 若 a 小于 b，在排序后的数组中 a 应该出现在 b 之前，则返回一个小于 0 的值。
    // 若 a 等于 b，则返回 0。
    // 若 a 大于 b，则返回一个大于 0 的值。
    function sortNumber(a,b) {
    	return a - b
    }
    var arr = [1, 3, 5, 8, 10, 23, 44]
    arr.sort(sortNumber) //[1, 3, 5, 8, 10, 23, 44]

    function sortNumber(a,b) {
    	return b - a
    }
    var arr = [1, 3, 5, 8, 10, 23, 44]
    console.log( arr.sort(sortNumber)) //[44, 23, 10, 8, 5, 3, 1]
    ```
##### 11. splice()
- 向/从数组中添加/删除项目，然后返回被删除的项目
- 1-1)一个参数表示从为该参数的下标截取到最后
    ```
    var arr = [1,2,3,4,5,6]
    console.log(arr.splice(1)) //[2, 3, 4, 5, 6]
    console.log(arr)           //[1]
    ```
- 1-2)一个参数为负表示从后面为第一个参数开始截取到最后
    ```
    var arr = [1,2,3,4,5,6]
    console.log(arr.splice(-1)) //[6]
    console.log(arr)            //[1, 2, 3, 4, 5]
    ```
-  2-1） 两个参数表示从为以一个参数的下标向后截取为第二个参数个
    ```
    var arr = [1,2,3,4,5,6]
    console.log(arr.splice(2, 4)) //[3, 4, 5, 6]
    console.log(arr) //[1, 2]
    ```
- 2-2) 一正一负表示从后面为第一个参数开始截取为第二个参数的个数
    ```
    var arr = [1,2,3,4,5,6]
    console.log(arr.splice(-4, 2))  //[3,4]
    console.log(arr)                //[1,2,5,6]
    ```
- 3)三个参数
- 第一个参数表示开始的下标位置，第二个参数表示从为第一个参数的下标开始替换的个数，（0表示插入）； 第三个参数表示替换或插入的元素
    ```
    //第二个参数为0
    var arr = [1,2,3,4,5,6]
    arr.splice(1, 0, "w")
    console.log(arr)  //[1, "w", 2, 3, 4, 5, 6]

    //第二个参数不为0
    var arr = [1,2,3,4,5,6]
    arr.splice(1, 2, "w")
    console.log(arr)  //[1, "w", 4, 5, 6]
    ```
##### 12. toLocaleString()
- 把数组转换为本地字符串，并返回本地字符串表示。
    ```
    var arr = ["a", "b", "d", "e", "c"]
    console.log(arr.toLocaleString()) //a,b,d,e,c
    ```





[查看更多文章](https://alley23.github.io/)