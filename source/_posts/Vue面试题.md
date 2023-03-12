---
title: Vue面试题
date: 2023-03-12 14:48:27
tags: Vue
categories: 面试题
cover: Vue.png
top_img: Vue.png
---


#### 你对 MVVM 的了解，以及跟 MVC 的区别

M V VM 是 Model-View-ViewModel，MVC 是 Model-View-Controller 的缩写，controller 是控制器的意思，MVVM 是 MVC 的变种

#### 生命周期

- beforCreate 实例创建之前
- created 实例创建之后
- beforeMount 实例挂载之前
- mounted 实例挂载之后
- beforeUpdate 实例更新前
- updated 实例更新后
- beforeDestory
- destoryed
- keep-alive 中的 actived 路由访问此组件时
- keep-alive 中的 deactived 路由访问此组件时



#### v-if 和 v-show 的区别

- v-if 是通过条件渲染或不渲染
- v-show 是通过条件更改 display 属性为 none 或 block；频繁操作一般使用 v-show

#### css 只在当前组件中起作用

style 标签加 scoped 属性

#### vue 中 key 值的作用?  key能不能用index?

如果在 v-for 遍历中不加 key 值，vue 会采用“就地复用”。


#### watch 和 computed 的区别

- watch
  - 不支持缓存，数据变，直接触发
  - 支持异步
  - 监听的数据必须已经定义
- computed
  - 支持缓存，依赖数据改变才会重新触发计算
  - 不支持异步，当内部有异步操作时，则无效

#### keep-alive

内置组件，可以缓存被包裹的组件状态

#### 怎么让部分组件缓存，部分组件不缓存

- include 包含的组件
- exclude 排除的组件
- max 缓存组件最大值
  > 也可以搭配路由使用 meta 中设置参数，然后组件判断当前路由中是否有这个参数

#### Vue 实现双向数据绑定的原理

> 采用数据劫持配合发布者-订阅者模式实现的

- vue2 中使用 Object.defineProperty 来劫持各个属性的 getter 和 setter，当劫持到数据变化时，将变化传给 setter，然后执行相应的回调
- vue3 中使用的是 Proxy 实现。

#### Proxy 的优点缺点

- 可以监听数组的变化
- 可以直接监听对象，而不是监听属性
- 劣势是兼容较差

#### 父子组件传参

- 父传子: 用绑定属性的方式将所需要传递的参数绑定到子组件上，然后子组件中通过或 props，接收参数，从而可以直接使用。props 可以设置参数类型、否为必传、默认值等
- 子传父: 通过$emit 方法，调用父组件的方法，方法中携带要传递的参数，父组间方法被执行，拿到参数

#### 兄弟组件传参

- eventBus 相当于创建一个实践中心，用他来传递和接收参数，项目较小时适合使用

  - new 一个新的 vue 实例 eventbus A 组件传值时触发 eventbus.$emit 方法携带参数
  - B 组件触发 eventbus.$on方法，触发以上事件，拿到传递的值（$on 用完必须$off）

- vuex 状态管理

#### vue 路由 hash 模式和 history 模式

- hash: 在浏览器 url 中显示#，#后边为 hash 值，使用 hash 模式，hash 虽然包含在 url 中，但不配包含在 http 请求中；后端不用单独再去相应配置
- history: 采用 h5 的新特性，提供了两个新方法 pushState()和 replaceState()可以对浏览器路由栈进行修改，以及 popState 时间监听到变化 - replace() 进入新页面，关闭旧页面（不能返
  回） - push() 进入相应页面，保留上个页面（可返回）

#### 路由守卫

- 全局钩子
  - router.beforeEach 前置
  - router.BeforeResolve(2.5 新增，解析守卫)
  - router.afterEach 后置
- 组件内钩子
  - beforeRouteEnter 渲染时
  - beforeRouteUpdate 更新时
  - beforeRouteLeave 离开时
- 路由独享钩子（在路由列表中调用）
  - beforEnter

#### 路由传参

- params 刷新参数会消失
- query 参数展示在 url 中，刷新之后依然存在

#### Vuex（状态存储）

- state 状态数据集，不可以直接修改 state 中的数据
- mutations 相当于组件中的 methods（方法集），用于改变 state 中的数据
- getters 相当于组件中的 compunted,当需要对 state 中的数据进行操作返回一个值的时候，可以使用它
- actions 主要用来存储异步操作
- modules 项目较复杂时，使用它来分模块

#### vue 自定义指令 directive

