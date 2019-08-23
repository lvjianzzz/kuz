# 数组(Array)
+ 数组的创建
    数组的元素可以是任意的数据类型，也可以是对象，也可以是函数，也可以是数组
    + 字面量定义 `var arr = [1, 2, 3, 4];`
      数组的下标从0开始
    + 对象定义（数组的构造函数）
        `var arr = new Array();`
        如果参数为空，则表示创建一个空数组；参数位置是一个数值时，表示数组长度；参数位置是多个数值时，表示数组中的元素
    + 数组元素
      数组的索引代表的是数组中的元素在数组中的位置，从 0 开始
      可以通过 `数组名[索引值]`来添加和修改元素
    + length 数组的长度(元素个数) `数组长度 = 数组名.length`
    + 修改数组长度 
      `数组名.length = 数组长度(元素个数)`
      - 如果修改的 length 大于原长度，则多出部分会空出来,值为empty
      - 如果修改的 length 小于原长度，则多出的元素会被删除，数组将从后面删除元素
+ 遍历数组元素
    + for循环
    ```
    var arr = [3, 7, 4, 6, 9];
    for (var i = 0; i < arr.length; i++) {  
        console.log(arr[i]);
    }
    ```
    + for in
    ```
    for (var key in arr) {
	    console.log(arr[key]);
    }
    ```
+ 求数组的平均值
    ```
    var arr = [24, 36, 2, 8];
        var sum = 0;
        for (var i = 0; i < arr.length; i++) {
            sum = sum + arr[i];
        }
        var arg = sum / arr.length;
        console.log(arg);
    ```
+ 冒泡排序
    ```
    var arr = [12, 8, 4, 24, 10];
    for (var j = 0; j < arr.length - 1; j++) {
        // 外层循环 控制 轮数
        for (var i = 0; i < arr.length - 1 - j; i++) {
        // 内层循环  负责  找出本轮最大值
        // arr[i] arr[i+1]
            if (arr[i] > arr[i + 1]) {
                // 交换位置  找第三方
                var temp = arr[i];
                arr[i] = arr[i + 1];
                arr[i + 1] = temp;
            }
        }
    }
    console.log(arr);
    ```
+ 阶乘
    ```
    var jc = 1;
    for (var i = 1; i <= 6; i++) {
        jc = jc * i;
    }
    console.log(jc)
    ```
+ 选择排序
    ```
    for (var j = 0; j < arr.length - 1; j++) {
        var minIndex = j;
        for (var i = j + 1; i < arr.length; i++) {
            if (arr[minIndex] > arr[i]) {
                minIndex = i;
            }
        }
            // 交换位置
        var temp = arr[j];
        arr[j] = arr[minIndex];
        arr[minIndex] = temp;
        console.log(arr);
    }
+ 数组的基本方法
    + push() `数组名.push()`
    向数组的最后面插入一个或多个元素，返回结果为该数组新的长度
    + pop()
    删除数组中的最后一个元素，返回结果为被删除的元素
    + unshift()
    在数组最前面插入一个或多个元素，返回结果为该数组新的长度 插入元素后，其他元素的索引会依次调整
    + shift()
    删除数组中的第一个元素，返回结果为被删除的元素
    + cancat() `数组名.concat(数组名)`
    连接两个或多个数组，返回结果为新的数组（不会改变原数组）
    + join()
    将数组转换为字符串，返回结果为转换后的字符串（不会改变原数组）
    + split()
    通过指定分隔符，如果省略，默认以逗号分隔，将字符串分割为字符串数组
+ 数组的高级API
    + reverse()
    反转数组，返回结果为反转后的数组（会改变原来的数组）
    + sort()
        对数组的元素进行从小到大来排序（会改变原来的数组）
        - 无参时
        如果在使用 sort() 方法时不带参，则默认按照Unicode 编码，从小到大进行排序
        因为是使用Unicode 编码进行排序,所以会出现11>1这种情况
        - 带参时
        为了解决如上情况 可以使用如下做法
        ```
        数组名.sort(function (a, b) {
            return a - b; //从小到大
            // 返回值<0 不交换位置
            // 返回值>0  交换位置
            // 返回值==0 不动

            // 从大到小排
            // return b - a;
        })
        ```
    + slice()
    数组中提取指定的一个或者多个元素，返回结果为新的数组（不会改变原来的数组）
    新数组 = 原数组.slice(开始位置的索引, 结束位置的索引);
    包含开始索引，不包含结束索引
    没有指定结束索引 截取到到最后
    + indexof()
    indexOf(value)：从前往后找，获取 value 在数组中的第一个下标
    + lastIndexof()
    astIndexOf(value) ：从后往前找，获取 value 在数组中的最后一个下标
    + splice()
    从数组中删除指定的一个或多个元素，返回结果为新的数组（会改变原来的数组，会将指定元素从原数组中删除）
    新数组 = 原数组.splice(起始索引index, 需要删除的个数,第三个参数, 第四个参数...)
    第三个及之后的参数，表示：向原数组中添加新的元素，这些元素将会自动插入到开始位置索引的前面

     

    