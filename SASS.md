# SASS

Sass/Less是一门CSS预处理语言，它扩展了CSS语言，增加了变量，Mixin，函数等特性，使CSS更易维护和扩展

## 安装

### 安装Ruby

`sass`基于`Ruby`语言开发而成，因此安装`sass`前需要安装`Ruby`

注意：安装过程中请注意勾选`Add Ruby executables to your PATH`添加到系统环境变量

安装完成后需测试安装有没有成功，win+r 输入 cmd 打开命令窗口，输入以下命令：

```
ruby -v
//如安装成功会打印
ruby 2.2.2p95 (2015-04-13 revision 50295) [i386-mingw32]
```

如上已经安装成功。但因为国内网络的问题导致`gem`源间歇性中断因此我们需要更换`gem`源。（使用国内镜像的的gem源 https://gems.ruby-china.com/）如下：>

```
//1.删除原gem源
gem sources --remove https://rubygems.org/

//2.添加国内镜像
gem sources -a https://gems.ruby-china.com/

//3.打印是否替换成功
gem sources -l

//4.更换成功后打印如下
*** CURRENT SOURCES ***
https://gems.ruby-china.com/
```

### 安装Sass

`Ruby`自带一个叫做`RubyGems`的系统，用来安装基于`Ruby`的软件。我们可以使用这个系统来 轻松地安装`Sass`和`Compass`。要安装最新版本的`Sass`和`Compass`，你需要 win+r 输入 cmd 打开命令窗口，输入下面的命令：

```
//安装如下(如mac安装遇到权限问题需加 sudo gem install sass)
gem install sass
gem install compass
```

在每一个安装过程中，你都会看到如下输出：

```
Fetching: sass-3.x.x.gem (100%)
Successfully installed sass-3.x.x
Parsing documentation for sass-3.x.x
Installing ri documentation for sass-3.x.x
Done installing documentation for sass after 6 secon
1 gem installed
```

安装完成之后，你应该通过运行下面的命令来确认应用已经正确地安装到了电脑中：

```
sass -v
Sass 3.x.x (Selective Steve)

compass -v
Compass 1.x.x (Polaris)
Copyright (c) 2008-2015 Chris Eppstein
Released under the MIT License.
Compass is charityware.
Please make a tax deductable donation for a worthy cause: http://umdf.org/compass
```

### Sass常用命令：

```
//更新sass
gem update sass

//查看sass版本
sass -v

//查看sass帮助
sass -h
```



## Sass的编译

### 命令行编译：

```
//单文件转换命令
sass input.scss output.css

//单文件监听命令
sass --watch input.scss:output.css

//如果你有很多的sass文件的目录，你也可以告诉sass监听整个目录：
sass --watch app/sass:public/stylesheets
```

### 命令行编译配置选项：

命令行编译`sass`有配置选项，如编译过后css排版、生成调试map、开启debug信息等，可通过使用命令`sass -v`查看详细。我们一般常用两种`--style`  `--sourcemap`

```
//编译格式
sass --watch input.scss:output.css --style compact

//编译添加调试map
sass --watch input.scss:output.css --sourcemap

//选择编译格式并添加调试map
sass --watch input.scss:output.css --style expanded --sourcemap

//开启debug信息
sass --watch input.scss:output.css --debug-info
```

+ `--style`表示解析后的`css`是什么排版格式
  sass内置有四种编译格式:`nested``expanded``compact``compressed`
+ `--sourcemap`表示开启`sourcemap`调试。开启`sourcemap`调试后，会生成一个后缀名为`.css.map`文件

### 编译演示

```scss
//未编译样式
.box {
  width: 300px;
  height: 400px;
  &-title {
    height: 30px;
    line-height: 30px;
  }
}
```

#### nested 嵌套格式

```scss
/*命令行内容*/
sass style.scss:style.css --style nested

/*编译过后样式*/
.box {
  width: 300px;
  height: 400px; }
  .box-title {
    height: 30px;
    line-height: 30px; }
```

