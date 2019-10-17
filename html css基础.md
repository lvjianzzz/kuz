#html&css

##html
###基本骨架
1. `<!DOCTYPE html>`以html5的标准解析页面  
2. `<html lang="en"></html>`html标签是网页根节点,一个html标签只有一个html标签;lang="en" 声明语言环境
    1. `<head></head>`
        1. `<meta>`meta标签(包含网站的一些元信息) 
        2. `<title></title>`
    2. `<body></body>`网页主体
###标签
1.`<div></div>` div标签(用做布局)
2.`<span></span>` span标签(用于一些特殊内容)
3. h标签(标题标签)
```
    <h1></h1>(一级标题只有一个)
    <h2></h2>
    <h3></h3>
    <h4></h4>
    <h5></h5>
    <h6></h6> 
```
4. `<p></p>`p标签(段落标签)
5. `<br>`换行
6. `<hr>`分割线
7. `<img src="" alt="">`引入图片,其中:
    1. alt属性:图片加载失败显示内容
    2. src属性:图片引入路径
        1. 绝对路径(网络路径)
        2. 相对路径(参照当前文档所在位置)
            1. 同级目录:直接引入 xx.png
            2. 上级目录:../xx.png
            3. 下级目录:xx(文件名)/xx.png
8. `<a href="" target=""></a>`a标签(超链接标签,点击跳转)
    1. href属性:跳转页面地址
    2. target属性:默认值 target="_self"(当前窗口打开)
                        target="_blank"(在新窗口打开)
                        target="_top"(在顶级窗口打开)
                        target="parent"(在父级窗口打开)
9. 列表
    1. 无序列表
    ``` 
    <ul>
        <li></li>
        <li></li>
    </ul>
    ```
    2. 有序列表
    ```
    <ol>
        <li></li>
        <li></li>
    </ol>
    ```
    3. 自定义列表
    ```
    <dl>
        <dt></dt>
        <dd></dd>
        <dd></dd>
        <dt></dt>
        <dd></dd>
        <dd></dd>
    </dl>
    ```
10. 斜体 
`<em></em>`(语义) `<i></i>`(无语义)
   加粗
`<strong></strong>`(语义) `<b></b>`(无语义)
   下标
`<sub></sub>` 如 分子表达式 H<sub>2</sub>0
   上标
`<sup></sup>` 如 平方 5<sup>2</sup> 
   删除线
`<del></del>`
   下划线
`<ins></ins>`
11. 转义字符
   空格 &nbsp ; &#160
   大于号 &lt ; &#60
   小于号 &gt ; &#62
12. input标签 搜索栏 button标签 搜索按钮   
###标签属性
1. id="" id属性 标签唯一标识 不可重复
2. class="" class属性 类
   title="" 鼠标悬浮时出现内容

##css
+ 书写位置
    + head标签内书写
    - 外部引用 `<link rel="stylesheet" href="xxx.css(同图片引入)">`
    - 内部书写
    ```
    <style>
    选中标签{
        样式名:样式值
    }
    </style>
    ```
    + 行内书写 `<标签 style="样式名:样式值"></标签>`
+ 选择器
    + 标签选择器 标签名{}
    + clss选择器 .类名{}
    + id选择器 #id{}
    + 后代选择器 父级(空格)子级{}
    + 交集选择器 同时具备多个类名 .类名.类名{}   
    + 并集选择器 同时选中多个标签,中间用逗号隔开 标签1,标签2{}
    + 通配符 选中所有标签 *{}
+ 继承性
    + 子类标签会继承父类标签 字体相关样式
    + a标签不会继承父类 字体颜色
+ 权重
    样式冲突时,计算权重
    + 行内样式(1000)>id权重(100)>class选择器(10)>标签选择器(1)>通配符/继承属性(0)
    + 权重相同时 就近原则
    + 复杂选择器权重 简单累加
+ 标签表现形式
    + 块状标签 独占一行，宽高有效 比如： div p h1~h6 form table hr br ul>li ol>li dl>dt/dd
    + 行内块标签 可以同一行显示，宽高有效 比如: input select img button
    + 行内标签 可以同一行显示，但是宽高无效， margin-top/margin-bottom无效 比如： a span strong del ins em i b 等字体标签
+ 样式
    + width 宽
    + height 高
    + background: 颜色 url(背景图片路径) no-repeat(是否平铺) center(背景图片位置) fixed(背景滚动)
    + background-color 背景颜色
        + 预定义颜色(颜色英文名)
        + 十六进制值 如#ffffff
        + rgb(xx,xx,xx)
        + rgba a透明度0-1
    + background-img 背景图片
    + background-repeat 背景图片是否平铺
    + background-position 背景图片位置
        + 水平方向left/rigjt/center
          垂直方向top/bottom/center
        + 像素值 距离左边与上边的距离
    + background-attachment 背景滚动 scroll(默认)/fixed
    + background-size 背景图片大小
    + background-clip: content-box;  使背景只在内容区域出现
    + color 字体颜色
    + font-size 字体大小
    + text-align 对齐方式 left/center/right
    + text-indent 首行缩进
    + font-family 字体
    + font-weight 字体加粗 bolder/lighter/normal
    + line-height 行高 line-height=height时字体上下居中
    + text-decoration: none/underline 去除和恢复a标签下划线
    + cursor:pointer 鼠标指针变为"小手"
    + display 修改元素性质 block(块)/inline-block(行内块)/inline(行内)/none(隐藏)
    + outline: none 去除input标签点击外边框效果
      1. 隐藏后显示
      选中父类标签:hover 选中标签{display:block/inline-block/inline}
      2. display：inline-block 标签的换行符会被显示为空格
    + border-radius: xxpx/xx%  圆角 (50%时变为圆形)
    + visibility: hidden(隐藏)/visible(显示) 隐藏后其在文档中所占的位置会依然保持
    + over-flow 文档查出部分 visible(默认值)/scroll(添加滚动条)/auto(根据需要添加滚动条)/hidden(隐藏超出盒子的内容)
    + margin: xxpx auto  可以实现左右居中
