## 移动端APP遇到的部分问题：

1.打包APP后，启动后出现白屏的情况。

解决方式：

1.首先检查路由模式，将history去掉或者替换为hash路由，因为history路由模式作为h5新出的API，兼容性还不是很好。2.修改项目下的config/index.js/build中的assetsPublicPath，将'/'改成'./'

2.点击手机返回键出现直接退出APP的情况。

定义一份appback.js文件，在main.js引入并重新打包。

3.移动端click事件的300ms延迟问题。

引入fastclick库来解决，在全局main.js引入并引用这个方法。

4.iOS的日期格式问题，在iOS上无法正常显示2019-09-09，会显示NAN。

解决方法：在处理日期之前转换为2019/09/09的格式

5.iPhone X等机型底部指示条与部分操作页面重合，容易造成误操作。

解决方法：

Vant 中部分组件提供了`safe-area-inset-bottom`属性，设置该属性后，即可在对应的机型上开启适配

<!-- 在 head 标签中添加 meta 标签，并设置 viewport-fit=cover 值 -->

<meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, minimum-scale=1.0, viewport-fit=cover">
<!-- 开启 safe-area-inset-bottom 属性 -->
<van-number-keyboard safe-area-inset-bottom />

![alt text](https://b.yzcdn.cn/vant/safearea.png)