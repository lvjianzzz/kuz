## es6入门

### es6 简介

ECMAScript 6.0（以下简称 ES6）是 JavaScript 语言的下一代标准，已经在 2015 年 6 月正式发布了。它的目标，是使得 JavaScript 语言可以用来编写复杂的大型应用程序，成为企业级开发语言。

### let和const 

ES6 新增了`let/const`命令，用来声明变量。它的用法类似于`var`，但是所声明的变量，只在let命令所在的`代码块内`有效。代码块是在大括号 `{}` 中所写的语句,if语句和 for语句里面的{ }也属于块作用域。对于var, 在`function `内部， 加var的是局部变量， 不加var的则是 全局变量；

+ let声明变量及作用域
let不存在变量提升
```html
<!-- 这个例子表面let只在当前代码块内有效 -->
<script>
    {
        var a = 10;
        let b = 20;
        const c = 30;
        {
            console.log(b); // b is not defined
            let b = 30;
            console.log(b) // 30
        }
    }
    console.log(a)  // 10 
    console.log(b)  // b is not defined
    console.log(c)  // 因为上面报错 执行不了c
</script>
```


```html
<script>
  for (var i = 0; i < 10; i++) {
        setTimeout(function(){
            console.log(i)  // 10次10
        },1000)
      }
      for (let j = 0; j < 10; j++) {
        setTimeout(function(){
            console.log(j)  // 0,1,2,3,4,5,6,7,8,9
        },1000)
      }
</script>
```
+ let/const

let/const声明的变量不能重新被定义 let 可以重新赋值  const不可以赋值 

``` html
<script>
// let i = 10;
// let i = 11;
// console.log(i) // Identifier 'i' has already been declared 
let i = 10;
const j = 20;
i = 30;
console.log(i);
j = 40;
console.log(j)
</script>
```

+ 什么时候使用const 什么时候使用let

如果确定值不会改变 就使用const 如果确定改变的化就使用let

### 箭头函数 

箭头函数  ES6 允许使用“箭头”（=>）定义函数。箭头函数实际还是函数
箭头函数的写法 
``` html
<script>
var f = v => v;

// 等同于
var f = function (v) {
    return v;
};
</script>
```
1. 不带参数的写法
```html
<script>
  var f = (a) =>  a 
</script>
```
2. 带一个参数的写法
```html
<script>
  var f = a => a
</script>
```
3. 带多个参数的写法 
```html
<script>
  var f = (a,b) => a+b
</script>
```
4. return 多行写法 
```html
<script>
var f = (a,b) => {
    return a+b;
}
</script>

```
5. 箭头函数的this指向 settimeout会改变this的指向 如果我们用箭头函数 箭头函数就指向父级。
在setInterval和setTimeout中传入函数时，函数中的this会指向window对象。
```html
<script>
var obj = {
    num : 1,
    add:function(){
        setTimeout(() => {
            console.log(this);
        },300)
    }
};
obj.add();
</script>

```
### 函数默认值
在ES6之前，不能直接为函数的参数指定默认值，只能采取变通的方法。
```html
<script>
function log(x,y){
    y = y||'world';
    console.log(x,y);
}
log('hello');//hello world

// es6 写法
function log(x ,y="world"){
    console.log(x,y);
}
log('hello');//hello  world
</script>
```

### 字符串模板 

字符串拼接是开发时一个必不可少的环节，也是很恶心的一个环节，尤其是又臭又长的html字符串拼接。

为什么说html字符串拼接很恶心呢，主要有以下几点：

1. 传统的字符串拼接不能正常换行
2. 传统的字符串拼接不能友好的插入变量 ${}
3. 传统的字符串拼接不能友好的处理单引号、双引号互相嵌套的问题。
es6的模板字符串解决了以上问题

+ 拼接字符串

```html
<script>
    // 以前拼接字符串
    var html = '<ul>'+
        '<li cla="aaa">'+1+'</li>'+
        '<li>2</li>'+
    '</ul>'
    // 现在拼接字符串
    // esc 下面的一个键
    ``
    var html = `<ul>
        <li>1</li>
        <li>2</li>
    </ul>`
</script>
```
+ 插入变量

```html
<script>
    var s1 = `hello vue`;
    var html = `xxx ${s1} xxx` 
    console.log(html) //xxx hello vue xxx
</script>
```

### 变量解构赋值
可以理解为变量的取出
+ 数组的解构赋值

