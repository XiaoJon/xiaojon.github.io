---
layout: post
title:  "Hybrid实现"
date:   2016-11-16 13:54:56 +0800
categories: jekyll update
---

> **前言**

在上一篇文章[Hybrid浅谈](http://www.jianshu.com/p/602906ca660c)中介绍了Hybrid开发的一些原理和看法，这篇文章就介绍下Hybrid开发的关键点。

> **分析**

交互接口 -------可以使用官方提供的JavascriptInterface接口，但是只能提供简单的交互操作，如果涉及的回调就无能为力了。

资源访问 -------原始的方法是通过URL访问html界面，但这有一个致命的地方，一旦网络不稳定，用户体验糟糕的想让人报警。

> **实现**

* **交互接口**

	可以使用JsBridge交互框架来处理复杂的交互，其原理就是Native和js约定通讯协议，相互注册对方想要调用的方法进行调用。[开源地址](https://github.com/lzyzsd/JsBridge)

	**native注册函数**
	![](http://i.imgur.com/yeKhaci.png)
	
	**js调用native注册的函数**
	![](http://i.imgur.com/nklYMMo.png)

	二者通过js桥进行连接，js桥的原理下篇文章在分析

* **资源访问**

	html界面肯定不能使用URL进行网络访问，必须是在本地。当APP启动时，APP会读取版本信息，当发现本地版本号比线上小，便会下载对应的zip文件，然后解压之并且替换整个资源文件夹。(这里可以做增量更新，需要维护版本库)

	重写WebViewClient的shouldInterceptRequest方法，加载html、css、js等资源文件时会被调用。我们对url进行判断在本地是否有对应的资源，如果有就使用本地的，没有就从网络请求再保存在本地显示。（这里需要定义好资源文件目录）

> **总结**

写**Hybrid App**最好要懂js，不然js和Native调用有问题时都不知道怎么调试。最重要的一点，一定要注意内存的控制，不然在垃圾的手机上随时会蹦。
