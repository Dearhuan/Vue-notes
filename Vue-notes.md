## 11月14号上午面试(数字广东)：
##### 1.尽可能多的说一下元素水平垂直居中的方式。
水平垂直居中效果图如下
![54491b281f58bf2fe470d0a5b2f15163.png](en-resource://database/3070:1)

方法一：position 定位（适用于子盒子有宽度和高度的时候）![927dd2b45f9cd2b921d92c0acd048685.png](en-resource://database/3072:1)
方法二：position + transform（子盒子有或没有宽高的时候都适用）![64fdf80b8b03cb196d03956ce4e5d339.png](en-resource://database/3074:1)
方法三：flex 布局（子盒子有或没有宽高的时候都适用）![af4bdec9fd21fa5a77e23cf252632796.png](en-resource://database/3076:1)

方法四：margin：auto；实现绝对定位元素的水平方向居中
![d209a1a94914ccdfe113a751f57c6d91.png](en-resource://database/3078:1)
##### 2.display:none和 visibility:  hidden和opacity区别，对事件的响应是怎样00000000000000的
（1）是否占据空间.

display:none 不再占据空间，会引起重排和重绘
visibility:hidden 占据空间，仅引起重绘
opacity:0 占据空间，引起重绘
（2）是否可以被继承

display:none 不会被子元素继承，但是子元素不会显示
visibility:hidden 会被子元素继承，子元素可以设置visibility:visible来进行反隐藏
opacity:0 会被子元素继承，但子元素不能通过opacity:1来进行反隐藏
（3）transition属性是否有效

display:none 完全不受transition属性的影响，元素立即消失
visibility:hidden 元素消失的时间跟transition属性设置的时间一样，但是没有动画效果
opacity:0 能够进行正常的动画效果
（4）对事件的响应

display:none 由于元素消失，不能触发如click等事件，但可以通过js触发设置了display:none的元素的事件
visibility:hidden 由于元素隐藏了，也不能触发click等事件
opacity:0 可以触发事件，元素只是看不见而已。
##### 3.原型和原型链
[重新认识构造函数、原型和原型链](
https://juejin.im/post/5c6a9c10f265da2db87b98f3)
每个对象拥有一个原型对象，通过 __proto__ 指针指向上一个原型 ，并从中继承方法和属性，同时原型对象也可能拥有原型，这样一层一层，最终指向 null。这种关系被称为原型链 (prototype chain)，通过原型链一个对象会拥有定义在其他对象中的属性和方法。

##### 4.构造函数和实例对象通过什么进行联系
实例对象和构造函数之间的关系:
​    * 1. 实例对象是通过构造函数来创建的---创建的过程叫实例化
​    * 2.如何判断对象是不是这个数据类型?
​    *  1) 通过构造器的方式 实例对象.构造器==构造函数名字
​    *  2) 对象 instanceof 构造函数名字
​    *  尽可能的使用第二种方式来识别
##### 5.CSS3里的变量怎么用的
[CSS/CSS3中的原生变量var详解](
https://www.cnblogs.com/moqiutao/p/7735124.html)
##### 6.你知道的跨域？为什么设置CORS能让客户端访问服务器
Jsonp和CORS
[说说AJAX（同源策略与CORS跨域）](
https://www.jianshu.com/p/f41457aa19a2)

##### 7.webpack的使用情况，原理
##### 8.babel的使用情况，为什么使用babel后在ie中任然运行异常
##### 9.你知道的网页安全问题有哪些
##### 10.用过babel-polyfill没有
webpack.base.conf.js文件中发现了一个babel-loader的配置，原因是我static下的js文件中用了ES6的语法，但是默认没有配置babel-loader来处理static下的文件，所以导致IE前端报错，页面无法加载
##### 11.SetTimeout和Promise的执行顺序
setTimeout,ajax属于宏任务，promise,async,await属于微任务
promise较定时器有限执行
[JS异步--async,await,promise,setTimeout 执行顺序](
https://juejin.im/post/5d7e0e136fb9a06b2262e415)
##### 12.对event loop的理解，宏任务和微任务
先同步后异步，先微任务后宏任务。
promise前部分属于同步，then后面是异步微任务
##### 13.说一下BFC
##### 14.css样式优先级，选择器权重问题
##### 15.Vuex的问题，mutations和actions
##### 16.页面缓存的问题
##### 17.使用Vue遇到过哪些坑？
##### 18.有没有使用过mixin（混入）？
[Vue之混入(mixin)与全局混入](https://www.cnblogs.com/fengyuexuan/p/10918011.html)
官方文档：混入提供了一种非常灵活的方式，来分发 Vue 组件中的可复用功能。一个混入对象可以包含任意组件选项。当组件使用混入对象时，所有混入对象的选项将被“混合”进入该组件本身的选项。

个人理解：混入就是用来对vue组件中的公共部分，包括数据对象、钩子函数、方法等所有选项，进行提取封装，以达到代码的复用。
##### 19.你平常通过哪些途径学习新技术？
掘金、博客园、github、知乎
##### 20.你还有什么要问的？
近期的项目情况、前后端对接情况、人员配比、使用的技术栈、产品涉及的主要方向