ES6 允许按照一定模式，从数组和对象中提取值，对变量进行赋值，这被称为解构

```html
<script>
    var arr = [1,2,3];
    //var a = arr[0],b = arr[1], c = arr[2];
    [a,b,c] = arr;
    console.log(a,b,c)
</script>
```
上面代码表示，可以从数组中提取值，`按照对应位置`，对变量赋值。
本质上，这种写法属于“模式匹配”，只要等号两边的模式相同，左边的变量就会被赋予对应的值。
如果解构失败，变量的值等于undefined。
```html
<script>
let [foo, [[bar], baz]] = [1, [[2], 3]];
foo // 1
bar // 2
baz // 3

let [ , , third] = ["foo", "bar", "baz"];
third // "baz"

let [x, , y] = [1, 2, 3];
x // 1
y // 3

let [x, y, z] = ['a'];
x // a
y // undefined
z // undefined
</script>
```

+ 对象的解构赋值
解构不仅可以用于数组，还可以用于对象。对象的解构与数组有一个重要的不同。数组的元素是按次序排列的，变量的取值由它的位置决定；而对象的属性没有次序，变量必须与属性同名，才能取到正确的值。如果解构失败，变量的值等于undefined。

```html
<script>
let { bar, foo } = { foo: 'aaa', bar: 'bbb' };
foo // "aaa"
bar // "bbb"

let { baz } = { foo: 'aaa', bar: 'bbb' };
baz // undefined
</script>
```

### 数组的扩展

+ 扩展运算符
扩展运算符（spread）是三个点（...）。它好比 rest 参数的逆运算，将一个数组转为`用逗号分隔的参数序列`。
```html
<script>
console.log(...[1, 2, 3])
// 1 2 3

console.log(1, ...[2, 3, 4], 5)
// 1 2 3 4 5

// 常用场景 合并两个数组
var arr = [1,2],arrs = [3,4];
var newArr = [...arr,...arrs];
console.log(newArr) // [1,2,3,4]
</script>
```

+ Array.from

Array.from方法用于将`类对象`转为真正的数组(类数组对象比如arguments)
类数组对象特点 表现像数组 却没有数组该有的方法 比如push
```html
<script>
    function aa(a,b){
        console.log(arguments) //Arguments(2) [1, 2, callee: ƒ, Symbol(Symbol.iterator): ƒ]
        arguments.push(3);
        console.log(arguments) //arguments.push is not a function
    }
    aa(1,2)
    //  想让类数组对象使用数组该有的方法 Array.from转换
     function aa(a,b){
        console.log(arguments) //Arguments(2) [1, 2, callee: ƒ, Symbol(Symbol.iterator): ƒ]
        var arr = Array.from(arguments)
        arr.push(3);
        console.log(arr) //arguments.push is not a function
    }
    aa(1,2)
</script>
```

+ find/findIndex
  - find 
  数组实例的find方法，用于找出`第一个符合条件的数组成员`。它的参数是一个回调函数，所有数组成员依次执行该回调函数，直到找出`第一个返回值为true`的成员，然后返回该成员。`如果没有符合条件的成员，则返回undefined`。
  find方法的回调函数可以接受三个参数，依次为当前的值、当前的位置和原数组。
  ```html
  <script>
      var ele = [1, 5, 10, 15].find(function(value, index, arr) {
        return value > 9;
      }) 
      console.log(ele) // 10
  </script>
  ```
  - findIndex 
  数组实例的findIndex方法的用法与find方法非常类似，返回第一个符合条件的数组成员的下标，如果所有成员都不符合条件，则返回-1。
  ```html
  <script>
      [1, 5, 10, 15].findIndex(function(value, index, arr) {
        return value > 9;
      }) // 2
  </script>
  ```

### Set 和 Map 数据结构

+ Set
ES6 提供了新的数据结构 Set。它类似于数组，但是成员的值都是唯一的，没有重复的值。
Set 本身是一个构造函数，用来生成 Set 数据结构。

```html
<script>
var s = new Set();
[2, 3, 5, 4, 5, 2, 2].forEach(x => s.push(x));
console.log(s)
// [2 3 5 4]
</script>
```
上面代码通过add方法向 Set 结构加入成员，结果表明 Set 结构不会添加重复的值。
  
  - size属性
  `Set.prototype.size`：返回Set实例的成员总数。array.length
  - size 方法
  `Set.prototype.add(value)`：添加某个值，返回 Set 结构本身。
  `Set.prototype.delete(value)`：删除某个值，返回一个布尔值，表示删除是否成功。 // 删除成功 返回true 否则 false
  `Set.prototype.has(value)`：返回一个布尔值，表示该值是否为Set的成员。
  `Set.prototype.clear()`：清除 清空set数据结构

