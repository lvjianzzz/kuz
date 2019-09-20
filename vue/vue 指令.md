开发版本 [https://cdn.jsdelivr.net/npm/vue/dist/vue.js](https://cdn.jsdelivr.net/npm/vue/dist/vue.js)
生产版本 [https://cdn.jsdelivr.net/npm/vue](https://cdn.jsdelivr.net/npm/vue)
# vue 常用指令
## 1.插值 v-text v-html {{}}
1. {{ }}     用来插入文本内容及执行简单的函数
```
<style>
  [v-cloak]{
    display:none;
  }
</style>
<div id="app" v-cloak>
// 用来解决页面闪烁问题 刷新页面出现大括号
```
2. v-text  用于渲染文本 不能在同一个标签写多个
3. v-html  用于解析标签
## 2.v-if v-show
* 指令v-show 控制元素的显示和隐藏 特点是vue在渲染有v-show的节点时这个节点的样式为display:none
* v-if 也是控制元素的显示和隐藏 如果为false的话在页面里面这个节点是不会渲染的
* v-if v-else-if v-else vue的条件语句
  * v-if 控制元素的显示和隐藏
  * v-else-if 前一兄弟元素必须有 v-if 或 v-else-if。
  * v-else 前一兄弟元素必须有 v-if 或 v-else-if。
```
<div v-if="bol">
   {{ name }}
</div>
        <!-- age>40 值为false -->
<p v-else-if="age>40">
   v-else-if: {{ age }}
</p>
<div v-else="!bol">
   {{ age }}
</div>

// bol为false
```
## 3.v-for
### 数组遍历
```
<ul>
    <li v-for="(item,index) in  list" :key="id">
         {{ item.name }} {{ item.age }} {{ index }}
         // item代表子元素 index 循环的下标
    </li>
</ul>
```
### 对象遍历
```
<ul>
    <li v-for="(val,name,index) in list" :key="id">
       {{ val }} {{ name }} {{ index }}
       <!--  val就代表循环的属性值 name 代表循环的属性名称 index循环的下标-->
    </li>
</ul>
```
## 4.v-bind 简写(:)  单向绑定
1. v-bind 动态绑定标签里面的属性 只要是标签里面的属性 都可以进行绑定
2. v-bind默认绑定的值是变量 如果想要直接绑定字符串 那么需要直接在这个字符串外面加引号
## 6.v-pre
vue默认不会解析这个标签
```
<div v-pre>
         {{ titles }}
</div>
```
## 5.v-once 
只在页面渲染一次
```
<div v-once>
            {{ titles }}
</div>
```

## 6.v-model  双向绑定
v-model指令用来在input、select、textarea、checkbox、radio等表单控件或者组件上创建双向绑定。
### v-model修饰符
1. v-model.trim   用于清除输入的前后空格
2. v-model.lazy   在 change 事件中同步
3. v-model.number  把用户输入的值转换成数字
## 7.v-on 绑定事件 简写(@)
鼠标事件 v-on: click / mouseover / mouseleave / mouseenter / mouseout / dblclick双击
```
//事件对象
<input type="button" value="按钮" @click="show($event)">
```
### 事件修饰符
1. v-on:click.stop  阻止事件冒泡
2. @click.prevent 阻止默认事件
3. @click.capture 实现事件捕获
4. @click.self       让点击事件只在当前元素触发
5. @click.once     事件只触发一次
```
<!-- 提交事件不再重载页面 -->
<form v-on:submit.prevent="onSubmit"></form>

<!-- 修饰符可以串联 -->
<a v-on:click.stop.prevent="doThat"></a>
```
### 按键修饰符
按键事件 keyup
```
 <input type="text" value="按钮" @keyup.enter="show()"/>
 键盘 上 up  下 down  左 let   右 right 
```
## 8.watch侦听器
可以监听data中数据的变化 然后触发watch中的函数变化 只有当数据更改的时候才会执行  侦听器监听的数据不能更改
```
<div id="app">
      姓<input type="text" v-model="xi" >+
      名<input type="text" v-model="name" >=
      完整姓名<input type="text" v-model="total">
</div>
var vm = new Vue({
        el: "#app",
        watch:{
          xi(newVal , oldVal){ // 新值  老值
                console.log("newVal ",newVal);
                console.log("oldVal ",oldVal);
                this.total = newVal + this.name;
            },
            name(newVal , oldVal){
                this.total =this.xi + newVal  ;
            }
        }
});
```
## 9.计算属性
computed 在vue中一些数据经常依赖于别的数据做出改变，且改变的逻辑也较复杂，这个时候就需要用到计算属性
特点
1. 计算属性本质是一个方法 但调用的时候不加括号
2. 计算属性所依赖的数据变化必然会触发计算属性的重新求值
3. 计算属性的值会缓存；
```
<div id="app">
      翻转过的数据:{{ reverse }}
      <input type="text" v-model="ipt">
      <hr>
      姓<input type="text" v-model="xi" >+
      名<input type="text" v-model="name" >=
      完整姓名<input type="text" :value="total">
      {{ total }}{{ total }}{{ total }}
</div>

computed: { /// 新建一个computed就代表这个里面的方法就叫做计算属性
          reverse(){
            return this.ipt.split("").reverse().join("");
          },
          total(){ // total是一个函数 这个函数里面存储了所需要的值 
            console.log("计算属性");
            return this.xi + this.name;
          }
},
```
### 侦听器和计算属性的不同
1. 计算属性一进入页面 就会执行 侦听器 只有当数据更改的时候才会执行
2. 侦听器监听的数据不能更改 计算属性当依赖的属性更改的时候会自动执行
3. 计算属性会缓存结果
4. 计算属性必须return一个值 而watch不需要
## 10.Class 与 Style绑定
1. 三元运算符
```
 <div :class=" num <= 10 ? 'on' : 'green'">
```
1. 对象的方式
```
<div v-bind:class="{ red:currentClass , green: !currentClass}"></div>
```
1. 数组方式
```
<div v-bind:class="[{red:currentClass , green: !currentClass}]"></div>
```
## 11.内联样式绑定
```
<!-- 绑定内联样式 对象的方式绑定 -->
        <!-- 2. 数组的方式绑定 -->
<div :style="{color:'red'}">
     //内联样式绑定
</div>
<div :style="[{color:'red'},{'font-size':'30px'}]">
     // 内联样式绑定
</div>
```
## 12.事件传值
```
<div id="app">
        <ul>
            <!-- $event -->
            <li v-for="item in list" :key="item.id" @click="del(item.id,$event)">
                {{ item.area }} <input  type="text" v-if="item.isInputShow">
            </li>
        </ul>
    </div>
    <script>
        
      var vm = new Vue({
        el: "#app",
        data() {
          return {
            list:[
                {
                    area:"河南",
                    id:1001,
                    isInputShow:false
                },
                {
                    area:"北京",
                    id:1002,
                    isInputShow:false
                },
                {
                    area:"上海",
                    id:1003,
                    isInputShow:false
                },
            ]
          };
        },
        methods: { // 专门用于处理事件
            del(val,e){
                console.log(val,e);
                var ele = this.list.find(ele => ele.id == val );
                ele.isInputShow = true;
                setTimeout(()=>{
                    console.log(e.target.childNodes);
                    var arr = Array.from(e.target.childNodes);
                    var eles = arr.find(ele => ele.nodeType == 1);
                    eles.focus();
                })
```