#### expanded 扩展格式

```scss
/*命令行内容*/
sass style.scss:style.css --style expanded

/*编译过后样式*/
.box {
  width: 300px;
  height: 400px;
}
.box-title {
  height: 30px;
  line-height: 30px;
}
```

#### compact 紧凑格式

```scss
/*命令行内容*/
sass style.scss:style.css --style compact

/*编译过后样式*/
.box { width: 300px; height: 400px; }
.box-title { height: 30px; line-height: 30px; }
```

#### compressed 压缩格式

```scss
/*命令行内容*/
sass style.scss:style.css --style compressed

/*编译过后样式*/
.box{width:300px;height:400px}.box-title{height:30px;line-height:30px}
```



## Sass的使用

### 一、嵌套

```scss
// sass 允许样式可以和页面布局一样嵌套
ul{
	list-style: none;
	li{
		width: 200px;
		height: 40px;
		border: 1px solid red;
        span{
            color: red;
        }
        // sass 的嵌套格式中 & 表示父选择器
        &:hover{
            border-color: green;
        }
        &.act{
            text-align: center;
        }
	}
}
// sass 允许使用属性嵌套
.box{
    font: {
        family: "Arial, sans-serif";
        size: 18px;
        weight: border;
    }
    border: 5px solid red {
        left: 0;
        right: 0;
    }
}
```

### 二、变量

```scss
// sass允许声明一个变量
$bgColor: #9000ff;
$border: 1px solid $bgColor;

.box{
	width: 300px;
	height: 300px;
	background-color: $baseSize;
}
.inner{
	border: $border;
}
```

### 三、混合

```scss
/* 语法
@mixin 名字(参数1,参数2...){
	...
}*/
@mixin base{
	width: 200px;
    height: 200px;
    color: green;
    // 可以在公共样式中使用嵌套
    a {
      color: #ccc;  
    }
}
@mixin text($text-color,$font-size){
    color: $text-color;
    font-size: $font-size;
}

.box{
	@include base;    
}
.inner{
    @include text(red,18px);
    // 有时候可能会很难区分每个参数是什么意思，参数之间是一个什么样的顺序,sass允许通过语法$name: value的形式指定每个参数的值
    // @include text($font-size: 18px,$text-color: red);
}

// 为了在@include混合器时不必传入所有的参数，我们可以给参数指定一个默认值
@mixin default($color,$hover: $color,$act: $color){
    color: $color;
    &:hover { color: $hover; }
    &.act { color: $act; }
}
.use{
    @include default(red);
    // $hover 和 $act 也会被自动赋值为 red
}
```

### 四、继承

```scss
// sass 使用@extend 选择器 来继承样式，选择器相关的样式都会继承
.box{
	padding: 15px;
    span {
        color: green;
    }
}

.inner{
	@extend .box;
	background-color: red;
}
```

### 五、导入扩展

```scss
// css @import 引入其它css文件会让浏览器发出请求引入其它css文件。sass中的 @import 可以将其它scss文件中的样式导入到自身文件中
// 文件 init.scss
*{
	margin: 0;
    padding: 0;
}
// 文件 style.scss
@import "init";
.box{
    width: 200px;
}
```

### 六、注释

```scss
在sass中使用这样的多行注释会在压缩输出的css中被去掉
/**
 * 天街小雨润如酥
 * 草色遥看近却无
 */
 sass 编译的css中 单行注释不会显示
 在多行注释的开头加上！号表示强制注释，编译的时候不会被去掉 /**! */ 
```

### 七、 颜色调整

```scss
// adjust-hue(要调整的颜色值,要调整的度数)
// lighten(要处理的颜色,要增加的亮度)  让一个颜色变亮
// darken(要处理的颜色,要减小的亮度)  让一个颜色变暗
// saturate(要处理的颜色,要增加的饱和度)
// desaturate(要处理的颜色,要减少的饱和度)
// opacify(要处理的颜色,要增加的不透明度)
// transparentize(要处理的颜色,要增加的透明度)
$base-color: #ff0000;
.box{
    color: lighten($base-color, 10%);
    background-color: adjust-hue($base-color, 137deg);
}
```

