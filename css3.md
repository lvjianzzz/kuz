# CSS3
+ CSS3选择器
    + 属性选择器（自定义属性也适用）
        + `标签名[属性名]`
        获取该标签具有此属性的元素
        + `标签名[属性名=属性值]`
        获取该标签具有此属性且为此属性值的元素
        + `标签名[属性名*=str]`
        获取该标签具有此属性且属性值任意位置存在str字符的元素
        + '标签名[属性名^=str]'
        获取该标签具有此属性且属性值开始位置存在str字符的元素
        + '标签名[属性名$=str]'
        获取该标签具有此属性且属性值结束位置存在str字符的元素
    + 伪类选择器（n必须写在前面）
        + E：frst-child
        E的父元素的第一个子元素
        + E：last-child
        E的父元素的最后一个子元素
        + E:nth-child(n)
        E的父元素第n个子元素
        + E：nth-child(n)
        E的父元素从后往前数第n个子元素
        + E:nth-child(n + 5)
        E的父元素5以后的子元素
        + li:nth-child(-n + 3)
        E的父元素前三个子元素
        + li:nth-last-child(-n + 3)
        E的父元素前三个子元素
        + li:nth-last-child(7n)
        E的父元素第7的倍数个子元素
        + li:nth-last-child(2n - 1/odd)
        奇数
        + li:nth-last-child(2n/even)
        偶数
    + 目标伪类
        ```
        li:target {
			font-size: 56px;
		}
        
        <a href="#li3">锚点</a>
        <ul>
            <li id="li3" contentEditable>li_3</li>
        </ul>
        
        ```
    + 伪元素
        +  E::before E::afte
        默认为行内元素  content：""必须写
        + E::first-letter
        文本的第一个字母或字
        + E::first-line
         文本第一行
        + E::selection
         可以用来修改文本选中后的样式
+ 颜色
    + rgba() 即Red Green Blue Alpha Alpha
    取值范围为0-255，透明度取值为0-1
    + hsla() 
    H(Hue) 色调 取值范围为0-360 360表示红色 120表示绿色 240表示蓝色
    S(Saturation) 饱和度 取值范围0%-100% 
    L(Lightness) 亮度 取值范围0%-100%
    A(Alpha) 透明度 取值范围0-1
    + #00000000
    十六进制表示颜色,这种也能表明透明度,在6位数的颜色值 后 加两位表示透明度
+ 透明度
    + rgba() hsla()
    不会影响子元素
    + opcity
    会影响子元素 用于单个元素
    + transparent
    不可调节透明度，始终完全透明
    三角形制作
    ```
    border: 20px solid blue;
    border-top: 10px solid transparent;
    border-bottom: 10px solid transparent;
    border-left: 20px solid transparent;
    ```
    同时border-radius
    可以通过两条边框控制一个顶角
    border-top-left-radius
    
+ 阴影
    + 文本阴影
    text-shadow: h-shadow(x) v-shadow(y) blur(模糊半径) color(颜色)
	水平偏移量 正值向右 负值向左
	垂直偏移量 正值向下 负值向上
	模糊半径是不能为负值
	可以有多个影子，用逗号隔开 
    + 盒子阴影
    box-shadow: h-shadow(x) v-shadow(y) blur(模糊半径) spread(扩展范围) color(颜色) inset(是否内嵌,可省略)
+ 盒子模型
    + box-sizing：content-box
    对象的实际宽度等于设置的width值和border、padding之和
    + box-sizing：border-box
    对象的实际宽度就等于设置的width值，即使定义有border和padding也不会改变对象的实际宽度
+ 补充前缀
    + Trident内核: 主要代表为 IE 浏览器  前缀为-ms
    + Gecko内核：主要代表为 Firefox 	前缀为-moz
    + Presto内核：主要代表为 Opera       前缀为-o
    + Webkit内核：产要代表为 Chrome 和 Safari  前缀为-webkit
+ 边框图片
	border-image 属性是一个简写属性，用于设置以下属性：
    + border-image-source：url()
    边框图片引入
    + border-image-slice
    图片边框向内偏移量 不写单位,默认像素,也可以是百分比
    + border-image-width 
    边框宽度
    + border-image-outset：xxpx
     边框图像区域超出边框的量
    + border-image-repeat
    图像边框是否应平铺(repeated)、铺满(rounded)或拉伸(stretched 默认) 可以写2个值,一个代表水平方向,一个代表垂直方向t
