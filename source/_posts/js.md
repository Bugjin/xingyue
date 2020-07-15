---
title: JavaScript数组方法操作集合（多种数组去重、reduce、排序）

---





JavaScript 数组知识大扫盲，几乎包括了目前所有的操作方式，虽然很简单基础，但是却很重要！  

*JS 中的 Array 方法新建数组常规方式*

## 新建数组


    // 先创建数组对象，再赋值 
    let temp = new Array();
    temp[0] = 123;
    temp[1] = "string";
    temp[2] = true;
    console.log(temp[0]); // 123
    console.log(temp[3]); // undefined
    
    let temp2 = new Array(2);// 规定了数组的长度为2
    temp2[0] = 123;
    temp2[1] = "string";
    temp2[2] = true; //虽然规定了数组长度，但仍可以再次添加元素，定义的数组大小对此没有影响
### 简洁方式 ###


    // 直接实例化创建 
    let temp = new Array(123, "string", true);
### 数组文本方式 ###


`let temp = [123, "string", true];`

> 这里有几个地方需要注意~
	
- 出于简洁、可读性和执行速度的考虑，推荐使用最后一种数组文本方法。
- 数组内可以存放任意类型的数据
- 数组元素不赋值，则为 undefined
- 访问数组范围以外的元素时，不会出现越界异常，为undefined
- 定义了数组大小，依然可以添加更多的元素

## 增删改查 ##


### 栈方法 push & pop 增删数组元素 ###
    
      // push()函数 
      let temp = [123, "string", true];
    
      let push1 = temp.push(456); // 插入一个元素
      console.log(push1, temp); // 4, [123, "string", true, 456]
    
      let push2 = temp.push(789, "string2", false); // 插入多个元素
      console.log(push2, temp); // 7, [123, "string", true, "456", 789, "string2", false]
    
      // pop()函数  
      let temp2 = [123];
    
      let pop1 = temp2.pop();
      console.log(pop1, temp2); // true, [];
    
      let pop2 = temp2.pop();
      console.log(pop2, temp2); // undefined, []; 


- 这两个方式都是对数组尾部进行压入和弹出操作。

- push(arg1, arg2, …)可以每次压入一个或多个元素，并返回更新后的数组长度。


- pop()函数则每次只会弹出尾部的元素，并返回弹出的元素，若对空数组调用 pop()则返回 undefined。会更改源数组。
### 队列方法 shift & unshift 增删数组元素 ###
    
      // unshift()函数 
      let temp = [123, 456, 789];
      let unshift1 = temp.unshift("abc", "efg");
      console.log(unshift1, temp); // 5, ["abc", "efg", 123, 456, 789]
    
      // shift()函数 
      let temp2 = [123, 456, 789];
      let shift1 = temp2.shift();
      console.log(shift1, temp2); // 123, [456, 789]
    

- 这两个方式都是对数组头部进行位移与弹出操作。

- unshift(arg1, arg2, …)可以像数组的头部添加一个或多个元素，并返回更新后的数组长度，并把所有其他元素位移到更高的索引。

- shift()方法会删除首个数组元素，并返回弹出的元素，并把所有其他元素位移到更低的索引。会更改源数组。
### delete 删除数组元素 ###
JS 数组属于对象，所以可以使用 JavaScript delete 运算符来删除，但这种方式会在数组留下未定义的空洞，所以很少使用。 会更改源数组。

    
    let temp = [123, 456, 789];
    delete temp[1];
    console.log(temp.length, temp[1]); // 3, undefined
### splice增删数组元素 ###
splice(arg1, arg2, arg3, …)第一个参数定义了新添加元素的位置，第二个参数定义应删除多少元素，其余参数定义要添加的元素，并返回一个包含已删除项的数组。
splice 还可以在数组不留空洞的情况下删除元素。会更改源数组。

    
      // 添加新元素，并删除已有元素 
      let temp1 = [1, 2, 3, 4, 5, 6];
      let splice1 = temp1.splice(1, 2, 7, 8, 9);
      console.log(splice1, temp1); //[2, 3],[1, 7, 8, 9, 4, 5, 6]
    
      // 只添加新元素，不删除元素 
      let temp2 = [1, 2, 3, 4, 5, 6];
      let splice2 = temp2.splice(1, 0, 7, 8);
      console.log(splice2, temp2);//[], [1, 7, 8, 2, 3, 4, 5, 6]
    
      // 不添加新元素，只删除元素 
      let temp3 = [1, 2, 3, 4, 5, 6];
      let splice3 = temp3.splice(1, 2);
      console.log(splice3, temp3);//[2, 3], [1, 4, 5, 6]