- 接收一个对象
- 钩子

  - bind 指令被绑定到元素上时调用，只调用一次
  - inserted 当组件被绑定到父节点的时候调用
  - upadte 所在组件更新时调用

- 钩子函数的参数
  - el DOM 元素
  - binding 包含指令名 name、指令绑定之 value 等
  - vNode 虚拟 DOM 节点

#### vue 过滤器 filter

定义过滤器返回一个值，第一个参数为默认值，第二个参数之后为传入的值，组件上以管道符 | 定义

#### mixin 注入

用来分发组件中可混用的功能全局混入时，会影响每个组件的实例，全局混入后，可以通过 this.变量拿到参数

#### nextTick

在下次 DOM 更新循环之后执行延迟回调

#### 虚拟 DOM

> 一个能代表 DOM 树的对象，通常含有标签名、便签上的属性、事件监听和子元素，以及其他属性

- 优点
  - 能减少不必要的 DOM 操作
  - 能跨平台渲染，如 ios 安卓 小程序
- 缺点
  - 需要额外的创建函数如 react 中的 createElement 或者 Vue 中的 h，但是可以通过 jsx 语法或者 vue 的模板语法简化成 html 的写法

#### 父子孙组件传参

$attrs以及$listeners

#### 子组件调用父组件方法 不用属性绑定的方式怎么实现

直接在子组件中通过 this.$parent.event 来调用父组件的方法

#### 动态绑定事件

事件委托的方式

#### vue 打包多页面 优化首屏加载

- 路由采用懒加载
- 不生成 map 文件
- 找到 config/index.js，修改为 productionSourceMap: false
- vue 组件尽量不要全局引入
- 开启 gzip 压缩
- 服务端渲染

#### axios 的封装

使用 promise 做二次封装，添加拦截器，请求头带上 token 响应状态判断。

```javascript
import axios from "axios";

import NProgress from "nprogress"; // 引入nprogress插件
import "nprogress/nprogress.css"; // 这个nprogress样式必须引入

import { BASE_URL, TIMEOUT } from "./config";

const instance = axios.create({
  baseURL: BASE_URL,
  timeout: TIMEOUT,
});
axios.defaults.headers["Content-Type"] = "application/json"; //设置默认提交 json
axios.defaults.transformRequest = (data) => JSON.stringify(data); //把数据对象序列化成 json字符串

instance.interceptors.request.use(
  (config) => {
    NProgress.start(); // 设置加载进度条(开始..)
    // 1.发送网络请求时, 在界面的中间位置显示Loading的组件

    // 2.某一些请求要求用户必须携带token, 如果没有携带, 那么直接跳转到登录页面

    // 3.params/data序列化的操作
    return config;
  },
  (err) => {}
);

instance.interceptors.response.use(
  (res) => {
    NProgress.done(); // 设置加载进度条(结束..)
    return res.data;
  },
  (err) => {
    if (err && err.response) {
      switch (err.response.status) {
        case 400:
          console.log("请求错误");
          break;
        case 401:
          console.log("未授权访问");
          break;
        default:
          console.log("其他错误信息");
      }
    }
    return err;
  }
);

export default instance;
```

#### vue-router 动态路由

在 router 目录下的 index.js 文件下，对 path 属性加上/：id。使用 router 对象的 params.id

#### 插槽 slot

组件封装时，可通过插槽 slot 设置占位，调用时直接将插槽内容添加到相应位置

#### vue 组件更新之后如何获取最新 DOM

在修改数据后调用 this.$nextTick，首次加载在mounted函数里面调用this.$nextTick

#### vue 动态组件是什么

让多个组件使用同一个挂载点，并动态切换，这就是动态组件

```html
<template>
  <div class="home">
    <component :is="currentComponent"></component>
  </div>
</template>
<script>
  import Tab0 from "@/components/Tab0.vue";
  import Tab1 from "@/components/Tab1.vue";
  export default {
      data: () => {
          return {
              currentIndex: 0 // 通过改变currentIndex改变要挂载的组件名
          }
      },
      components: {
          "tab-0": Tab0,
          "tab-1": Tab1
      }
      currentComponent() { // 动态计算要挂载的组件的组件名
        return `tab-${this.currentIndex}`; // "tab-0" 、"tab-1"
      }
  }
</script>
```

#### vue 如何异步加载组件

什么时候用什么时候加载

```javascript
components:{
   abc：（）=> import(../../abc.vue)
}
```

#### vue 如何缓存组件

keep-alive