+ 渐变
    + 线性渐变（沿着某条直线朝一个方向产生渐变效果）
    `background: linear-gradient(direction, color-stop1, color-stop2, ...);`
    direction: 方向 可以是 角度(10deg)顺时针  也可以是 to top/left/right/bottom
    颜色后面可以跟百分比,表示从百分几开始渐变
    渐变的兼容写法 方向是相反的  而且不带to:
    `background: -webkit-linear-gradient(right ,red 60%,orange 80%);`
    重复渐变
    ` background: repeating-linear-gradient(to right,red 0, red 10%, purple 10%, purple 20%)`
    + 径向渐变
    `background: radial-gradient((shape? size? (at position?))?, start-color, ..., last-color)/？表示可以省略`
    shape 渐变形状 : circle | ellipse(椭圆)
    size 渐变大小 ：
        closest-side（指定径向渐变的半径长度为从圆心到离圆心最近的边）
        closest-corner （指定径向渐变的半径长度为从圆心到离圆心最近的角）
        farthest-side（指定径向渐变的半径长度为从圆心到离圆心最远的边）
        farthest-corner（指定径向渐变的半径长度为从圆心到离圆心最远的角）
        也可指定大小: 需要注意的是 若渐变形状为圆形，则该渐变大小只能设置一个数且不能为百分数，而椭圆既可以为具体数值也可以为百分数
        只传一个值默认形状为圆形,传入的是半径大小,不能为百分比
        传两个值则代表形状为椭圆形,第一个是x轴半径,第二个是y轴半径
    at position 圆心位置
+ 图片加强
    + background-size 设置背景图片的尺寸
     cover 会自动调整缩放比例，保证图片始终填充满背景区域，如有溢出部分则会被隐藏
     contain 会自动调整缩放比例，保证图片始终完整显示在背景区域
    + background-origin (原点，起点)设置背景定位的原点
    border-box 以边框做为参考原点；
    padding-box 以内边距做为参考原点； 默认值
    content-box 以内容区做为参考点
    + background-clip 设置背景区域clip(裁切)
    border-box 裁切边框以内为背景区域； 默认值
    padding-box 裁切内边距以内为背景区域；
    content-box 裁切内容区做为背景区域；
    text 实验属性,文本裁剪,给文字增加背景图片,显示需要文字颜色为透明
+ 过渡
    transition: transition-property transition-duration transition-timing-function transition-delay；
    + transition-property 规定应用过渡的 CSS 属性的名称 (一般都写 all)
    + transition-duration 定义过渡效果花费的时间。默认是 0
    + transition-timing-function: 规定过渡效果的时间曲线。默认是 "ease"
    linear|ease|ease-in|ease-out|ease-in-out|cubic-bezier(n,n,n,n)（贝塞尔曲线）
    + transition-delay 规定过渡效果何时开始。默认是 0
+ 2D转换
    transform:
    +  scale(x, y) 缩放 可以对元素进行水平和垂直方向的缩放，x、y的取值可为小数，不可为负值
    + translate(x, y) 移动 可以改变元素的位置，x、y可为负值
    + rotate(deg) 旋转 可以对元素进行旋转，正值为顺时针，负值为逆时针
    + skew(x-angle,y-angle) 倾斜 定义沿着 X 和 Y 轴的 2D 倾斜转换
    skewX(x-angle) 	定义沿着 X 轴的 2D 倾斜转换
    skewY(y-angle)	定义沿着 Y 轴的 2D 倾斜转换
+ 3D转换
    + perspective: 1000px
    设置给父元素，作用给所有3D转换的子元素
    perspective-origin可以指定视角原点
    + transform-style: preserve-3d
    transform属性的一个值 设置以后子元素的3D效果可以呈现
    +  透视会产生近大远小的效果
    + backface-visibility：visible/ hidden
    设置元素背面是否可见
    + rotateX/Y/Z 沿X/Y/Z轴旋转
      translateX/Y/Z 沿X/Y/Z轴移动
+ 动画
    animation: name duration timing-function delay iteration-count direction fill-mode
    name duration 必须写,其余可以都不写
    + Animation-name 动画名称(必填)
    + Animation-duration 动画持续时间(必填)
    + animation-timing-function 运动规律
    linear/ease/ease-in/ease-out/ease-in-out/cubic-bezier(n,n,n,n)：	特定的贝塞尔曲线类型，4个数值需在[0, 1]区间内
    + animation-delay 动画延迟（只是第一次）
    + animation-iteration-count	重复次数	
    infinite 无限次
    + animation-direction 动画是否重置后再开始播放
    alternate 动画直接从上一次停止的位置开始执行，倒着来
    normal 动画第二次直接跳到0%的状态开始执行
    + animation-fill-mode 动画执行完毕后状态
    forwards 当动画完成后，保持最后一个属性值（在最后一个关键帧中定义）
    backwards 在 animation-delay 所指定的一段时间内，在动画显示之前，应用开始属性值（在第一个关键帧中定义）
    both 设置对象状态为动画结束或开始的状态，结束时状态优先
    + animation-play-state	播放状态（ running 播放 和 paused 暂停 ）
+ 动画监听
    + animationstart  动画开始后触发
    + animationiteration  动画重复播放时触发
    + animationend 动画完成后触发
    ```
    // 过渡只有监听结束的方法,  start 和 run 的监听方法在开发状态
    d2.addEventListener('transitionstart',function () {
    	console.log('过渡开始...');
    })
    d2.addEventListener('transitionrun', function() {
    	console.log("过渡执行中");
    });
    d2.addEventListener('transitionend',function () {
    	console.log('过渡结束...');
    ```