### concat 合并数组 ###
合并现有数组来创建一个新的数组，concat(arg1, arg2, …)不会更改现有数组，总是返回一个新的数组，可以使用任意数量的数组参数。不会更改源数组。
    
    
    let temp1 = [1, 2];
    let temp2 = [3, 4];
    let temp3 = [5];
    let concat1 = temp1.concat(temp2, temp3);
    console.log(concat1, temp1, temp2); // [1,2,3,4,5], [1,2],[3,4]
### 操作符...合并数组，不会更改源数组。 ###
    
    
    let temp1 = [1,2,3];
    let temp2 = [4,5,6];
    let arr = [...temp1, ...temp2];
    console.log(arr); //[1,2,3,4,5,6]
    ### slice 裁剪数组 ###
slice(arg1, arg2) 方法用数组的某个片段切出新数组，不会修改源数组中的任何元素，返回一个新数组，第一个参数为元素选取开始位置，第二个参数为元素选取结束位置，如果第二个参数被省略则会切除数组的剩余部分。不会更改源数组。

    
    let temp = [1,2,3,4,5,6,7,8];
    let slice1 = temp.slice(2, 4);
    console.log(slice1, temp); //[3, 4],[1,2,3,4,5,6,7,8];
    
    let slice2 = temp.slice(4);
    console.log(slice2); //[5,6,7,8]
### 查找定位Math.max 查数组最大值 ###
Math.max.apply(arg1,arg2)参数不支持数组，所以可以用Math.max.apply(null,arr)来获取数组中的最大值。

    
    let temp = [1,3,6,2,8,4];
    let max1 = Math.max.apply(null, temp);
    console.log(max1); // 8
### Math.min 查数组最小值 ###
Math.min.apply(arg1,arg2)参数不支持数组，所以可以用Math.min.apply(null,arr)来获取数组中的最小值。

    
    let temp = [1,3,6,2,8,4];
    let min1 = Math.min.apply(null, temp);
    console.log(min1); // 1

### JavaScript 方法查数组最大值 ###

    
    function getArrayMaxValue(arr) {
    var len = arr.length
    var max = -Infinity;
    while (len--) {
    if (arr[len] > max) {
    max = arr[len];
    }
    }
    return max;
    }
    let temp = [1,3,6,2,8,4];
    let max1 = getArrayMaxValue(temp);
    console.log(max1);// 8
### JavaScript 方法查数组最小值 ###

    
    function getArrayMinValue(arr) {
    var len = arr.length
    var min = Infinity;
    while (len--) {
    if (arr[len] < min) {
    min = arr[len];
    }
    }
    return min;
    }
    let temp = [1,3,6,2,8,4];
    let min1 = getArrayMinValue(temp);
    console.log(min1);// 1
### 查找索引 ###
    
    let temp = [1,2,3,4,5,4,3,2];
    let pos1 = temp.indexOf(4);
    console.log(pos1); //3
    
    let pos2 = temp.lastIndexOf(4);
    console.log(pos2);//5
    
    let temp = [1,35,67,8];
    
    //返回第一个大于10的元素索引 
    let findIndex1 = temp.findIndex(function(value){
    return value > 10;
    });
    console.log(findIndex1); //1
- indexOf(arg1, arg2)方法在数组中搜索元素值并返回其位置。arg1 为搜索元素，arg2 可选从哪里开始搜索。负值将从结尾开始的给定位置开始，并搜索到结尾。
- lastIndexOf(arg1,arg2) 与 indexOf() 类似，但是从数组结尾开始搜索。arg2 可选从哪里开始搜索。负值将从结尾开始的给定位置开始，并搜索到开头。
- findIndex() 方法返回通过测试函数的第一个数组元素的索引。

### 查找值 ###
find(function(arg1,arg2,arg3)) 方法返回通过测试函数的第一个数组元素的值。arg1 为数组元素值， arg2 为数组元素索引，arg3 为数组本身。

    
    let temp = [1,35,67,8];
    
    // 返回第一个大于10的值 
    let find1 = temp.find(function(value){
    return value > 10;
    });
    console.log(find1);//35

*这里需要注意几个点哦！* 
- splice 和 slice 容易混淆，记住 splice 翻译是拼接，slice 翻译是切片。
	
- splice 会返回被删除元素组成的数组，或者为空数组

