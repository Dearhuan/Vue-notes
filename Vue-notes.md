#### 1.在使用计算属性的时，函数名和data数据源中的数据可以同名吗？
不能同名 因为不管是计算属性还是data还是props 都会被挂载在vm实例上，因此 这三个都不能同名

#### 2.你知道v-model的原理吗？说说看

原生input其实只是一个语法糖，:bind="value"与@change="value = $event.target.value"的结合。自定义组件的时候的v-model默认监听change事件和绑定value 的prop。


#### 3.怎么给vue定义全局的方法？
第一种：挂载到Vue的prototype上。把全局方法写到一个文件里面，然后for循环挂载到Vue的prototype上，缺点是调用这个方法的时候没有提示 
```
Object.keys(tools).forEach(key => {
      Vue.prototype[key] = tools[key]
 })
```
第二种：利用全局混入mixin，因为mixin里面的methods会和创建的每个单文件组件合并。这样做的优点是调用这个方法的时候有提示Vue.mixin(mixin)
```
new Vue({
    store,
    router,
    render: h => h(App),
}).$mount('#app')

import tools from "./tools"
import filters from "./filters"
import Config from '../config'
import CONSTANT from './const_var'

export default {
    data() {
        return {
            CONFIG: Config,
            CONSTANT: CONSTANT
        }
    },
    methods: {
        // //将tools里面的方法挂载到vue上,以方便调用，直接this.$xxx方法名就可以了
        // Object.keys(tools).forEach(key => {
        //     Vue.prototype[key] = tools[key]
        // })
        //将tools里面的方法用对象展开符混入到mixin上,以方便调用，直接this.$xxx方法名就可以了
        ...tools
    },
    filters: {
        // //将filter里面的方法添加了vue的筛选器上
        // Object.keys(filters).forEach(key => {
        //     Vue.filter(key, filters[key])
        // })
        ...filters
    }
}
```
#### 4.怎么解决vue动态设置img的src不生效的问题？

因为动态添加src被当做静态资源处理了，没有进行编译，所以要加上require。
#### 5.使用vue后怎么针对搜索引擎做SEO优化？

ssr,即单页面后台渲染
vue-meta-info 与prerender-spa-plugin 预渲染
nuxt
phantomjs

#### 6.跟keep-alive有关的生命周期是哪些？描述下这些生命周期

activated和deactivatedkeep-alive的生命周期
1.activated： 页面第一次进入的时候，钩子触发的顺序是created->mounted->activated
2.deactivated: 页面退出的时候会触发deactivated，当再次前进或者后退的时候只触发activated
#### 7.你知道vue2.0兼容IE哪个版本以上吗？

不兼容ie8及以下是因为vue的响应式原理是基于es5的Object.defineProperty的,而这个方法不支持ie8及以下
#### 8.你是从vue哪个版本开始用的？你知道1.x和2.x有什么区别吗？

像1.0与2.0，我只知道一点-。-1、 2.0生命生命周期变化感觉变得更加语义化一点（有规律可寻，更好记了），而且增加了beforeUpdate、updated、activated、deactivated，删除了attached、detached。2、2.0将1.0所有自带的过滤器都删除了，也就是说，在2.0中，要使用过滤器，则需要我们自己编写，以下是一个自定义过滤器示例,Vue.filter('toDou',function(n,a,b){return n<10?n+a+b:''+n;});
#### 9.你知道vue中key的原理吗？

作用的话，便于diff算法的更新，key的唯一性，能让算法更快的找到需要更新的dom，需要注意的是，key要唯一，不然会出现很隐蔽性的更新问题。
#### 10.你知道style加scoped属性的用途和原理吗？

用途：防止全局同名CSS污染原理：在标签加上v-data-something属性，再在选择器时加上对应[v-data-something]，即CSS带属性选择器，以此完成类似作用域的选择方式
#### 11.你有使用过babel-polyfill模块吗？主要是用来做什么的？

ES6的转码。IE的兼容。
babel默认只转换语法,而不转换新的API,如需使用新的API,还需要使用对应的转换插件或者polyfill去模拟这些新特性。
#### 12.在.vue文件中style是必须的吗？那script是必须的吗？为什么？

在.vue文件中，我们可以没有style，但是必须要有script来利用 exports default 来导出模块，否则就会出错。
#### 13.说说你对provide和inject的理解

通过在父组件中provide一些数据然后再所有子组件中都可以通过inject获取使用该参数,主要是为了解决一些循环组件比如tree, menu, list等, 传参困难, 并且难以管理的问题, 主要用于组件封装, 常见于一些ui组件库
#### 14.ajax、fetch、axios这三都有什么区别？

1.ajax是最早出现发送后端请求的技术，属于原生js范畴,核心是使用XMLHttpRequest对象,使用较多并有先后顺序的话，容易产生回调地狱。2.fetch号称可以代替ajax的技术，是基于es6中的Promise对象设计的，参数和jQuery中的ajax类似，它并不是对ajax进一步封装，它属于原生js范畴。没有使用XMLHttpRequest对象。
3.axios不是原生js,使用时需要对其进行安装，客户端和服务器端都可以使用，可以在请求和相应阶段进行拦截，基于promise对象。
#### 15.vue首页白屏是什么问题引起的？如何解决呢？

