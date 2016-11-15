## 关于Hybrid浅谈 ##

### 前言 ###
现在使用**HTML5**开发app好像慢慢成为了一种趋势，
其中比较主流的模式**Hybrid App** 和 **React Native**开发。

### 简介 ###
**Hybrid App** （混合模式移动应用）是介于**Web-App**  和 **React Native** 间的一种开发模式，兼具了**Native App** 良好的用户交互体验的优势和 **Web App** 跨平台开发的优势

**React Native** 是 **Facebook** 开源的框架，可以直接用 **Javascript** 开发原生的**APP**，并不使用WebView，这里就不详谈了。


### 分析 ###
**Hybrid App**优点：

-  效率高   -----------html5写界面的速度比native快多了
-  跨平台   -----------移动端只要使用WebView装载就OK了
-  低成本   -----------没有学习成本，不需要学习新语言，只需要前端和移动端

**Hybrid App**缺点：

- 体验比不上Native，甚至不如React Native。
- 只适合做重展示轻交互的功能。
- 依赖于WebView,而Android WebView的设计简直坑爹。

### 设计 ###
交互设计是Hybrid开发的重中之重，如果这块设计不好会让你后面痛不欲生。
  
- 交互接口 -----------NativeUI组件的调用，系统、设备等信息读取的接口。Native与Html5互调以及回调。
- 资源访问 -----------Native首先要考虑如何访问H5资源，做到既能以file的方式访问Native内部资源，又能使用url的方式访问线上资源;需要提供增量更新机制，摆脱APP迭代发版问题，避免用户升级。这里会涉及到静态资源在APP中的存放策略，更新策略的设计，需要服务器端的支持。
- 开发调试 -----------功能设计并没有完，如果WebView加载html交互出了问题，到底是Native的问题还是Html的问题，中间哪里出了bug。  

  
### Hybrid交互原理 ###
- App调H5 -----------将一组API绑定在WebView的window对象上，App通过原生方法调用window对象中的js方法
- H5调App -----------App实现对WebView URL的观察者模式，H5通过改变URL的哈希值使得App察觉并解析URL执行对应的操作。或者使用Android自带的方式，使用addJavascriptInterface方法提供一个对象给JS调用。

### 总结 ###
  
Hybrid开发或许不会成为主流，但绝对是提高效率、降低成本的选择。
  


### 感言 ###
这算是我第一篇正式的博文了，其实早就有写博客的想法，只是这种原因。。。。。。其实总结起来就是懒，啊啊啊！！！后面会坚持写下去的。