### 八、map

```scss
// 语法： $map: (key1: value1, key2: value2, key3: value3 ...)
// map-keys($colors) 拿到所有的key值
// map-values($colors) 拿到所有的value值
// map-has-key($colors, light) 检测key值是否存在
// map-merge($colors. (grey: $eee)) 合并项目
// map-remove($colors, light) 删除其中的项
$colors: (light: #fff, dark: #000);
.box{
    // map-get 获取map中的某个值
    color: map-get($colors, dark);
}
```

### 九、数值类型与运算

sass 支持的数据类型有:

+ 数字，1, 2, 13, 10px
+ 字符串，有引号字符串与无引号字符串，"foo", 'bar', baz
+ 颜色，blue, #04a3f9, rgba(255,0,0,0.5)
+ 布尔型，true, false
+ 空值，null
+ 数组 (list)，用空格或逗号作分隔符，1.5em 1em 0 2em, Helvetica, Arial, sans-serif
+ maps, 相当于 JavaScript 的 object，(key1: value1, key2: value2)

```scss
/*
type-of()	可以判断类型
sass 支持数学计算	2*8 2+8 除法要加() (8/4) 5px+5px 5px-2 5px*2 (5px*5px) (10px/2px) (40px/2)
sass 支持一些数学函数
	abs()	取绝对值
	round() 取四舍五入的值
	ceil()	向上取整
	floor() 向下取整
	percentage(650px / 1000)	取百分比
	min(8,5,3)	取最小数
	max(8,5,7)	取最大值
字符串 ni + "hao"   wid + th 不能使用*号
字符串函数：
	to-upper-case("width")变大写
	to-lower-case("Width")变小写
	str-length("hello") 求字符串长度
	str-index("hello","h") 求下标
	str-insert("hello","world", 2) 插入
list 列表 如： 1px solid red; 5px 25px 25px 15px;
	length(list) 求长度
	nth(list,1)	根据下标找列表相应位置的值
	index(1px solid red, solid)	根据值找下标
	append(5px 10px, 20px) 添加项
	join(20px 30px, 30px 20px) 合并
	join(20 15, 10 45, common)
*/
```

### 十、拼接、插入

```scss
$version "0.0.1";
/* 项目的当前版本： #{$version} */
$name: "info";
$attr: "border";

.alert-#{$name}{
    #{$attr}-color: #ccc;
}
```

### 十一、控制指令

```scss
// 判断
/*
	@if 条件 {
		...
	} @else if 条件 {
		...
	} @else {
		...
	}
*/
$flag: true;
$width: 200;

.box {
    @if $flag {
        border-radius: 50%;
    } @else{
        border-radius: 10px;
    }
}
.inner {
    @if $width == 200 {
        height: 50px;
    }
}
// 循环 $var 表示变量
/*
	@for $var from <开始值> through/to <结束值> {
		...
		through $var可以等于 结束值，to 不会
	}
*/
$columns: 4;
@for $i from 1 through $columns {
    .col-#{$i} {
        width: 100% / $columns * $i;
    }
}

/*
	@while 条件 {
		...
	}
*/
$j: 6;
@while $j > 0 {
    .item-#{$j} {
        width: 5px * $j;
    }
    $j: $j - 2;
}
// 遍历
/*
	@each $var in $list {
		...
	}
*/
$icons: success error warning;
@each $icon in $icons {
    .icon-#{$icon} {
        background-image: url("../imgs/#{$icon}.png");
    }
}
```

### 十二、函数

```scss
/*
	@function 名称 (参数1,参数2){
		...
	}
*/
$colors: (light: #fff, dark: #000);
@function getColor($key){
    @return map-get($colors, $key);
}

.box{
    color: getColor(light);
}
```

### 十三、警告与错误

```scss
@warn "这是一个警告提示信息";
@error "这是一个错误提示信息";
```



