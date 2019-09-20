# jquery
##  jquery 是原生js的框架
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
jQuery的两个变量   $ 和  jQuery
(当有其他框架中使用$造成影响的时候才使用jQuery)

+ jQuery基本选择器和css是一模一样的 .我们可以调用css的选择器方法到jq里.

+ 层级选择器 
.li2+li{color : red} .下一个兄弟选择器
.wrap>.w{color : red} .子代选择器
.li3~ li {color : red} .li3后面的所有兄弟选择器
+ 过滤选择器
$(' li:eq (4)') .css(backgroundColor ,red) 第5个
$(' li:gt (4)') .css(backgroundColor ,red) 大于第4个坐标
$(' li:lt (4)') .css(backgroundColor ,red) 小于第4个坐标
:odd 奇数    :even偶数
:first 第一个元素    :last 最后的一个元素.

+ 属性选择器
$ ('a [herf]').css ('color','blank') 具有herf属性的标签
$ ('a [title="你好"]').css ('color','blank') 具有title属性并且为你好的属性的标签
^= 以什么开头的 属性标签
$= 以什么结尾的 属性标签
*=f 所有的带有f的 属性标签

##### 关系筛选选择器
| find(selector) | 查找指定元素的所有后代元素|\$(“#j_wrap”).find(“li”).css(“color”, “red”);|
| ---- | ---- |---- |
| children()  |指定元素的直接子元素|$(“#j_wrap”).children(“ul”).css(“color”, “red”);|
| siblings()  |查找所有兄弟元素（不包括自己）|$(“#j_liItem”).siblings().css(“color”, “red”);|
| parent() |查找父元素 |$(“#j_liItem”).parent(“ul”).css(“color”, “red”);

+ eq(index) 查找指定元素的第index个元素
$(“li”).eq(2).css(“color”, “red”);

## jQuery 事件

| \$(document).ready(function) |	将函数绑定到文档的就绪事件（当文档完成加载时）|
| ---- | ---- |
| \$(selector).click(function)|触发或将函数绑定到被选元素的点击事件|
| \$(selector).dblclick(function)|	触发或将函数绑定到被选元素的双击事件|
| \$(selector).focus(function)|	触发或将函数绑定到被选元素的获得焦点事件|
| \$(selector).mouseover(function) |	触发或将函数绑定到被选元素的鼠标悬停事件|
+ DOM对象 转化jq 对象
   var pEl =document.getElementsByTagName('p')//得到dom对象
   var jqpEl =$(pEl);//转化jquery对象
+ Jquery对象转换成DOM对象
   var jqueryObj = $('#objId');　　//得到Jquery对象
   var domObj = jqueryObj[0];　　//通过下标得到DOM对象，jqueryObj[0]等同于jqueryObj.get(0)
#### dom查找(关系选择器)
+ siblings()  除了自己以外的所有的兄弟节点
+ next()	下一个兄弟
+ nextAll()		后面所有的兄弟
+ nextUntil()	后面所有的兄弟直到…
+ prev()	前面的兄弟
+ prevAll()		前面所有的兄弟
+ parent()		上一个兄弟
+ parents()		所有的父节点
+ prevUntil()  
   $("li.start").nextUntil("li.stop").css({"color":"red","border":"2px solid red"}); 查找 "start" 和 "stop" 的两个 \<li> 元素之间的所有同级元素
+ parentsUntil()
#### jQuery动画
+  隐藏和显示动画
   $(xx).show(2000);//隐藏动画
   $(xx).hide(2000); //显示动画
+ 滑入滑出
$(selector).slideUp(speed,callback);//向上滑动  里面的speed 可以修改成毫秒的时间  callback 参数是滑动完成后所执行的函数名称。
$(xx).slideDown()// 向下滑出
$(xx).slideToggle(speed,callback);//滑入滑出
+ 淡入淡出
	$(xx).fadeIn(speed, callback);//淡入
   $(xx).fadeOut(1000);//淡出
   $(xx).fadeToggle('fast',function(){}); //淡入淡出
+ 自定义动画
   $(selector).animate(styles,speed,easing,callback);
   styles  规定产生动画效果的 CSS 样式和值。
   speed 规定动画的速度
   easing 规定在不同的动画点中设置动画速度的 easing 函数
   callback animate 函数执行完之后，要执行的函数。

+ 停止动画
1.stop();
作用:停止当前正在执行的动画
2.stop(stopAll,goToEnd);
stopAll  是否全部停止，默认false 停止队列中所有的动画
goToEnd  是否将停止的动画  停止在当前动画的最后一个状态   
##### jQuery节点
+  创建元素
   var node = $('#box1').html('\<li>我是\</li>');
   添加元素
   在元素的最后一个子元素后面追加元素：
   + append();
   在元素的第一个子元素前面追加内容或节点:
   + prepend();
   把\$(selector)追加到node中
   \$(selector).appendTo(node);
   + after()
   在被选元素之后，作为兄弟元素插入内容或节点
   + before()
   作用：在被选元素之前，作为兄弟元素插入内容或节点
   $(selector).before(node);
+ 清空元素
   $(selector).empty();
   $(selector).html(“”);
   $(selector).remove();  //会把对象也干掉
+ 复制元素
   $(selector).clone();

