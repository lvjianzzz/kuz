# DOM
（在 HTML DOM （文档对象模型）中，每个部分都是节点
文档本身是文档节点
所有 HTML 元素是元素节点
所有 HTML 属性是属性节点
HTML 元素内的文本是文本节点
注释是注释节点
+ HTML DOM Element 对象
在 HTML DOM 中，Element 对象表示 HTML 元素
+ document对象
Document 对象是 Window 对象的一部分，可通过 window.document 属性对其进行访问
每个载入浏览器的 HTML 文档都会成为 Document 对象
Document 对象使我们可以从脚本中对 HTML 页面中的所有元素进行访问
+ document.body
返回html dom中的body节点 即<body>
+ document.documentElement
返回html dom中的root 节点 即<html>）（来自网络）
+ H5新增
    + 获取元素
        + document.querySelector("同css选择器")
        html5新选择器，参数是css选择器参数,选择选中的第一个
        + document.querySelectorAll("")
        选择全部
    + 类名操作
        + Node.classList.add('class') 添加类名
        + Node.classList.remove('class') 移除类名
        + Node.classList.toggle('class') 切换类型，有责移除，无责添加
        + Node.classList.contains('class') 检测是否存在类名
        + Node.classList.item(index) 
        返回元素中索引值对应的类名。索引值从 0 开始
        如果索引值在区间范围外则返回 null
    + 自定义属性
        `data-属性名="属性值"` 在标签内添加自定义属性 
        Node.dataset.属性名（驼峰命名） 获取自定义属性的属性值
+ 事件三要素
    事件三要素: 事件源 事件 事件处理程序
    1. 获取事件源
    2. 给事件源绑定事件
    3. 触发点击事件时 做的事情
+ DOM 是由节点组成的;
   DOM 为文档提供了结构化表示，并定义了如何通过脚本来访问文档结构。目的其实就是为了能让 js 操html 元素而制定的一个规范;
   HTML 加载完毕，渲染引擎会在内存中把 HTML 文档，生成一个 DOM 树;
   节点: 元素节点 文本节点(换行空格都是节点)属性节点 注释节点;
+ 获取事件源
    获取到的均为伪数组
    + 通过id获取
    document.getElementById('id值')
    + 通过class 获取(ie678)用不了
    document.getElementsByClassName('class名')
    + 通过标签名获取
    document.getElementsByTagName('标签名')
    + 获取父亲节点
    node(dom对象).parentNode
    + 获取兄弟节点
    nextsibling 标准属性
    火狐、谷歌、IE9+版本：都指的是下一个节点（包括标签、空文档和换行节点）
    IE678 版本：指下一个元素节点（标签）
    nextElementSibling 非标准属性
    火狐、谷歌、IE9+版本：都指的是下一个元素节点（标签）
    ie678中没有这个属性
    兼容写法
    ` var nextS = li3.nextElementSibling || li3.nextSibling;`
    + 上一个兄弟节点
    previousSibling
    previousElementSibling
    + 获取子节点
    fistChild
    `高级浏览器 包括换行符等节点`
    `ie5678  下一个 元素 节点`
    firstElementChild
    `高级  下一个元素节点`
    `ie5678 不支持`
    lastChild
    lastElementChild
    childNodes
    `高级  包括 注释 换行符`
    children
    `获取 所有元素子节点(不包括空格换行符)`
    `在 IE6/7/8 中包含注释节点（在 IE678 中，注释节点不要写在里面）`
    ```
    // 兼容 
        function myChildren(el) {
            var children = el.childNodes;
            var result = [];
            for (var i = 0; i < children.length; i++) {
                // children[i]判断是不是元素节点
                // 通过nodeType 来判断 是哪种节点
                // 1 元素节点
                // 3 文本节点
                // 8 注释节点
                if (children[i].nodeType === 1) {
                    result.push(children[i])
                }
            }
            return result;
        }
        var children = myChildren(ulEl);
        console.log(children);
    ```
    + 获取除自己以外的所有兄弟节点
    ```
     var li3 = document.getElementsByClassName('li3')[0];

        function getSiblings(el) {
            var elParent = el.parentNode;
            var elChildren = elParent.children;
            var result = [];
            for (var i = 0; i < elChildren.length; i++) {
                // 不具备数组方法
                // console.log(elChildren[i].splice);
                if (elChildren[i] !== li3) {
                    result.push(elChildren[i]);
                }
            }
            return result;
        }
        var siblings = getSiblings(li3);
        console.log(siblings);


        // 实现 获取 li3 后边的 所有兄弟节点
        // 倒着 遍历
        function getNextSiblings(el) {
            var elParent = el.parentNode;
            var elChildren = elParent.children;
            var result = [];
            var lock = false;
            for (var i = 0; i < elChildren.length; i++) {
                if (elChildren[i] == li3) {
                    lock = true;
                    continue;
                }
                if (lock) {
                    result.push(elChildren[i]);
                }
                // console.log(1);
            }
            return result;
        }
        console.log(getNextSiblings(li3));
    ```
    + 节点属性操作
        + 获取节点属性
        元素节点.getAttribute("属性名称")
        + 增加节点属性
        元素节点.setAttribute(属性名, 新的属性值)
        如果指定属性已经存在,则只设置该值
        + 删除节点属性
        元素节点.removeAttribute(属性名)