1.打包后文件引用路径不对，导致找不到文件报错白屏
在config文件夹中找到index.js打开把assetsPublicPath: '/'改成assetsPublicPath: './'
2.路由模式mode设置影响
把h5的history路由模式改成hash


#### 16.说说你对单向数据流和双向数据流的理解
单向数据流：所有状态的改变可记录、可跟踪，源头易追溯；所有数据只有一份，组件数据只有唯一的入口和出口，使得程序更直观更容易理解，有利于应用的可维护性；一旦数据变化，就去更新页面(data-页面)，但是没有(页面-data)；如果用户在页面上做了变动，那么就手动收集起来(双向是自动)，合并到原有的数据中。
双向数据流：无论数据改变，或是用户操作，都能带来互相的变动，自动更新。
#### 17.说说你对SPA单页面的理解，它的优缺点分别是什么？

介绍：SPA应用就是一个web应用，可理解为：是一种只需要将单个页面加载到服务器之中的web应用程序。当浏览器向服务器发出第一个请求时，服务器会返回一个index.html文件，它所需的js，css等会在显示时统一加载，部分页面需要时加载。
优点：1.良好的交互式体验。意思是：用户无需刷新页面，获取数据通过异步ajax获取，页面显示流畅2.良好的前后端分离模式（MVVM），减轻服务端压力。服务器只需要输出数据就可以，不用管逻辑和页面展示，吞吐能力会提高几倍3.共用同一套后端程序代码，不用修改就可用于web界面，手机和平板等客户端设备
缺点：1.不利于SEO优化2.由于单页应用在一个页面中显示，所以不可以使用浏览器自带的前进后退功能，想要实现页面切换需要自己进行管理3.首屏加载过慢（初次加载耗时多），原因是：为了实现单页web应用功能及展示效果，在页面初始化的时候就会将js，css等统一加载，部分页面在需要时加载。当然也有解决方法。
解决方法：①使用路由懒加载 ②开启Gzip压缩 ③使用webpack的externals属性把不需要的库文件分离出去，减少打包后文件的大小 ④使用vue的服务端渲染（SSR）举例spa应用：网易云音乐、QQ音乐等

#### 18.第一次加载页面时会触发哪几个钩子？

beforeCreate, created, beforeMount, mounted


#### 19.什么是双向绑定？原理是什么？
双向数据绑定个人理解就是存在data→view,view→data两条数据流的模式。其实可以简单的理解为change和bind的结合。目前双向数据绑定都是基于Object.defineProperty()重新定义get和set方法实现的。修改触发set方法赋值，获取触发get方法取值，并通过数据劫持发布信息.


#### 20.vuex中actions和mutations有什么区别？
mutations可以直接修改state，但只能包含同步操作，同时，只能通过提交commit调用(尽量通过Action或mapMutation调用而非直接在组件中通过this.$store.commit()提交)actions是用来触发mutations的，它无法直接改变state，它可以包含异步操作，它只能通过store.dispatch触发

#### 21.vue组件之间的通信都有哪些？

父子Coms: props,$emit/$on,($parent/$children)/$refs
兄弟Coms: Vuex,Bus
跨级Coms: Vuex,Bus,(provide/inject),($attrs/$listeners)
#### 22.vue-router有哪几种导航钩子（ 导航守卫 ）？

三种导航钩子：
1.全局导航钩子：router.beforeEach(to,from,next) 作用：跳转前进行判断拦截
2.组件内的钩子
3.单独路由独享组件


#### 23.如何获取路由传过来的参数？
[vue-router query和params传参(接收参数)，$router、$route的区别](
https://www.cnblogs.com/zhangruiqi/p/9412539.html)
如果使用query方式传入的参数使用this.$route.query 接收
如果使用params方式传入的参数使用this.$route.params接收


#### 24.Vue怎样实现路由懒加载？
```
//使用箭头函数动态import相应的组件
component: () => import( '../views/mine.vue')
```
#### 25.route和router有什么区别？
route代表当前路由对象，router代表整个vue实例下的路由对象
#### 26.异步执行的运行机制

（1）所有同步任务都在主线程上执行，形成一个执行栈（execution context stack）。
（2）主线程之外，还存在一个"任务队列"（task queue）。只要异步任务有了运行结果，就在"任务队列"之中放置一个事件。
（3）一旦"执行栈"中的所有同步任务执行完毕，系统就会读取"任务队列"，看看里面有哪些事件。那些对应的异步任务，于是结束等待状态，进入执行栈，开始执行。
（4）主线程不断重复上面的第三步。
#### 27.vue中的nextTick

应用场景：需要在视图更新之后，基于新的视图进行操作。

需要注意的是，在 created 和 mounted 阶段，如果需要操作渲染后的试图，也要使用 nextTick 方法。

#### 28.[vue项目前端限制页面长时间未操作超时退出到登录页](https://www.cnblogs.com/steamed-twisted-roll/p/11851658.html)