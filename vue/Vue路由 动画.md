# 动画
## 自定义过渡的类名
* enter-class
* enter-active-class
* enter-to-class (2.1.8+)
* leave-class
* leave-active-class
* leave-to-class (2.1.8+)

他们的优先级高于普通的类名，这对于 Vue 的过渡系统和其他第三方 CSS 动画库，如 [Animate.css](https://daneden.github.io/animate.css/) 结合使用十分有用。
# npm安装vue路由
这一步是安装路由 保存到我们package.json 里面的dependencies里面
```
cnpm install vue-router --save
```
## vue-router的使用
* 引入vue-router 注册全局router Vue.use(Router) vue.use就代表全局插件
```
<script>
import Vue from "vue";
import Router from "vue-router"

Vue.use(Router)
</script>
```
* 写router的配置
```
import Vue from "vue";
import Router from "vue-router"

Vue.use(Router)

const router = new Router({

    routes:[ // 存放所有路由的地方 
        
    ]
})
```
* 每个路由配置是一个对象
  * path 定义访问的路径
  * component 路由所对应的组件
* 选择router 需要渲染的区域 一般把这个区域放在App.vue里面
  * router-view 组件 路由将会被渲染的位置
  * royter-link 类似a标签 跳转连接用的
* 路由重定向 redirect 指定页面需要被重定向的路由
## 跳转方法
```
// js的方式跳转页面
this.router.push("需要跳转的路径")进行跳转this.router.push("/home/1")(不存在缓存问题 传值也简单 )

// 在浏览器中前进一步  等同于 history.forward()
router.go(1)
// 在浏览器后退一步  等同于 history.back()
```
## 路由重定向 redirect
重定向 把地址重定向到某个路由 重定向”的意思是，当用户访问 /a时，URL 将会被替换成 /b，然后匹配路由为 /b
```
const router = new VueRouter({
  routes: [
    { path: '/a', redirect: '/b' }
  ]
```
## })

路由懒加载
1. 对页面优化有很大的好处
1. 最主要的作用 当匹配奥路由的时候再路由对应的组件
1. 脚手架打包项目的时候默认会把所有的路由对应的组件打包进router-view里面(app.vue)
1. 路由懒加载 吧路由对应的组件打包成一个个js文件 在需要的时候再引入打包生成的js文件
```
component: () => import( '@/views/info/index.vue')
```
# route router
* route  当前的路由对象 
  * this.$route 当前路由界面
  * v-if="$route.meta.isshow"  可以判断导航
* router 所有的路由对象 可以想象成路由配置文件
  * this.$router.push('/home')   js跳转页面
## 导航守卫
### 全局守卫
* 只要加了全局守卫,每次路由的跳转都要经过全局守卫,一般用的是前置守卫
  * 全局前置守卫应用场景(进入页面登录判断、管理员权限判断、浏览器判断等)
```
// 可以通过导航首位判断用户有没有权限进入某个页面
<script>
    // to 代表我们将要跳转的路径
    // from 上一个路径
    // next代表 守卫可以通过next控制下一步的跳转 如果写了前置守卫 一定要添加next()到下一步
    // 需要注意的是 如果当跳转的地址带参数的时候(动态路由) next("/user/1")
    router.beforeEach((to, from, next) => {
        if(to.path != "/login"){
        if(localStorage.getItem("user")){
            next()
        }else{
            next("/login")
        }
        }else{
        next()
        }
    })
</script>
```
### 路由守卫
运行在路由上的守卫 (相比上面的全局守卫 全局守卫是只要有跳转就会执行守卫函数 而路由守卫呢 是只有跳转到当前的守卫时才执行路由守卫函数) 用处做跳转判断
```
const router = new VueRouter({
  routes: [
    {
      path: '/foo',
      component: Foo,
      beforeEnter: (to, from, next) => {
        // ...
      }
    }
  ]
})
```
### 组件守卫
* beforeRouteEnter 这个守卫不做什么操作 在这一步的时候this都还没有绑定到vue实例类上(组件实例还没有被创建) 也就是说在这一步我们还不能用this
* beforeRouteUpdate (在组件复用的时候调用 用于解决组件复用问题)
* beforeRouteLeave (导航离开该组件的对应路由时调用 这个离开守卫通常用来禁止用户在还未保存修改前突然离开。该导航可以通过 next(false) 来取消。 还可以用来清除定时器)
### 路由元信息
在路由列表中，每个路由都有一个 meta 元数据字段， 我们可以在这里设置一些自定义信息，供页面组件或者路由钩子函数中使用。（如设置网页标题,设置某个页面是否需要登陆才能进入）
* window.document.title = to.meta.title
```
export default new VueRouter({
  routes: [
    {
      path: '/foo',
      component: Foo,
      children: [
        {
          path: 'bar',
          component: Bar,
          // a meta field
          meta: { title: true }
        }
      ]
    }
  ]
})
router.beforeEach((to, from, next) => {
  window.document.title = to.meta.title;
  next();
})
```

## 滚动行为
使用前端路由，当切换到新路由时，想要页面滚到顶部，或者是保持原先的滚动位置，这个时候就可以使用router的滚动行为
* 理解 vue在页面切换的时候 比如a页面跳转到b页面的时候 滚动条的位置是保持不变的 跟传统路由切换页面相差很大
* 如果要实现和前端路由一样的效果 这个时候就可以使用router提供的滚动行为 这个更好[vue-router官方issues](https://github.com/vuejs/vue-router/issues/2533) (浏览器后退时返回到顶部)
```
scrollBehavior (to, from, savedPosition) {
    return new Promise((resolve, reject) => {
        setTimeout(() => {
        resolve({ x: 0, y: 0 })
        })
    })
    }
```
# html5 History模式
* mode属性 跟routers 同级 俩值  `hash` `history` 
* vue-router 默认 hash 模式 —— 使用 URL 的 hash 来模拟一个完整的 URL，于是当 URL 改变时，页面不会重新加载。

* 如果不想要很丑的 hash，我们可以用路由的 history 模式，这种模式充分利用 history.pushState API 来完成 URL 跳转而无须重新加载页面。
* 当使用 history 模式时，URL 就像正常的 url，例如 [http://yoursite.com/user/id，也好看！](http://yoursite.com/user/id%EF%BC%8C%E4%B9%9F%E5%A5%BD%E7%9C%8B%EF%BC%81)
* 不过这种模式要玩好，还需要后台配置支持。因为我们的应用是个单页客户端应用，如果后台没有正确的配置，当用户在浏览器直接访问 [http://oursite.com/user/id](http://oursite.com/user/id) 就会返回 404。

[https://router.vuejs.org/zh/guide/essentials/history-mode.html#后端配置例子](https://router.vuejs.org/zh/guide/essentials/history-mode.html#%E5%90%8E%E7%AB%AF%E9%85%8D%E7%BD%AE%E4%BE%8B%E5%AD%90)
>解决方法
>在服务端增加一个覆盖所有情况的候选资源：如果 URL 匹配不到任何静态资源，则应该返回同一个 index.html 页面，这个页面就是你 app 依赖的页面。