+ 常用事件
    onabort	图像加载被中断
    onblur	元素失去焦点
    onchange	用户改变域的内容
    onclick	鼠标点击某个对象
    ondblclick	鼠标双击某个对象
    onerror	当加载文档或图像时发生某个错误
    onfocus	元素获得焦点
    onkeydown	某个键盘的键被按下
    onkeypress	某个键盘的键被按下或按住
    onkeyup	某个键盘的键被松开
    onload	某个页面或图像被完成加载
    onmousedown	某个鼠标按键被按下
    onmousemove	鼠标被移动
    onmouseout	鼠标从某元素移开
    onmouseover	鼠标被移到某元素之上
    onmouseup	某个鼠标按键被松开
    onreset	重置按钮被点击
    onresize	窗口或框架被调整尺寸
    onselect	文本被选定
    onsubmit	提交按钮被点击
    onunload	用户退出页面
+ DOM节点的操作
    + 创建新节点
    新的标签(元素节点) = document.createElement("标签名")
    + 父节点的最后插入一个新的子节点
    父节点.appendChild(新的子节点)
    当多个节点同时插入同一个节点时，具有剪切效果
    + 在参考节点前插入一个新的节点
    父节点.insertBefore(新的子节点, 作为参考的子节点)
    如果参考节点为 null，那么他将在父节点里面的最后插入一个子节点
    + 删除节点
    父节点.removeChild(子节点)
    用父节点删除子节点 必须要指定是删除哪个子节点
    删除自身`node1.parentNode.removeChild(node1)`
    + 复制节点
    `要复制的节点.cloneNode()`括号里不带参数和带参数false，效果是一样的
    `要复制的节点.cloneNode()` 深度复制
    + innerHTML
    插入标签 如有标签则会将字符串解析为标签
    + innerText
    插入文本
+ 定时器
    + 定时器
    ```
    setTimeout(function () {
        console.log('你好')
    }, 2000);
    ```
    + 循环定时器(设立，清除)
    ```
    var timer = setInterval(function () {
        console.log('我是循环执行')
    }, 2000);
    clearInterval(timer) //清除循环定时器

    ```
+ nodeType 属性
    获得元素的节点类型
    nodeType == 1 表示的是元素节点(标签)
    nodeType == 2 表示是属性节点
    nodeType == 3 是文本节点
    nodeType == 8 注释节点
    获取出自己以外的兄弟元素
    ```
    function getSiblings(el) {
	    var siblings = [];
	    var pNode = el.parentNode;
	    var children = pNode.children;
	    for (var i = 0; i < children.length; i++) {
	    	// 兼容ie8
	    	if (children[i].nodeType === 1) {
	    		// 不是el再push
	    		if (children[i] !== el) {
	    			siblings.push(children[i]);
	    		}
	    	}
	    }
	    return siblings;
    }
    ```
+ onload事件
    页面加载完成（图片文本加载完成）执行
    window.onload 事件有个事件覆盖的问题
    只可写一个
    ```
    window.onload = function () {}
    ```

