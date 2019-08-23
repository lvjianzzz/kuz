+ Date对象
    + 写法
        1. 当前时间对象 `var date1 = new Date();`
        打印结果为中国标准时间(当前时间)
        2. 在参数中传递一个表示时间的字符串
        `var date2 = new Date("2019/07/22 10:00:00");`
    + 获取当前时间的 年 月 日 时 分 秒 毫秒
        `var date = new Date();`
        1. 年  `var year = date.getFullYear();`
        2. 月  `var month = date.getMonth() + 1;`
        getMonth()的值是0-11,获取月份时需＋1
        3. 日  `var day = date.getDate();`
        4. 时  `var hour = date.getHours();`
        5. 分  `var min = date.getMinutes();`
        6. 秒  `var second = date.getSeconds();`
        7. 毫秒  `var mSecond = date.getMilliseconds();`(1s == 1000ms)
        8. 星期  `var weekDay = date.getDay();`
    + 时间戳
        `var stamp = date.getTime();`
        从格林威治标准时间的1970年1月1日，0时0分0秒到当前日期所花费的毫秒数
+ Math对象
    + Math.ceil() 天花板函数(向上取整);
    + Math.floor() 地板函数(向下取整);
    + Math.max(x,y,z) 取多个数的最大值;
    + Math.min(x,y,z) 取多个数的最小值;
    + Math.pow(x,y) x的y次方;
    + Math.random() 生成0-1之间的随机数 [0,1);
        - 例: 生成一个[1,10]范围的随机数 整数
        `Math.floor(Math.random() * 10) + 1`
    + Math.round() 四舍五入(存在误差);
    + Math.abs() 取绝对值;
    + Math.sqrt() 进行开方;
+ 逻辑运算符
    && 与（且）：两个都为真，结果才为真
    || 或：只要有一个是真，结果就是真
    ! 非：对一个布尔值进行取反
    + 短路运算
        - && 如果第一个值为false,则不会看第二个值;
        - || 如果第一个值为true,则不会看第二个值;
    + 非布尔值得运算
        - 如果对非布尔值进行 非运算， 则会先将其转换为布尔值， 然后再操作
        ```
        var a = 10;
        a = !a;
        console.log(a); // false
        console.log(typeof a); // boolean
        ```
        - 非布尔值进行与或运算时，会先将其转换为布尔值，然后再运算，但返回结果是原值
        ```
        console.log(5 && 6); // 6
        console.log(5 || 6); // 5
        console.log('' || 6); // 6
        ```
+ if语句
    + 条件判断语句
    ```
    if(条件判断){
        符合条件执行
    }
    ```
    + 条件分支语句
    ```
    if(条件判断){
        符合条件执行
    } else {
        不符合条件执行
    }
    ```
    + 多分支条件语句
    ```
    if (条件表达式1) {
	// 条件1为真时，做的事情
    } else if (条件表达式2) {
	// 条件1不满足，条件2满足时，做的事情
    } else if (条件表达式3) {
	// 条件1、2不满足，条件3满足时，做的事情
    } else {
	// 条件1、2、3都不满足时，做的事情
    }
    ```
    + if语句具有跳楼现象
    + if语句可以嵌套
+ 三元运算符
    例  `5 > 3 ? 5 : 3; // 5`
+ switch语句
    依次比较，一旦有对应的值，就会执行相应的语句，在执行的过程中，遇到 break 就会结束(break结束switch语句)
    当所有的比较结果都为 false 时，则只执行 default 里的语句
    例:
    ```
    var num = 1;
    switch (num) {
        case 0:
            alert('0');
            break;
        case 1:
            alert('1');
            break;
        default:
            alert('NaN');
            break;
    }
    ```
+ for循环
    例:
    ```
    for (var i = 0; i <= 100; i++) {
        console.log(i);
    }
    console.log(i); //101
    ```
+ while循环
    必要时可以使用break终止循环
    + while
    先判断在执行  列:
    ```
    var num = 10;
    while (num > 0) {
        console.log(num);
        num--;
        if (num === 7) {
            break;
        }
    }
    ```
    + do while
    先执行后判断(保证循环体至少执行一次) 列:
    ```
    var count = 10;
    do {
        console.log(count);
        count--;
    } while (count > 0)
    ```
+ break和continue
    + break 
        终止整个循环语句 列:
        ```
        for (var i = 0; i < 5; i++) {
            if (i === 2) {
                // 停止循环 或者 说 退出循环
                break;
                // 本次循环后边的代码也不会在执行了
            }
            console.log(i); //0 1
        }
        ```
    + continue
        跳出循环(只跳过本次) 例:
        ```
        for (var i = 0; i < 5; i++) {
            if (i === 2) {
                continue;
                // 跳出循环(仅跳过本次)
            }
            console.log(i); //0 1 3 4 
        }
        ```


