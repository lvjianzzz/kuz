Vue
前言
使用vue开发大型项目时，需要考虑到目录结构、项目构建以及部署、热加载、代码单元化测试等事情，如果手动完成这些，效率非常低，一般情况下我们使用脚手架完成这样的工作。在vuejs的生态中，我们可以使用vue-cli来快速的构建项目。
## 1.下载nodejs    
下载地址


## 2.同意node的协议

## 3.选择node的安装路径

## 4.选择online documentation shortcuts

## 5.安装

## 6.检查是否安装完成
输入node –v 或 npm –v 如果出来就代表安装完成



## 7.设置淘宝镜像(由于被墙的缘故，所以安装依赖较慢，设置镜像之后就没有这个问题)
npm install -g cnpm --registry=https://registry.npm.taobao.org

## 8.局安装vue脚手架  2.x的版本 现在的是3.x的版本
cnpm i vue-cli -g
## 9.安装成功可以查看版本
vue -V
## 10.vue创建基于webpack模板的项目 vue init webpack helloworld
## 11.安装依赖 cnpm install
## 12.项目运行 npm run dev
4修改app.vue里面的代码为
<template>
  <div id="app">
    {{msg}}
  </div>
</template>

<script>
export default {
  name: 'App',
  data () {
    return {
      msg:"hello"
    }
  }
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>

## 13.新版vue3创建项目

 vue create my-project


选择default按照操作就行

自定义

选择babel router vuex css预处理器

选择路由history

Scss预处理器

保存配置文件到package.json

项目目录
(一)前言
vuejs作为单页应用的必备技术之一，对于解决大部分的单页简单应用，是比较实用而且轻量级的
备注：vue不支持ie8等低版本浏览器。
(二)目录结构
目录/文件	说明
build	最终发布的代码存放位置
config	配置目录，包括端口号等
node_modules	npm 加载的项目依赖模块
src	这里是我们要开发的目录，基本上要做的事情都在这个目录里。里面包含了几个目录及文件：assets: 放置一些图片，如logo等；components: 目录里面放了一个组件文件，可以不用；App.vue: 项目入口文件，我们也可以直接将组件写这里，而不使用 components 目录； main.js: 项目的核心文件
static	静态资源目录，如图片、字体等
test	初始测试目录，可删除
.xxxx文件	这些是一些配置文件，包括语法配置，git配置等
index.html	首页入口文件，你可以添加一些 meta 信息或统计代码啥的
package.json	项目配置文件，在这里可以查看依赖
README.md	项目的说明文档，markdown 格式

render: h => h(App); // render:function(createElement){ createElement (App)}

其中 根据 Vue.js 作者 Even You 的回复，h 的含义如下：
It comes from the term "hyperscript", which is commonly used in many virtual-dom implementations. "Hyperscript" itself stands for "script that generates HTML structures" because HTML is the acronym for "hyper-text markup language".
它来自单词 hyperscript，这个单词通常用在 virtual-dom 的实现中。Hyperscript 本身是指 
生成HTML 结构的 script 脚本，因为 HTML 是 hyper-text markup language 的缩写（超文本标记语言）

理解：createElement 函数是用来生成 HTML DOM 元素的，也就是上文中的 generate HTML structures，也就是 Hyperscript，这样作者才把 createElement 简写成 h。
 Vue.js 里面的 createElement 函数，这个函数的作用就是生成一个 VNode节点，render 函数得到这个 VNode 节点之后，返回给 Vue.js 的 mount 函数，渲染成真实 DOM 节点，并挂载到根节点上。


