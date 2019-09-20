Vue 实现了一套内容分发的 API，将 元素作为承载分发内容的出口。
插槽（Slot）是Vue提出来的一个概念，正如名字一样，插槽用于决定将所携带的内容，插入到指定的某个位置，从而使模板分块，具有模块化的特质和更大的重用性。
插槽显不显示、怎样显示是由父组件来控制的，而插槽在哪里显示就由子组件来进行控制。
## 默认插槽 slot
```
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>Document</title>
    <script src="lib/vue.js"></script>
</head>
<body>
    <div id="app">
        <div>123</div>
        <com>
            <div>
                插入组件的标签
            </div>
            456
        </com>
    </div>
    <script>
        var vm = new Vue({
            el:"#app",
            components: {
                "com" : {
                    template:"<h2>子组件<slot></slot></h2>"
                }
            }
        })
    </script>
</body>
</html>
```
## 具名插槽
```
用于标记往哪个具名插槽中插入子组件内容。简单理解就是 给每一个 slot 一个name属性，父组件中 使用子组件标签时用的v-slot:name要跟子组件的name匹配上，才会渲染出来需要template
<div id="app">
        
        <com>
            <template v-slot:header>
                <h1>标题</h1>
            </template>
            <template v-slot:main>
                <h2>内容</h2>
            </template>
            <template v-slot:footer>
                <h3>底部内容</h3>
            </template>
        </com>
    </div>
    <script>
        var vm = new Vue({
            el:"#app",
            data () {
                return {
                    info:1
                }
            },
            components: {
                "com" : {
                    template:`
                    <div class="container">
                        <header>
                            <slot name="header"></slot>
                        </header>
                        <main>
                            <slot name="main"></slot>
                        </main>
                        <footer>
                            <slot name="footer"></slot>
                        </footer>
                    </div>
                    `
                }
            }
        })
    </script>
```
## 编译作用域
```
<div id="app">
        <!-- 在组件标签里面写的变量查找的是父级里面的属性或者方法 编译作用域 作用域默认是父级的而不是自定义组件里面的作用域 -->
        <com>
            {{ msg }} 
        </com>
    </div>
    <script>
      var vm = new Vue({
            el: "#app", 
            data() {
                return {
                   isInputShow:true,
                   msg:"不凡学院"
                };
            },
            methods: { 
            },
            components: {
                com:{
                    template:`<div><slot></slot></div>`,
                    data () {
                        return {
                            name:"不凡学院",
                            msg:"郑州"
                        }
                    },
                    methods: {
                        getParent(){
                           console.log(this.$root.isInputShow)
                        },
                        alerts(){
                            alert(this.name)
                        }
                    },
                }
            }
        });
```

## 后备内容
```
// 在组件中没有写入内容的时候默认展示的内容
<div id="app">
        {{ red }}
        <com1></com1>
    </div>
    <script>
      var vm = new Vue({
        el: "#app",
        data(){
            return {
                isActive : true,
                red:"red"
            }
        },
        components: {
          com1 : {
            data(){
              return {
                info:"子组件内容"
              }
            },
            template:"<h2>我是子组件{{ info }}<slot>我是插槽的默认内容</slot></h2>"
            
          }
        }
      });
    </script>
```
## vue的可复用性与组合
混入 混入 (mixins) 是一种分发 Vue 组件中可复用功能的非常灵活的方式。混入对象可以包含任意组件选项。当组件使用混入对象时，所有混入对象的选项将被混入该组件本身的选项。
比如 vue有可复用的属性的方法的话 可以把可复用的属性或者方法提取出来 未来有某个组件需要用到这个属性或者方法 可以把这个属性或者方法直接混入到这个组件里面

## 动画
* v-enter 定义进入过渡的开始状态。在元素被插入之前生效，在元素被插入之后的下一帧移除。
* v-enter-active：定义进入过渡生效时的状态。在整个进入过渡的阶段中应用，在元素被插入之前生效，在过渡/动画完成之后移除。这个类可以被用来定义进入过渡的过程时间，延迟和曲线函数。
* v-enter-to: 2.1.8版及以上 定义进入过渡的结束状态。在元素被插入之后下一帧生效 (与此同时 v-enter 被移除)，在过渡/动画完成之后移除。
* v-leave: 定义离开过渡的开始状态。在离开过渡被触发时立刻生效，下一帧被移除。
* v-leave-active：定义离开过渡生效时的状态。在整个离开过渡的阶段中应用，在离开过渡被触发时立刻生效，在过渡/动画完成之后移除。这个类可以被用来定义离开过渡的过程时间，延迟和曲线函数。
* v-leave-to: 2.1.8版及以上 定义离开过渡的结束状态。在离开过渡被触发之后下一帧生效 (与此同时 v-leave 被删除)，在过渡/动画完成之后移除。
```
<style>
        .animated{
            animation-duration: 4s!important;
        }
    </style>
    <link rel="stylesheet" href="https://daneden.github.io/animate.css/animate.min.css">
  </head>
  <body>
    <div id="app">
        <!-- enter-active-class 动画进入时将要执行的类名 -->
        <!-- leave-active-class 动画离开时将要执行的类名 -->
        <!-- duration 过渡持续时间 -->
        <transition enter-active-class="animated fadeIn" leave-active-class="animated fadeOut" 
        :duration="{ enter : 4000 , leave : 3000}">
            <div class="box" v-if="boxShow">

              </div>
              <h2 v-else>h2标签</h2>
        </transition>
        <button @click="boxShow = !boxShow">div动画</button>
    </div>
    <script>
      var vm = new Vue({
        el: "#app",
        data(){
            return {
                rootInfo:"我是根元素的属性",
                isShow:false,
                boxShow:true
            }
        },
        methods: {
          alerts(){
            alert(111)
          }
        },
      });
```
# 
# 
# 
# 获取组件节点的方法
```
1. 获取父组件的属性或方法  this.$parent.isInputShow
2. 获取根组件的属性或方法  this.$root.alerts()
3. 获取子组件的属性或方法
// this.$ref.com1.name
<com ref="com1"></com>
```
## 