```html
<script>
    var s = new Set([1,23,4]);
    s.add(5); // Set(4) {1, 23, 4, 5}
    console.log(s.size) // 4 
    s.delete(1) //
    console.log(s) // Set(3) {23, 4, 5}
    var sets = s.has(23) // 
    console.log(sets) // true
    s.clear() ;
    console.log(s) //Set(0)
</script>
```
   - Set实现数组去重 
```html
<script>
const items = new Set([1, 2, 3, 4, 5]);
const array = Array.from(items);
</script>
``` 

+ Map

ES6 提供了 Map 数据结构。它类似于对象，也是键值对的集合，但是“键”的范围不限于字符串，各种类型的值（包括对象）都可以当作键。也就是说，Object 结构提供了“字符串—值”的对应，Map 结构提供了“值—值”的对应，是一种更完善的 Hash 结构实现。如果你需要“键值对”的数据结构，Map 比 Object 更合适。

```html
<script>
const m = new Map();
const o = {p: 'Hello World'};

m.set(o, 'content')
m.get(o) // "content"

m.has(o) // true
m.delete(o) // true
m.has(o) // false
</script>
```
Map实例的属性和操作方法 
+ size 属性
size属性返回 Map 结构的成员总数。
+ Map.prototype.set(key, value) 
set方法设置键名key对应的键值为value，然后返回整个 Map 结构。如果key已经有值，则键值会被更新，否则就新生成该键。
```html
<script>
    var map = new Map();
    map.set("aa","100");
    console.log(map) // Map(1) {"aa" => "100"}
</script>
```
+ Map.prototype.get(key)
get方法读取key对应的键值，如果找不到key，返回undefined。
```html
<script>
    var map = new Map();
    map.set("aa","100");
    console.log(map.get("aa")) // 100
</script>
```

+ Map.prototype.has(key)
has方法返回一个布尔值，表示某个键是否在当前 Map 对象之中。
```html
<script>
    var map = new Map();
    map.set("aa","100");
    console.log(map.has("aa")) // true
</script>
```

+ Map.prototype.delete(key)
delete方法删除某个键，返回true。如果删除失败，返回false。
```html
<script>
    var map = new Map();
    map.set("aa","100");
    console.log(map.delete("aa")) // true
</script>
```

+ Map.prototype.clear() 
clear方法清除所有成员，没有返回值。
```html
<script>
    var map = new Map();
    map.set("aa","100");
    map.clear()
    console.log(map) // Map(0) {}
</script>
```

### Promise 

Promise 是异步编程的一种解决方案，比传统的解决方案——回调函数和事件——更合理和更强大。它由社区最早提出和实现，ES6 将其写进了语言标准，统一了用法，原生提供了Promise对象。

所谓Promise，简单说就是一个容器，里面保存着某个未来才会结束的事件（通常是一个异步操作）的结果。从语法上说，Promise 是一个对象，从它可以获取异步操作的消息。Promise 提供统一的 API，各种异步操作都可以用同样的方法进行处理。


```html
<script>
    var p = new Promise(function(resolve , reject){
    setTimeout(() => {
        var num = Math.random()*10;
        if(num>6){
        resolve(num)
        }else{
        reject("小于6")
        }
    }, 1000);
    
    })
    p.then(function(val){
    console.log(val)
    }).catch(function(val){
    console.log(val)
    })
</script>
```
Promise构造函数接受一个函数作为参数，该函数的两个参数分别是resolve和reject。它们是两个函数，由 JavaScript 引擎提供，不用自己部署。

resolve函数的作用是，将Promise对象的状态从“未完成”变为“成功”（即从 pending 变为 resolved），在异步操作成功时调用，并将异步操作的结果，作为参数传递出去；reject函数的作用是，将Promise对象的状态从“未完成”变为“失败”（即从 pending 变为 rejected），在异步操作失败时调用，并将异步操作报出的错误，作为参数传递出去。

Promise实例生成以后，可以用then方法分别指定resolved状态和rejected状态的回调函数。

Promise最大的好处是在异步执行的流程中，把执行代码和处理结果的代码清晰地分离了

