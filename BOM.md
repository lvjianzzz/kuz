# BOM
BOM 的核心对象是 window ，它表示浏览器的一个实例。在浏览器中， window 对象有双重角色，它既是通过 javascript 访问浏览器窗口的一个接口，又是 ECMAScript 规定的 Global 对象。所有全局作用域中声明的变量、函数都会变成 window 对象的属性和方法
### 事件对象
+ Event
兼容写法 `event || window.event`
对象代表事件的状态，比如事件在其中发生的元素、键盘按键的状态、鼠标的位置、鼠标按钮的状态
+ event.target / e.currentTarget
event.target的兼容写法`event.target || event.srcElement`
```
<body>
  <ul>
    <li>hello 1</li>
    <li>hello 2</li>
    <li>hello 3</li>
    <li>hello 4</li>
  </ul>
  <script>
    let ul = document.querySelectorAll('ul')[0]
    let aLi = document.querySelectorAll('li')
    ul.onclick = function(e){
       let oLi1 = e.target  
       let oLi2 = e.currentTarget
        console.log(oLi1)   //  被点击的li
        console.log(oLi2)   // ul
        console.og(oLi1===oLi2)  // false
    }
  </script>
</body>
```
e.target指向引发触发事件的元素
e.target指向用户点击的li，由于事件冒泡，li的点击事件冒泡到了ul上，通过给ul添加监听事件而达到了给每一个li添加监听事件的效果
而e.currentTarget指向的是给绑定事件监听的那个对象，即ul
+ 事件委托 
通过监听一个父元素，来给不同的子元素绑定事件，减少监听次数，从而提升速度。
由于事件的冒泡机制,可以使用事件委托的方式给元素添加事件,多用于ul监听事件更改li的情景
+ 阻止冒泡
event.stopPropagation()；
event.cancelBubble = true (IE<=10专用)
兼容写法 `event.stopPropagation?event.stopPropagation():event.cancelBubble = true;`
+ 组织默认事件
兼容写法 `event.preventDefault() || event.returnValue = false`
+ offsetX/Y
表示鼠标指针位置相对于触发事件的对象的位置 = `e.pageX/Y - 绑定事件的元素距离页面的左/上边距(offsetLeft/Top)`
+ e.pageX/Y
获取鼠标点击的相对于页面的位置,算入滚动条的距离
+ e.clientX/Y
获取鼠标点击的相对于可视区域的位置,目前可见区域
+ e.screenX/Y
获取鼠标点击的相对于屏幕的位置,整个屏幕
+ event.type
事件的类型
+ event.key
键盘按键码
+ event.button
鼠标点击的按键(只认识三个键) 可在 onmousedown 事件中测试
=== 0 您点击了鼠标左键
=== 1 您点击了鼠标中键
=== 2 您点击了鼠标右键
### 鼠标事件
+ onmousedown
鼠标按下事件
+ onmouseup
鼠标松开事件
+ onmousemove
鼠标移动事件
+ onmouseover
事件会在鼠标指针移动到指定的元素上时发生
+ onmouseout
在鼠标指针移动到元素外时触发
+ 鼠标拖拽事件时如果在鼠标松开时结束onmousemove事件则可以：
作用范围元素.onmousemove = null
### offset家族
+ offsetWidth offsetHeight(检测盒子自身宽高)
offset宽/高 = 盒子自身的宽/高(width/height) + padding +border
+ offsetLeft offsetTop(检测距离父盒子有定位的左/上面的距离)
如果父级都没有定位则以 body 为准
offsetLeft 从父亲的 padding 开始算,父亲的 border 不算
在父盒子有定位的情况下，offsetLeft == style.left(去掉 px)
+ offsetParent(检测父系盒子中带有定位的父盒子节点)
如果当前元素的父级元素没有进行 CSS 定位(absolute,relative,fixed) offsetParent 为 body
如果当前元素的父级元素中有 CSS 定位 offsetParent 取最近的那个父级元素
+ offsetTop/Left style.top/left 区别
offsetTop/Left 返回的是整数 只读
style.top/left 返回的是字符串，带有单位：px 可读写(但只可获取行内样式)
+ 案列 缓动动画
```
function slowlyMove(ele,target){
	// 防止定时器冲突
	clearInterval(ele.timer);
	// 声明定时器,为了保证定时器的唯一性,绑定在了元素上
	ele.timer = setInterval(function (){
		// 声明起点 获取元素的左边距 style.left 只能获取行内样式
		var start = ele.offsetLeft;
		// 声明步长
		var step = (target - start) / 10;
		// 元素运动 终点跟起点之间的距离会在小于10的时候,每次走1px,可以走到终点
		// step < 1 ===> target - start < 10  有方向问题
		if(Math.abs(step) < 1){	// 判断步长值小于 1  (-1,1)
			// 判断移动方向  加上 判断 步长为 0 的情况 (-1,0] (0,1)
			step = step > 0 ? 1 : Math.floor(step);
		}
		// 运动 运动位置 = 起点 + 步长
		ele.style.left = start + step + "px";
		// 判断停止条件
		if(start + step === target){
			// 关闭定时器
			clearInterval(ele.timer);
			// 给出提示
			console.log("stop ...");
		}
	},17)
}
```
### Scroll家族
+ scrollWidth scrollHeight
(内容未溢出: 内容宽高 + padding) 
(内容溢出时：内容宽/高 + padding
有滚动条时,左右的padding只显示一个
没有滚动条时,padding 只显示 上面的和左面的)
+ scrollTop scrollLeft (可读写)
被浏览器或父类遮挡的上/左部分(获取元素被卷入的上左距离)
目标元素需有滚动条，否则获取值为0
兼容写法`var scrollTop = document.documentElement.scrollTop //火狐 谷歌等浏览器 || window.pageYOffset // Safari浏览器 || document.body.scrollTop //IE678`
`document.documentElement.scrollLeft || window.pageXOffset || document.body.scrollLeft`
+ onscroll事件
当元素的滚动条滚动时触发的事件 设置此事件的元素一定要有滚动条
可以绑定DOM元素、window元素、document元素
`window.onscroll=function(){}` //浏览器滚动条监听
+ window.scroll(x,y)
是让window滚动条滚动到那个x,y坐标 //x是水平坐标，y是垂直坐标
+ window.scrollBy(x,y)
让window滚动条相对滚动到某个坐标
- 10即相对向左/向上滚动10像素
+ window.scrollTo(x,y)
window.scrollTo(x,y)和window.scroll(x,y)一样