- pop,shift 会返回那个被删除的元素
	
- push,unshift 会返回新数组长度
	 
- pop,push,shift,unshift,splice 会改变源数组
	
- indexOf,lastIndexOf,concat,slice 不会改变源数组

### 数组转换toString 数组转字符串 ###
toString()方法把每个元素转换为字符串，然后以逗号连接输出显示， 不会更改源数组。
    
    
    // toString()方法把每个元素转换为字符串，然后以逗号连接输出显示
    let temp = [1,2,3,4];
    let toString1 = temp.toString();
    console.log(toString1, temp);//1,2,3,4   [1,2,3,4]
### join 数组转字符串 ###
join()方法可以把数组转换为字符串，不过它可以指定分隔符。
在调用 join() 方法时，可以传递一个参数作为分隔符来连接每个元素。
如果省略参数，默认使用逗号作为分隔符，这时与toString()方法转换操作效果相同。不会更改源数组。
    
    
      let temp = [1,2,3,4];
      let join1 = temp.join();
      let join2 = temp.join("*");
      console.log(join1, join2); //1,2,3,4   1*2*3*4
### split 字符串转数组 ###
split(arg1, arg2)方法是 String 对象方法，与 join()方法操作正好相反。该方法可以指定两个参数，第一个参数为分隔符，指定从哪儿进行分隔的标记；第二个参数指定要返回数组的长度。

    
    let temp = "1-2-3-4-5";
    let split1 = temp.split("-");
    let split2 =temp.split("-", 2);
    console.log(split1, split2);//[1,2,3,4,5],[1,2]
### 对象转数组 ###

    
    let temp = {key1: "value1", key2: "value2"};
    
    // 对象的键组成数组 
    let trans1 = Object.keys(temp);
    console.log(trans1, temp);//["key1", "key2"],  {key1: "value1", key2: "value2"}
    
    // 对象的值组成数组 
    let trans2 = Object.values(temp);
    console.log(trans2); //["value1", "value2"]
    
    // 键值对组成的数组 
    let trans3 = Object.entries(temp);
    console.log(trans3); //[["key1", "value1"], ["key2", "value2"]]
### 数组转对象 ###


    let temp = ["a","b"];
    let trans1 = {...temp};
    console.log(trans1, temp); // {0: "a", 1: "b"}, ["a","b"]
    
    let trans2 = Object.assign({}, temp);;
    console.log(trans2, temp); //{0: "a", 1: "b"}, ["a","b"]
    
    // 上面方法要注意temp位置，如果位置放错则不能成功转换，如下 
    let trans3 = Object.assign(temp, {});
    console.log(trans3, temp); // ["a","b"], ["a","b"]

*注意*

- toString, join 不会改变源数组数组排序sort 数组排序
- sort 按照字母顺序对数组进行排序, 直接修改了源数组，所以可以不用再将返回值赋给其他变量。
该函数很适合字符串排序，如果数字按照字符串来排序，则 "25" 大于 "100"，因为 "2" 大于 "1"，正因如此，sort()方法在对数值排序时会产生不正确的结果。
- 可以通过修正比值函数对数值进行排序。比较函数的目的是定义另一种排序顺序。比较函数应该返回一个负，零或正值，当 sort() 函数比较两个值时，会将值发送到比较函数，并根据所返回的值（负、零或正值）对这些值进行排序。会更改源数组。 

如下 
    
    let temp = ["bi", "ci", "ai", "di"];
    let sort1 = temp.sort(); // 可以不用复制给sort1, 直接执行temp.sort()这里是为方便大家直观比较
    console.log(sort1, temp); // ["ai","bi","ci","di"], ["ai","bi","ci","di"]
    
    
    
    // sort比值函数修正：降序
    let temp = [40, 100, 1, 5, 25, 10];
    temp.sort(function(a, b){
    return b-a
    });
    console.log(temp); // [100, 40, 25, 10, 5, 1]
    
    // sort比值函数修正：升序 
    let temp = [40, 100, 1, 5, 25, 10];
    temp.sort(function(a, b){
    return a-b;
    });
    console.log(temp); // [1, 5, 10, 25, 40, 100]
    reverse 数组反转
    reverse()反转数组中的元素，直接修改了源数组。
    
    
    let temp = [1,3,2,4];
    temp.reverse();
    console.log(temp); //[4,2,3,1];

*注意 * 

