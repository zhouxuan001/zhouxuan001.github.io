---
title: HTML里的数据存储分析
date: 2018-05-25 13:53:52
categories:
  - 前端开发	# 文章分类
tags:
  - JS	# 文章标签
# sidebar: none # 默认启用右侧sidebar侧边栏，none：不启用
mathjax: true # markdown渲染引擎
# toc: true # 启用内容索引,搭配h1-h6使用右侧形成章节目录索引
---
<h4 style="margin-bottom:0px;">
	在前端开发工作中，常用的数据存储有三种，分别是cookie，localStorage和sessionStorage。
	其中，cookie是存储在浏览器的一段文本，而localStorage和sessionStorage则是HTML5中所提供的本地存储。
</h4>

<h4 style="margin-top:0px;">
	那么，这几种数据存储方式之间有什么区别呢？让我们来了解一下。
</h4>

<h4>
	1.cookie
</h4>

<p>
	cookie是什么?cookie就是一段文本，它存储在客户端（通常来说是浏览器），目前为各大主流浏览器存储数据所用。
	一般来说用其存储的数据有比如：名字、密码、日期...等信息。cookie存储的数据能在客户端上保留相当长的时间。
</p>

<p>
	<b>分析：</b>用cookie存储的数据有大小限制，一般不可超过4096 个字节(4kb)，而且cookie的安全系数不高，有被篡改的风险。
	不过其好处是几乎支持所有浏览器。
</p>

<h4>
	2.localStorage 和 sessionStorage
</h4>

<div class="passages"><!--passages：段落专用div类标签-->
<p>
	localStorage和sessionStorage是HTML5 提供的两种在客户端存储数据的新方法。
	主要目的是为了克服由cookie所带来的一些限制，当数据需要被严格控制在客户端时，不需要持续的将数据发回服务器。
	同时它们能够存储的数据大小一般都是：5MB，可以在不影响网站性能的前提下将大量数据存储于本地。
</p>

<p>
	localStorage是本地存储，它的生命周期是永久的，关闭页面或浏览器之后localStorage中的数据也不会消失。除非主动删除数据，否则数据永远不会消失。
</p>

<p>
	sessionStorage是会话存储，它是针对一个session(会话) 进行数据存储，它的生命周期仅在当前会话下有效。当用户关闭浏览器窗口后，数据将会被实时删除。
</p>
</div>


<p>
	<b>分析：</b>localStorage和sessionStorage的存储空间更大；
	数据不会传送到服务器，减少了客户端和服务器端的交互，节省了网络流量；
	同时数据不发送到服务器端，不会担心数据被截获，安全性相对于cookie更高一些。
</p>



------------------

<p style="font-size: 2rem;font-weight:600;text-align:center;">
	END
</p>