### Client家族
+ clientWidth clientHeight
 自身宽高(content) + padding 内容溢出不算
 当有滚动条的时候，不算滚动条的宽度
+ document.documentElement.clientWidth/clientHeight
获取浏览器可视区域的宽高	没有兼容问题
+ window.innerWidth/innerHeight
IE <= 8 不支持	表示获取 window 可视区域的内部大小
+ window.outerWidth/outerHeight
IE <= 8 不支持	表示整个浏览器窗体的大小
+ clientTop clientLeft
只读
表示内容区域的左上角相对于整个元素左上角的位置 实际上就是 border 的宽度
内容区域(内容+padding) padding 之外就剩 border
+ 获取任意元素与页面之间的上左边距
运用递归
```
	function getTop(ele) {
		if (ele.offsetParent.tagName === "BODY") {
			return ele.offsetTop;
		}
		return ele.offsetTop + ele.offsetParent.clientTop + getTop(ele.offsetParent);
	}
```
while循环方法
```
function getElementTop(elem) {
    var elemTop = elem.offsetTop; //获得elem元素距相对定位的父元素的top
    elem = elem.offsetParent; //将elem换成起相对定位的父元素
    while (elem != null) { //只要还有相对定位的父元素 
        //获得父元素 距他父元素的top值,累加到结果中
        elemTop += elem.offsetTop;
        //再次将elem换成他相对定位的父元素上;
        elem = elem.offsetParent;
    }
    return elemTop;
}
```
+ 获取元素的样式
window.getComputedStyle(element, [pseudoElt]).styleName
// 仅用于谷歌和火狐等标准浏览器
pseudoElt 指定一个要匹配的伪元素的字符串 所以普通元素省略（或null）一般都写成 null
 如果要获取伪元素的样式,则写上要获取的伪元素的名字
 element.currentStyle.styleName
 // 仅用于 IE
 兼容写法： 
 ```
 function getStyle(ele,styleName){
	if(ele.currentStyle){
		return ele.currentStyle[styleName];
	}else{
		return window.getComputedStyle(ele,null)[styleName];
	}
}
```