- sort,reverse 会更改源数组
- 数组迭代：数组迭代即对每个数组项进行操作
- forEach(function(arg1,arg2,arg3){})方法为每个数组元素调用一次函数（回调函数），arg1 为数组元素值， arg2 为数组元素索引，arg3 为数组本身， 此方法不会更改源数组，也不会创建新数组。
    
如下 
  
    let temp = [1,3,5];
    temp.forEach(function(value, index, array){
    console.log(value, index, array);
    });
    /***
    * 1 0 [1,3,5]
    * 3 1 [1,3,5]
    * 5 2 [1,3,5]
    ***/
### Array.map() ###
map(function(arg1,arg2,arg3){})方法通过对每个数组元素执行函数来创建新数组，arg1 为数组元素值， arg2 为数组元素索引，arg3 为数组本身，方法不会对没有值的数组元素执行函数，不会更改源数组，创建一个新数组。
    
    
    let temp = [1, 3, 5, , 9];
    
    //index， value不用时可以省略
    let map1 = temp.map(function(value, index, array){ 
    return value*2
    });
    console.log(map1); // [2, 6, 10, empty, 18]
### Array.filter() ###
filter(function(arg1,arg2,arg3){})方法创建一个包含通过指定条件的数组元素的新数组, arg1 为数组元素值， arg2 为数组元素索引，arg3 为数组本身，不会更改源数组。
    
    
    let temp = [1, 3, 5, 7, 9];
    let filter1 = temp.filter(function(value){
    return value > 5;
    });
    console.log(filter1); // [7, 9]
### Array.every() ###
every(function(arg1,arg2,arg3){})方法测试数组的所有元素是否通过了置顶条件。arg1 为数组元素值， arg2 为数组元素索引，arg3 为数组本身。不会更改源数组。


    let temp = [3, 5, 7, 9];
    
    // 检查所有元素是否都大于1 
    let every1 = temp.every((value) => {
    return value > 1;
    });
    console.log(every1); //true
### Array.some() ###
some(function(arg1,arg2,arg3){})方法测试数组中是否有元素通过了指定条件的测试。不会更改源数组。
    
    
    let temp = [3, 5, 7, 9];
    
    // 检测数组中是否包含大于6的元素 
    let some1 = temp.some(function(value){
    return value > 6;
    });
    console.log(some1); // true
### Array.reduce() ###
reduce(function(arg1,arg2,arg3,arg4){})接收一个函数作为累加器（accumulator），数组中的每个值（从左到右）开始缩减，最终为一个值。
arg1 上一次调用回调返回的值，或者是提供的初始值（initialValue）,arg2 为数组元素值， arg3 为数组元素索引，arg4 为数组本身。不会更改源数组。

    
      let temp = [3, 5, 7, 9];
      let reduce1 = temp.reduce(function(a,b){
      console.log(a,b);
      return a+b;
      });
      console.log(reduce1);
      /***
      * 3 5
      * 8 7
      * 15 9
      * 24
      ***/
### 普通 for 循环 ###
性能比较好
    
    
    let temp = [1,2,3,4];
    for(let i=0,len=temp.length;i<len;i++) {
    console.log(temp[i]);
    }
    //1 2 3 4
### for…in ###

    
    let temp = [1,22,33,4];
    for(let i in temp){
    console.log(i, temp[i]);
    }
    //0 1
    //1 22
    //3 22
    //4 4
### for…of ###
for..of 是 es6 中引进的循环，主要是为了补全之前 for 循环中的以下不足
    
    
    let temp = [1,2,3,4];
    for(let i of temp){
    console.log(i);
    }
    //1 2 3 4
    跳出循环forEach跳出循环
    
    
    let temp = [1,2,3,4];
    let arr = [];
    temp.forEach((value, index) =>{
    if(index === 1){
    // break;
    // continue;
    // return;
    // return true;
    return false;
    }
    arr.push(value);
    });
    console.log(arr);
    /***
    * break: Uncaught SyntaxError: Illegal break statement 不合法
    * continue: Uncaught SyntaxError: Illegal continue statement 不合法
    * return: [1,3,4] 跳出本次循环
    * return true: [1,3,4] 跳出本次循环
    * return false: [1,3,4] 跳出本次循环
    ***/
