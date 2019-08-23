# jQuery
+ jquery的引入
使用jquery在引入只有
`<script src="js/jquery-3.4.1.min.js"></script>`
+ 入口函数 
相当于原生js的window.onload
但不会覆盖,可以写多个
而window.onload只可写一个，写多个会被覆盖
同时，window.onload必须等到页面内包括图片的所有元素加载完毕后才能执行
而$(document).ready()是DOM结构绘制完毕后就执行，不必等到加载完毕。只加载了dom框架，对于需要时间的大的图片不等待
```
$(document).ready(funciton(){

}) //方法1 
$(function(){}) //方法2 

```
+ jquery变量
jquery的两个变量:$ jquery
不能再使用这两个变量 防止引起冲突
当有其他框架中使用$造成冲突的时候使用jQuery
jquery内命名变量时
可使用 ： 下划线，字母，$，数字
但不能使数字作为开头
