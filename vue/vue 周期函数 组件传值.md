# 生命周期钩子
常用的两个 created mountd 带before的钩子都没啥用  created mounted用作获取数据
## 创建 期间的生命周期函数
### 1.beforeCreate
实例刚在内存中被创建出来，此时，还没有初始化好 data 和 methods 属性
### 2.created
实例已经在内存中创建OK，此时 data 和 methods 已经创建OK，此时还没有开始 编译模板(模板 比如{{}})
### 3.beforeMount
此时已经完成了模板的编译，但是还没有挂载到页面中
### 4.mounted
此时，已经将编译好的模板，挂载到了页面指定的容器中显示
## 运行期间的生命周期函数
### 5.beforeUpdate
状态更新之前执行此函数， 此时 data 中的状态值是最新的，但是界面上显示的 数据还是旧的，因为此时还没有开始重新渲染DOM节点
### 6.updated
实例更新完毕之后调用此函数，此时 data 中的状态值 和 界面上显示的数据，都已经完成了更新，界面已经被重新渲染好了！
## 销毁期间的生命周期函数
### 7.beforeDestory
实例销毁之前调用。在这一步，实例仍然完全可用。
### 8.destroyed
Vue 实例销毁后调用。调用后，Vue 实例指示的所有东西都会解绑定，所有的事件监听器会被移除，所有的子实例也会被销毁。
# 组件
组件的特点
1. data 必须是一个函数
2. 组件是密封的 组件之间的数据是相互独立的 也就是说即使写几个组件 更改其中的某一个组件之间的值 其他的组件也不会受到影响
3. 组件模板中只能有一个根元素
4. 每个组件都有自己的内部状态和方法(data methods) 组件里面的状态是互不影响的

## 全局注册组件
 全局注册的组件可以用在其被注册之后的任何 (通过 new Vue) 新创建的 Vue 根实例，也包括其组件树中的所有子组件的模板中。
```
<div id="app">
        <com></com>
    </div>
    <script>
        // 全局组件
        Vue.component("com",{
            data(){
                return {
                    num : 10
                }
            },
            template:"<h2>{{ num }}</h2>"
        })
        var vm = new Vue({
            el : "#app"
        })
    </script>
```
## 局部组件
```
// 只能在当前页面中使用
<div id="app">
            <com></com>
            <com1></com1>
    </div>
    <script>
        // 局部注册组件
        
        var vm = new Vue({
            el : "#app",
            components: {
                "com":{
                    data () {
                        return {
                            info:"我是局部注册的组件"
                        }
                    },
                    template:"<h3>{{ info }}</h3>"
                },
                "com1":{
                    data () {
                        return {
                            info:"我是局部注册1的组件"
                        }
                    },
                    template:"<h3>{{ info }}</h3>"
                }
            }
        })
    </script>
```
## 组件传值
组件是密封的 所有想给某个组件传值 vue提供了props 通过props传值 这个props是写在我们组件里面的一个属性 传值通过这个属性来传值的
```
<div id="app">
        <is-show prop1="父组件传递的数据" :parinfo="parinfo"></is-show>
    </div>
    <script>
        // 局部注册组件
        
        var vm = new Vue({
            el : "#app",
            data(){
                return {
                    parinfo:"我是父组件的数据"
                }
            },
            components: {
                "is-show":{
                    props:[
                        "prop1",
                        "parinfo"
                    ],
                    data () {
                        return {
                            info:"我是局部注册的组件"
                        }
                    },
                    template:"<h3>{{ info }} {{ prop1 }} {{ parinfo }}</h3>"
                }
            }
        })
    </script>
```
!!!! 单向数据流 父级 prop 的更新会向下流动到子组件中，但是反过来则不行 如果我们实在想改变这个传值 我们用data或者计算属性来代替这个传值

子组件传值
1. 子组件向父元素传递值 通过自定义事件来完成
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
            {{  childInfo }}
        <is-show  :parinfo="parinfo" @childevents="parEvents"></is-show>
    </div>
    <script>
        // 局部注册组件
        
        var vm = new Vue({
            el : "#app",
            data(){
                return {
                    parinfo:"我是父组件的数据",
                    childInfo:""
                }
            },
            methods:{
                parEvents(val){
                    this.childInfo = val;
                    console.log("我是子组件传递过来的数据",val)
                }
            },
            components: {
                "is-show":{
                    props:[
                        "parinfo"
                    ],
                    data () {
                        return {
                            info:"我是局部注册的组件"
                        }
                    },
                    methods: {
                        mes(){
                            this.$emit("childevents",this.info)  //  @childevents="parEvents"
                            console.log("我是子组件里面的事件",this)
                        }
                    },
                    template:"<h3 @click='mes'>{{ info }} {{ parinfo }}</h3>"
                }
            }
        })
    </script>
</body>
</html>
```