### map跳出循环 ###

    
    let temp = [1,2,3,4];
    let arr = temp.map((value, index) =>{
    if(index === 1){
    // break;
    // continue;
    // return;
    // return true;
    // return false;
    }
    return value;
    });
    console.log(arr);
    /***
    * break: Uncaught SyntaxError: Illegal break statement 不合法
    * continue: Uncaught SyntaxError: Illegal continue statement 不合法
    * return: [1,undefined,3,4] 跳出本次循环
    * return true: [1,true,3,4] 跳出本次循环
    * return false: [1,false,3,4] 跳出本次循环
    ***/
### filter跳出循环 ###

    
    let temp = [1,9,2,3,4];
    let arr = temp.filter((value, index) =>{
    if(index === 1){
    // break;
    // continue;
    // return;
    // return true;
    // return false;
    }
    return value > 2;
    });
    console.log(arr);
    /***
    * break: Uncaught SyntaxError: Illegal break statement 不合法
    * continue: Uncaught SyntaxError: Illegal continue statement 不合法
    * return: [3,4] 跳出本次循环
    * return true: [9,3,4] 跳出本次循环, 返回了9是因为return true符合条件
    * return false: [3,4] 跳出本次循环
    ***/
### every跳出循环 ###

    
    let temp = [1,9,2,3,4];
    let arr = [];
    temp.every((value, index) =>{
    if(index === 1){
    // break;
    // continue;
    // return;
    // return true;
    // return false;
    }
    arr.push(value);
    return true; // every遇到return false会跳出循环,方便测试这里返回return true
    });
    console.log(arr);
    /***
    * break: Uncaught SyntaxError: Illegal break statement 不合法
    * continue: Uncaught SyntaxError: Illegal continue statement 不合法
    * return: [1] 成功跳出循环
    * return true: [1,2,3,4] 跳出本次循环
    * return false: [1] 成功跳出循环
    ***/
### some跳出循环 ###

    
    let temp = [1,9,2,3,4];
    let arr = [];
    temp.some((value, index) =>{
    if(index === 1){
    // break;
    // continue;
    // return;
    // return true;
    // return false;
    }
    arr.push(value);
    return false; // every遇到return true会跳出循环,方便测试这里返回return false
    });
    console.log(arr);
    /***
    * break: Uncaught SyntaxError: Illegal break statement 不合法
    * continue: Uncaught SyntaxError: Illegal continue statement 不合法
    * return: [1,2,3,4] 跳出本次循环
    * return true: [1] 成功跳出循环
    * return false: [1,2,3,4]跳出本次循环
    ***/
### for跳出循环 ###


    let temp = [1,9,2,3,4];
    let arr = [];
    for(let i = 0; i  < temp.length; i++){
    if(i === 1){
    // break;
    // continue;
    // return;
    // return true;
    // return false;
    }
    arr.push(temp[i]);
    }
    console.log(arr);
    /***
    * break: [1] 成功跳出循环
    * continue: [1,2,3,4] 跳出本次循环
    * return: Uncaught SyntaxError: Illegal return statement 不合法
    * return true: Uncaught SyntaxError: Illegal return statement 不合法
    * return false: Uncaught SyntaxError: Illegal return statement 不合法
    ***/
### for…in跳出循环 ###

    
    let temp = [1,9,2,3,4];
    let arr = [];
    for(let index in temp){
    if(index === 1){
    // break;
    // continue;
    // return;
    // return true;
    // return false;
    }
    arr.push(temp[index]);
    }
    console.log(arr);
    /***
    * break: [1,9,2,3,4] 无效
    * continue: [1,9,2,3,4] 无效
    * return: Uncaught SyntaxError: Illegal return statement 不合法
    * return true: Uncaught SyntaxError: Illegal return statement 不合法
    * return false: Uncaught SyntaxError: Illegal return statement 不合法
    ***/
### for…of跳出循环 ###
    
    
    let temp = [1,9,2,3,4];
    let arr = [];
    let index =1
    for(let value of temp){
    if(value === 9){
    // break;
    // continue;
    // return;
    // return true;
    // return false;
    }
    arr.push(value);
    }
    console.log(arr);
    /***
    * break: [1] 成功跳出循环
    * continue: [1,2,3,4] 跳出本次循环
    * return: Uncaught SyntaxError: Illegal return statement 不合法
    * return true: Uncaught SyntaxError: Illegal return statement 不合法
    * return false: Uncaught SyntaxError: Illegal return statement 不合法
    ***/
汇总表格



这里有几个需要注意的点~

- forEach,map,filter,every,some,reduce 这些迭代方法不会改变源数组

- some 在有 true 的时候停止

- every 在有 false 的时候停止