+ 盒子模型
    + content 内容区域
    + padding 内边距 
        + padding-top/bottom/right/left
        + padding: xxpx xxpx xxpx xxpx(上右下左)
    背景图片会出现在padding区域,且padding区域背景颜色与内容区域相同
    + border 边框
        + border-top/bottom/right/left
        + border: xpx(边框厚度) solid(线条类型) #xxxxxx(颜色)
        + border-width 
          border-style none (默认) / dashed(虚线) / dotted（点） / solid(实线) / double(双实线) 
          border-colo
    + margin 外边距
        + margin-top/bottom/right/left
        + margin: xxpx xxpx xxpx xxpx(上右下左)
        + 嵌套崩塌 两个盒子发生嵌套的时候，给子类设置maring会给父类造成一种崩塌现象，子类的margin-top没有效果，而直接作用到父类。
          解决方法 1.给父类盒子设置 overflow: hidden
                  2.给父类设置极小的padding/border
        + 两盒子 水平方向margin值叠加 垂直方向margin值重叠(margin值为跟大的那个)
+ 浮动
    + float:left/right(右浮动 顺序改变)/none(不浮动)
   
    + 表现形式
    1. 脱离文档流,但不会飘出父元素
    2. 块级元素和行内元素都可以浮动，当一个行内元素浮动以后将会自动变为一个块级元素
    3. 当一个块级元素浮动以后，宽度会默认被内容撑开，所以当漂浮一个块级元素时我们都会为其指定一个宽度
    4. 当一个元素浮动以后，其下方的元素会上移。元素中的内容将会围绕在元素的周围。
    浮动会使元素完全脱离文本流，也就是不再在文档中在占用位置。
    5. 元素设置浮动以后，会一直向上漂浮直到遇到父元素的边界或者其他浮动元素。
    6. 元素浮动以后即完全脱离文档流，这时不会再影响父元素的高度。也就是浮动元素不会撑开父元素。
    7. 浮动元素默认会变为块元素，即使设置display:inline以后其依然是个块元素。  
    + 浮动影响
    如果子类元素设置了浮动，而父类元素没有设置高度，或者高度比子类元素小，那么子类元素脱离了文档流，就无法把父类盒子撑开。那么整个文档的结构将受到破快。
    + 清除浮动的影响：
        1. 严格计算父类盒子高度
        2. 给父类盒子 设置 overflow:hidden
        3. 在浮动元素的最后面追加一个空的div,设置clear:both即可清除浮动的影响。
+ 定位
    + position: static(默认)/relative(相对定位)/absolute(绝对定位)/fixed(固定定位)/sticky;
      right/left: xxpx;
      top/bottom: xxpx;
    + relative 相对定位。 相对元素本身的位置定位。
        + 每个元素在页面的文档流中都有一个自然位置。相对于这个位置对元素进行移动就称为相对定位。周围的元素完全不受此影响。
        + 当开启了相对定位以后，可以使用top、right、bottom、left四个属性对元素进行定位。
        + 如果不设置元素的偏移量，元素位置不会发生改变。
        + 相对定位不会使元素脱离文本流。元素在文本流中的位置不会改变。
        + 相对定位不会改变元素原来的特性。
        + 相对定位会使元素的层级提升，使元素可以覆盖文本流中的元素。
    + absolute 绝对定位指使元素相对于html元素或离他最近的祖先定位元素进行定位。
        + 当开启了绝对定位以后，可以使用top、right、bottom、left四个属性对元素进行定位。
        + 绝对定位会使元素完全脱离文本流。
        + 绝对定位的块元素的宽度会被其内容撑开。
        + 绝对定位会使行内元素变成块元素。
        + 一般使用绝对定位时会同时为其父元素指定一个相对定位，以确保元素可以相对于父元素进行定位。
    + fixed 固定定位。元素会被锁定在屏幕的某个位置上，当访问者滚动网页时，固定元素会在屏幕上保持不动。
        + 固定定位不占据原来的位置，会脱标。
        + 给元素设置固定定位之后，元素位置从浏览器左上角出发。
        + 可以将行内元素转换为行内块元素。
    + 补充 定位上下居中
        1.先将其定位  top/bottom: 50%
        2.上移或下移自身的一半
        margin-top/bottom: -自身一半的值

+ z-index 当元素开启定位以后就可以设置z-index这个属性。默认是0值越大，越靠上。
z-index可以指定一个整数作为参数，值越大元素显示的优先级越高，也就是z-index值较大的元素会显示在网页的最上层。
+ css设置文字多余部分显示省略号
    // 有时添加在嵌入样式中不生效，需要添加在行内样式中
    + 显示单行
        overflow: hidden;
　　    text-overflow:ellipsis;
　　    white-space: nowrap;
    + 显示多行 
        word-break: break-all;
　　    text-overflow: ellipsis;
　　    display: -webkit-box;
　　    -webkit-box-orient: vertical;
　　    -webkit-line-clamp: 2; //行数
　　    overflow: hidden;    

