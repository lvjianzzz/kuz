# 对象
+ 创建对象
    + 使用 new 关键字 构造函数创建对象
    `var obj = new Object();`
    + 使用对象字面量来创建一个对象
    可以直接指定对象中的属性
    ```
    var obj = {
        属性名: 属性值,
        属性名: 属性值
    }
    ```
    + 自定义构造函数 创建对象
        ```
        function Person(name, age) {
            this.name = name;
            this.age = age;
            this.say = function () {
                alert(this.name);
            }
        }
        var zc = new person('李四', 27);
        ```
        + new的作用
            1. 开辟内存空间创建了一个对象{}
            2. 将构造函数中的 this 指向 {}
            3. 执行函数中的代码
            4. 返回 {}
    + this的指向
        1. 以函数的形式调用时，this 永远都是 window 比如fun();相当于window.fun()
        2. 以方法的形式调用时，this 是调用方法的那个对象
        3. 以构造函数的形式调用时，this 是 new 出来的那个对象
    + 对象追加和修改属性和方法 
    `obj.属性名 = 属性值` 
     ```
      obj.属性名 = function () {
          alert('0')
      }
     ```
     + 删除对象的属性
     `delete obj.name;`
+ 对象的遍历
    ```
    for (var key in obj) {
        console.log('属性名' + key + ',属性值' + obj[key]+ '');
    }
    ```
    1. key 是对象的 每一个 属性名
    2. obj.key 你获取的是 obj的 key属性,没有这个属性  它的属性值就是undefined
    3. 对象.xx获取属性时.xx 是个变量 ,需要用这种形式获取 obj[xx]   
+ jason对象
    是一种轻量级的数据交换格式
    JSON 是 JS 对象的字符串表示法，它使用文本表示一个 JS 对象的信息，本质是一个字符串
    ```
    // 普通对象
    var obj = {
        name: '张三',
        age: 24
    }
    // JSON 对象
    var objJson = {
        "name": "李四",
        "age": 36
    }
    ```
    + JSON.stringify(对象名)
    将对象转换为jason字符串
    + JSON.parse(接受jason字符串的变量)
    将jason字符串转换为 jason对象
    只有jason字符串可以转换为jason对象
    + jason可以解决控制台打印复杂数据的问题 例
    ```
    var arr = [3, 4, 5, 6, 7];
    console.log(JSON.stringify(arr)); // 想印的是当前状态
    arr[3] = 200;
    console.log(arr);
    ```
+ 字符串对象的常用方法(可以参照数组高级API内容)
    + charAt(下标(位置)) 
    获取相应位置的字符
    + charCodeAt(下标(位置))
    获取相应位置字符的Unicode编码
    + indexOf('字符')
    返回第一个字符在字符串中的位置,从前往后
    + lastIndexOf('字符')
    返回第一个字符在字符串中的位置,从后往前
    + concat() 
    字符串名.concat(字符串名)
    连接字符串
    + slice()
    提取字符串的某个部分
    `字符串名.slice(2, 9) // 字符串下标为2到下标为9的部分`包含开始索引，不包含结束索引
    + substr
    截取字符串
    `字符串名.substr(2,9) //从下标为2的字符开始截取9个字符
    + toUpperCase()
    将字符串全部变为大写英文
    + toLowerCase()
    将字符串全部变为小写英文


    
    