```html
<script>
    function ajax(method, url, data) {
        var request = new XMLHttpRequest();
        
        return new Promise(function (resolve, reject) {
            // 当服务器响应已做好被处理的准备时所执行的任务
            request.onreadystatechange = function () {
                    // 存有 XMLHttpRequest 的状态。从 0 到 4 发生变化。
                    // 0: 请求未初始化
                    // 1: 服务器连接已建立
                    // 2: 请求已接收
                    // 3: 请求处理中
                    // 4: 请求已完成，且响应已就绪
                if (request.readyState === 4) {
                     // 返回服务器状态码
                    if (request.status === 200) {
                        resolve(request.responseText);
                    } else {
                        reject(request.status);
                    }
                }
            };
            request.open(method, url);
            request.send(data);
        });
    }
    var p = ajax('GET', 'http://59.110.138.169/api/douban/movie/in_theaters');
   
</script>
```
```html
<script>
    
   
</script>
```
### 常用的数组的操作 map、filter、foreach、some、every、includs、find、findIndex 、reduce

+ map() JavaScript 数组map()方法主要创建一个新的数组使用调用此数组中的每个元素上所提供的函数的结果。即对数组中的每一项运行给定函数，返回每次函数调用的结果组成的数组。对数据进行操作 返回新的数据
```html
<script>
var list = [1,2,3,4];
var newList = list.map(ele =>{
    return ele*2
});
console.log(list,newList) // [1,2,3,4] [2,4,6,8]
</script>

```

+ forEach  方法对数组的每个元素执行一次提供的函数。
foreach 相当于for循环 对数据进行便利
foreach第一个特点 不能对每一项进行更改
第二个特点  不能终止  
```html
<script>
var array1 = ['a', 'b', 'c'];

array1.forEach(function(element) {
  console.log(element);
});

//  "a"
//  "b"
//  "c"
</script>
```
+ filter  方法创建一个新的数组，新数组中的元素是通过`检查指定数组中符合条件的所有元素`。
```html
<script>
var list = [1,2,3,4];
var newList = list.filter(ele => ele > 2);
console.log(list,newList) // [1,2,3,4] [3,4]
</script>
```
+ every()与some()方法都是JS中数组的迭代方法。

every()是对数组中每一项运行给定函数，如果该函数对每一项返回true,则返回true。


some()是对数组中每一项运行给定函数，如果该函数对任一项返回true，则返回true。
```html
<script>
var arr = [ 1, 2, 3, 4, 5, 6 ]; 
 
console.log( arr.some( function( item, index, array ){ 
    return item > 3; 
}));   // true 

console.log( arr.every( function( item, index, array ){ 
    return item > 3; 
}));  // false
</script>

```
   
+ includes 方法用来判断一个数组是否包含一个指定的值，如果是返回 true，否则false。
```html
<script>
[1, 2, 3].includes(2);     // true
[1, 2, 3].includes(4);     // false
[1, 2, 3].includes(3, 3);  // false
[1, 2, 3].includes(3, -1); // true
[1, 2, NaN].includes(NaN); // true
</script>
```
+ find和findIndex find()函数用来查找目标元素，找到就返回该元素，找不到返回undefined，而findIndex()函数也是查找目标元素，找到就返回元素的位置，找不到就返回-1。
```html
<script>
var stu =[
    {
        "name": "张三",
        "gender": "男",
        "age": 20
    },
    {
        "name": "王小毛",
        "gender": "男",
        "age": 20
    },
    {
        "name": "李四",
        "gender": "男",
        "age": 20
    }
]
var item = stu.find((element) => (element.name == '李四'))  // 返回的是{name: "李四", gender: "男", age: 20}
var index = stu.findIndex((element)=>(element.name =='李四'))  // 返回的是索引下标：2
console.log(item , index)
</script>

```
+ reduce 
reduce() 方法接收一个函数作为累加器，数组中的每个值（从左到右）开始缩减，最终计算为一个值。
常用用途用作求和
  - total不带初始值的写法
```html
<script>
 var arr = [1,2,3,4]; 
 //current  当前的元素 total 总和
 var totals = arr.reduce((total,current)=>{
     console.log("total=>",total,"current=>",current,)
     return total = total + current
 })
 console.log(totals)
</script>
```
  - total带初始值的写法
```html
<script>
var totals = arr.reduce((total,current)=>{
    console.log("total=>",total,"current=>",current,)
    return total = total + current
},0)
</script>
```