### 其他常用操作检测数组 ###

    
    let temp1 = [1,2,4];
    let temp2 = 5;
    
    // instanceof 测试某个对象是否由某个指定的构造器创建 
    console.log(temp1 instanceof Array); // true
    console.log(temp2 instanceof Array); //false
    
    // Array.isArray 比instanceof更可靠  
    console.log(Array.isArray(temp1)); //true
    console.log(Array.isArray(temp2)); //false
    
    // Object对象的toString()方法，可以返回所创建对象的内部类名 
    console.log(Object.prototype.toString.call(temp1)); //[object Array]
    console.log(Object.prototype.toString.call(temp2)); // [object Number]
### 洗牌算法 ###
将一个数组打乱,返回一个打乱的数组

    
    let temp = [1,3,5,6,7,2,4];
    temp.sort(() => {
    return Math.random() - 0.5;
    })
    console.log(temp);
    ### 数组去重 ###
    
    
    let temp = [1,3,5,6,7,9,4,3,1,6];
    
    // es6的set方法
    let unique1 = Array.from(new Set(temp));
    console.log(unique1);//[1, 3, 5, 6, 7, 9, 4]
    
    // es6的set方法 
    let unique2 = [...new Set(temp)];
    console.log(unique2);//[1, 3, 5, 6, 7, 9, 4]
    
    // 遍历数组法: 先创建一个新的空数组用来存储新的去重的数组，然后遍历arr数组，在遍历过程中，分别判断newArr数组里面
    //是不是有遍历到的arr中的元素，如果没有，直接添加进newArr中，如果已经有了（重复），那么不操作。
    let newArr = [];
    for(let i=0; i<temp.length;i++){
    if(newArr.indexOf(temp[i]) === -1){
    newArr.push(temp[i]);
    }
    }
    console.log(newArr);//[1, 3, 5, 6, 7, 9, 4]
    
    // 数组下标判断法: 如果在arr数组里面找当前的值，返回的索引等于当前的循环里面的i的话，那么证明这个值是第一次出现，
    //所以推入到新数组里面，如果后面又遍历到了一个出现过的值，那也不会返回它的索引，indexof()方法只返回找到的第一个值的索引，所以重复的都会被pass掉，只出现一次的值都被存入新数组中。 
    let newArr = [];
    for(let i=0; i<temp.length;i++){
    if(temp.indexOf(temp[i]) === i){
    newArr.push(temp[i]);
    }
    }
    console.log(newArr);//[1, 3, 5, 6, 7, 9, 4]
    
    // 排序后相邻去除法: 先用sort()方法把arr排序，那么排完序后，相同的一定是挨在一起的，把它去掉就好了。首先给新数组
    //初始化一个arr[0]，因为我们要用它和arr数组进行比较，所以，for循环里面i也是从1开始了，我们让遍历到的arr中的值和
    //新数组最后一位进行比较，如果相等，则pass掉，不相等的，push进来 
    let arr = [1,3,5,6,7,9,4,3,1,6];
    arr.sort();
    let newArr = [arr[0]];
    for(let i=1; i<arr.length;i++){
    if(arr[i] !== newArr[newArr.length - 1]){
    newArr.push(arr[i]);
    }
    }
    console.log(newArr); //[1, 3, 4, 5, 6, 7, 9]
    
    // 双层for循环去重 
    let arr = [1,3,5,6,7,9,4,3,1,6];
    for(let i=0; i<arr.length;i++){
    for(let j=i+1; j<arr.length; j++){
    if(arr[i] === arr[j]){
    arr.splice(j,1);
    j--;
    }
    }
    }
    console.log(arr);// [1, 3, 5, 6, 7, 9, 4]
### 数组去虚值 ###
虚值有 false, 0，''， null, NaN, undefined
    
    
    let temp = [1,2,"",4,undefined,5, false,0,null,NaN];
    let newArr = temp.filter((value) => {
    return value;
    })
    console.log(newArr); //[1,2,4,5]
    用数据填充数组
    
    
    let  arr = new Array(5).fill(1);
    console.log(arr);//[1,1,1,1,1]
    数组中获取随机值根据数组长度获取一个随机索引。
    
    
    let arr = ['a','b','c','d'];
    let randomIndex = Math.floor(Math.random()*arr.length);
    let randomValue = arr[randomIndex];
    console.log(randomIndex, randomValue); // 2 c
## 总结 ##
上面的 JavaScript 数组知识点虽然不难，但是却很容易弄混淆，小伙伴们一定要注意哦~

	






