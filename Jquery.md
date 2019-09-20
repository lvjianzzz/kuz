## 命名规范
1.下划线,字母,,数字 2.但是不能以数字作为开头 jquery的两个变量:
,数字2.但是不能以数字作为开头*jquery*的两个变量: 和 jquery
注意:不能再使用这两个变量 方式引起冲突,什么时候使用jquery?当有其他框架中使用$造成冲突的时候使用jquery
## jquery基本选择器
| 选择器   | 符号   | 说明   | 用法   | 
|:----|:----|:----|:----|
| id选择器   | $('#demo')   | 选择id为demo的第一个元素   | $('#demo').css('color','red')   | 
| 类选择器   | $('.d1')   | 选择所有类名为d1的元素   | $('.d1).css()   | 
| 标签选择器   | $('div')   | 选择所有div标签元素   | $('div').css()   | 
| 全选择器   | $('*')   | 选择所有元素   | $('*').css()   | 
| 交集选择器   | $('.div.active')   | 选择div和active的元素   | $('.div.active').css()   | 
| 后代选择器   | $('.demo .li')   | 选择demo的后代li   | $('.demo .li').css()   | 
| 子代选择器   | $('.ul>.li')   | 选择所有的子代元素   | $('.ul>.li').css()   | 
| 兄弟选择器   | $('.li3+li')   | li3的下一个兄弟元素   | $('.li3+li').css()   | 
| 兄弟选择器   | $('.li3~li')   | li3后面的li兄弟元素   | $('.li3~li').css()   | 

## 过滤选择器
| 符号   | 说明   | 用法   | 
|:----|:----|:----|
| :eq(index)   | 选择序号为index的元素   | $('li:eq(1)').css()   | 
| :gt(index)   | 选择序号> index的元素   | $('li:gt(2)').css()   | 
| :lt(index)   | 选择序号< index的元素   | $('li:lt(2)').css()   | 
| :odd(index)   | 选择所有序号为奇数元素   | $('li:odd').css()   | 
| :even(index)   | 选择所有序号为偶数元素   | $('li:even').css()   | 
| :first   | 选择匹配第一个元素   | $('li:first').css()   | 
| :last   | 选择匹配最后一个元素   | $('li:last').css()   | 

### 属性选择器
| 符号   | 说明   | 用法   | 
|:----|:----|:----|
| $('a[title]')   | 包含title属性的元素   | $('a[title]').css()   | 
| $('a[title="你好"]')   | title属性为你好   | $('a[title="你好"]')   | 
| $('a[title!="你好"]')   | 有title属性,但title属性不=你好   | $('a[title!="你好"]')   | 
| $('a[title$="院"]')   | title属性以 院 结尾的   | ('a[title(′*a*[*title*="院"]')   | 
| $('a[title*="学"]')   | title属性包含学这个字   | $('a[title*="学"]')   | 
| $('a[href][title="你好"]')   | 既包含href又包含title=你好   | $('a[href][title="你好"]')   | 

### 筛选选择器
| 符号   | 说明   | 用法   | 
|:----|:----|:----|
| find()   | 查找box后代的所有p1元素   | $('.box').find('.p1').css()   | 
| children()   | 所有子元素(儿子元素)   | $('.box').children().css()   | 
| sibling()   | 所有兄弟元素(不包括自己)   | $('.li3').sibling().css()   | 
| parent()   | 父元素   | $('.d2').parent().css()   | 
| eq(index)   | 查找指定元素的第index个元素,索引   | $('li').eq(3).css()   | 

## DOM对象和jquery对象相互转换
1.jquery对象转换为DOM对象
1. $('.box')[0];
2. $('.box').get[0];

2.DOM对象转换为jquery对象
1. $(document) --> 把DOM对象转成了jquery对象

var btn = docuemnt.getElementById('btn');
btn --> $(btn);

# DOM 操作
## 1.样式操作
```
获取对应的属性值 : console.log($('.box').css('color'));
设置单个css样式 : $('.box').css('color','red')
设置多个属性样式 : $('.box').css({                 
                  backgroundColor: 'blue',
                  height: '30px'
                  }) 
```
## 2. 属性操作 attr()
```
获取属性 : console.log($('.box').attr('title'))
设置属性 : $('.box').attr('title','d1')
删除属性 : $('.box').removeAttr('title')
```

## 3. 内容操作
```
添加标签 : $('.box').html('<p>我是盒子</p>')
添加内容 : innerText : $('.box').text('我是盒子')
操作表格值 : value: $('input').val('张三')  
```
## 4.操作类名
* addClass() 向被选元素添加一个或多个类名
* removeClass() 从被选元素删除一个或多个类名
* toggleClass() 对被选元素进行添加/删除类名的切换操作
* hasClass() 判断是否存在类名
## 5.DOM查找
* sibling() 除了自己以外的所有的兄弟节点
* next() 下一个兄弟
  * nextAll() 后面所有的兄弟
  * nextUntil() 后面所有的兄弟直到...
* prev() 前面的兄弟
  * prevAll 前面所有的兄弟
  * prev
* parent() 元素的父节点
  * parents() 所有的父节点
  * parenntUntil() 所有的父节点直到...
# Jquery动画
## 隐藏显示动画
### 1. show 方法 : 让匹配的元素展示出来
* $(xx).show(400,function(){});
  * 第一个参数 : 动画持续时间 slow:600ms, normal: 400ms, fast: 200ms
  * 第二个参数 : 回调函数,动画执行结束后 做什么 (选填)
### 2. hide 方法
* $(xx).hide(400,function(){});
### 3. 滑入滑出动画
* 滑入(显示): $(xx).slideDown('slow',callback);
  * 注意: 省略参数或者传入不合法的字符串,那么使用默认值:400ms(同样适用fadeIn/slideDown/slideUp)
* 滑出(隐藏): $(xx).slideUp('slow',callback);
* 滑入滑出切换动画效果 : $(xx).slideToggle('slow',callback)
### 4. 淡入淡出动画
* 淡入动画效果 : $(xx).fadeIn('slow',callback);
* 淡出动画效果 : $(xx).fadeOut('slow',callback);
* 淡入但称呼切换动画效果 : $(xx).fadeTogglee('fast',function(){});
* 淡入改变透明度到某个值 : $(xx).fadeTo(1000,.5); 0全透,1全不透
### 5. 自定义动画
* 语法: $(xx).animate(styles,speed,easing,callback)
  * 第一个参数表示: 要执行动画的css属性(必选)
  * 第二个参数表示: 执行动画时长(可选)
  * 第三个参数表示: 动画执行完后立即执行的回调函数(可选)
```
$(xx).animate({
    width:200,
    color:200, 
    backgroundColor 需要安装插件
},2000,function(){})
```
### 6. 停止动画
* stop() 停止当前正在执行的动画
* stop(stopAll,goToEnd)
  * stopAll 是否全部停止,默认false 停止队列中所有的动画
  * goToEnd 是否将停止的动画 停止在当前动画的最后一个状态
# jquery节点操作
## 1. 创建节点
var node = $('.box').html('<li\>我是<\/li>');
## 2. 插入节点
* append($node或者标签字符串) 注意:剪切效果
  * 作用:在被选元素内部的最后一个子元素(或内容)后面插入内容(存在或者创建出来的元素都可以)
  * 如果是给多个目标追加元素,那么方法的内部会复制多份这个元素,然后追加到多个目标里面去
* appendTo()
  * 作用: 把$(selector)追加到node中去
  * $(selector).appendTo(node);
* prepend()
  * 作用: 在元素的第一个子元素前面追加内容或节点
  * $(selector).prepend(node)
* after()
  * 作用: 在被选元素(之后),作为兄弟元素插入内容或节点
  * $(selector).after(node)
* before()
  * 作用: 在被选元素(之前),作为兄弟元素插入内容或节点
  * $(selector).before(node)
## 3. 删除节点
* $(selector).remove(); 会把对象也干掉 (重要)
* $(selector).empty(); 被选节点里面的内容
* $(selector).html('');
## 4. 复制节点
* $(selector).clone(); jq对象
# 表单 prop()
1. $(input).prop('checked') 获取单选框或者多选框的 状态
* $(input).prop('checked',true) 如果是true 返回有这个属性 否则反之
# 尺寸位置操作(bom)
## 1. 高度和宽度操作
>height() 和 width()
>被选元素的高度 和 宽度 num 类型
>可以获取 也可以设置
```
console.log($('.box').width())
$('.btn1').click(function(){
    $('.box').width(500);
    $('.box').height(200);
})
```
## 2. 坐标值操作
>offset()
>作用: 获取或设置元素相对于文档的位置
>对象 可以获取left 和 top 属性
>num 类型 (设置获取)
```
console.log('offset.left',$('.box').fooset());
$('.btn2').click(function(){
    <!-- 设置相对于文档的位置 -->
    $('.box').offset({
        left: 300,
        top: 100
    })
})
```
## 3. 获取相对于其最近的具有定位的父元素的位置
>position()
>注意 只能获取 不能设置
>console.log($('.inner-box').position());
## 4. 获取或者设置元素垂直方向滚动的位置
>scrollTop()
>网页被卷进去的高度
```
$('.btn4').click(function(){
    <!-- 打印相对于网页垂直方向滚动的距离 -->
    console.log($(document.documentElement).scrollTop());
})
$('.top').click(function(){
    $(document.documentElement).animate({
        <!-- 设置卷进去的高度为0 回到顶部 -->
        scrollTop: 0
    },400)
})
```
# jquery事件机制
## 1.jquery事件的绑定
>on方式(兼容zepto(移动端类似jquery的一个库),建议使用)
>jquery1.7版本后,jquery用on统一了所有的事件处理的方法 给匹配的元素绑定事件
* $(selector).on('click',function(){事件处理程序})
## 2.事件解绑
* off解绑on方式绑定的事件
  * $(selector).off() 取消所有事件
  * $(selector).off('click') 取消指定事件
## 3.事件委托
```
$('.btn').click(function(){
    $('.box').append('<p>不凡学院</p>');
})
<!-- 想实现后来添加的元素也具备点击事件
事件委托 -->
$('.box').on('click','p',function(){
    console.log('天气很好')
})
```
## 4.事件对象
| event.data   | 传递给事件处理程序的额外数据   | 
|:----|:----|
| event.currentTarget   | 等同与this,当前DOM对象   | 
| 内容   | 内容   | 
| event.target   | 触发事件源,不一定===this   | 
| event.pageX   | 鼠标相对于文档左部边缘的位置   | 
| event.type   | 事件类型:click,dbclick   | 
| event.keyCode   | 键盘按键代码   | 
| event.stopPropagation()   | 阻止事件冒泡   | 
| event.preventDefault()   | 阻止默认事件   | 


## 5.事件触发
* $(selector).click() 触发click事件
* $(selector).trigger('click') 方法触发指定事件 (一般不用)
* $(selector).triggerHandler('click') 方法触发被选元素指定事件类型
## jquery 补充
## #1.链式编程
>链式编程原理: return this; 调用任何一个方法都是返回了对象本身
>通常情况下,只有设置操作才能把链式编程延续下去.因为获取操作的时候,会返回获取到的相应的值,无法返回this

$(this).css('width','20px').attr('class','title').css('color','red');
    `end()` 结束当前链最近的一次过滤操作,并且返回匹配元素之前的状态
### 2.隐式迭代
隐式迭代的意思是: 在方法的内部会为匹配到的所有元素进行循环遍历,执行相应的方法:而不用我们再进行循环,简化操作,方便调用
通过$(this).html() 吐过获取的是多元素的值,大部分情况下返回的是第一个元素的值
### 3.each方法
```
$('li').each(function(index,ele){
    <!-- ele 正在遍历的元素 dom对象 -->
    <!-- index 当前遍历的元素 的下标 -->
    if(index >= 3){
        ele.onclick = function(){
            console.log($(this).ttext());
        }
    }
})
        <!-- 大部分情况下是不需要使用each的,因为jquery隐式迭代特性,
        如果要对每个元素做不同的狐狸,这时候就用到了each方法 -->
```
### 多库共存
$.noConflict();让jQuery释放对的控制权,让其他库能够使用
的控制权,让其他库能够使用符号,达到多库共存的目的
此后只能使用jquery来调用jquery提供的方法
### 任何一种jq插件的使用过程
1. 下载插件库
2. 在页面引入插件的css或者字体图片等（如果有的话）
3. 在页面引入jQuery.js
4. 在页面引入插件的js文件（core）
5. 在页面通过插件的api初始化插件 即可使用（通过查看相应的API）
`常用的插件 : 日历-- 滚动-- 表格-- 报表echar-- 树行-- 富文本--
swiper插件