#### vue 组件如何抽离公共逻辑

mixin

#### vue 是如何监听数组变化的

vue 重写了数组的 push、splice、pop 等方法。

#### 虚拟 DOM diff 算法

虚拟 dom 相当于在 JS 和真实 dom 中间加了一个缓存，利用 diff 算法避免了没有必要的 dom 操作，从而提高性能。

#### vue 组件是如何渲染和更新的

vue 组件初次渲染过程

- 解析模板为 render 函数
- 触发响应式，监听 data 属性的 getter 和 setter
- 执行 render 函数， 生成 vnode，patch(elem,vnode)

vue 组件更新过程

- 修改 data， 触发 setter （此前在 getter 中已被监听）
- 重新执行 render 函数，生成 newVnode
- patch(vnode, newVnode)

#### v-for 为何使用 key

如果在 v-for 遍历中不加 key 值，vue 会采用“就地复用”。

#### 组件 data 为何是函数

组件中的 data 写成一个函数，数据以函数返回值形式定义，这样每复用一次组件，就会返回一份新的 data，类似于给每个组件实例创建一个私有的数据空间，让各个组件实例维护各自的数据。而单纯的写成对象形式，就使得所有组件实例共用了一份 data，就会造成一个变了全都会变的结果。

#### 何时使用 keep-alive

- 缓存组件，不需要重复渲染
- 优化性能

#### 何时需要使用 beforeDestroy

页面卸载需要清除的时间绑定 定时器 以及初始化数据等

#### 使用 this.obj={} 给 data 中新加入一个属性，这个数据是响应式的么？为什么？

不是响应式数据。

响应式对象和响应式数组是指在 vue 初始化时期，利用 Object.defineProperty()方法对其进行监听，这样在修改数据时会及时体现在页面上。

可以使用$set 方法

#### delete 和 Vue.delete 删除数组的区别

delete 只是被删除的元素变成了 empty/undefined 其他的元素的键值还是不变。

Vue.delete 直接删除了数组 改变了数组的键值。

#### 如何优化 SPA 应用的首屏加载速度慢的问题？

- 将公用的 JS 库通过 script 标签外部引入，减小 app.bundel 的大小，让浏览器并行下载资源文件，提高下载速度；
- 在配置 路由时，页面和组件使用懒加载的方式引入，进一步缩小 app.bundel 的体积，在调用某个组件时再加载对应的 js 文件；
- 加一个首屏 loading 图，提升用户体验；

#### 前端如何优化网站性能

- 减少 HTTP 请求数量
- CSS Sprites
- 合并 CSS 和 JS 文件
- 采用 lazyLoad
- 控制资源文件加载优先级
- 利用浏览器缓存
- 减少重排（Reflow）
- 减少 DOM 操作
- 图标使用 IconFont 替换

#### query 和 params 的区别

- query 要用 path 来引入，params 要用 name 来引入，
- 接收参数时，分别是 this.$route.query.name和this.$route.params.name（注意：是$route而不是$router）。
- query 更加类似于我们 ajax 中 get 传参，params 则类似于 post，前者在浏览器的地址栏中显示，params 不显示
- params 传值一刷新就没了，query 传值刷新还存在

#### SPA 单页面，有什么优缺点？

SPA（ single-page application ）仅在 Web 页面初始化时加载相应的 HTML、JavaScript 和 CSS。一旦页面加载完成，SPA 不会因为用户的操作而进行页面的重新加载或跳转；取而代之的是利用路由机制实现 HTML 内容的变换，UI 与用户的交互，避免页面的重新加载。

**优点：**

- 良好的交互体验

- 良好的前后端工作分离模式

- 减轻服务器压力

**缺点：**

- 首屏加载慢 解决方案：Vue-router 懒加载、使用 CDN 加速、异步加载组件、服务端渲染
- 不利于 SEO 解决方案：服务端渲染、页面预渲染、路由采用 h5 history 模式

#### 聊聊你对 Vue.js 的 template 编译的理解？

简而言之，就是先转化成 AST 树，再得到的 render 函数返回 VNode（Vue 的虚拟 DOM 节点）

#### 第一次页面加载会触发哪几个生命周期？

beforeCreate, created, beforeMount, mounted

#### 为什么会出现 vue 修改数据后页面没有刷新这个问题？如何解决？

如 Vue 不能检测通过数组索引直接修改一个数组项
数组改变后重新赋值 或着使用文档推荐的 vue 重写过的数组操作方法，或者 set
