---
title: CSS完成元素水平垂直居中
date: 2018-05-31 15:39:00
categories:
  - 前端开发	# 文章分类
tags:
  - CSS	# 文章标签
# sidebar: none # 默认启用右侧sidebar侧边栏，none：不启用
mathjax: true # markdown渲染引擎
# toc: true # 启用内容索引,搭配h1-h6使用右侧形成章节目录索引
---
<h3>
	要求：子元素和父元素宽高不确定，需要设置子元素水平垂直居中，效果如下图：
</h3>

![水平垂直效果图](center.png)

<h4>
	这里提供几种简单的实现方法：
</h4>

<h4>
	1.使用margin:auto属性实现【兼容IE7以上大部分浏览器】
</h4>

<p>
	首先这个元素和它的父元素都要设置定位，其中这个要水平垂直居中的元素需设置绝对定位absolute，
	然后再给它设置样式{left: 0;right: 0;top: 0;bottom: 0;margin:auto;}。这样便可以实现元素在父容器里垂直居中显示了。
</p>

``` 代码区
<style type="text/css">
.parent{
	/*子元素和父元素宽高随意，都可以实现水平垂直居中，这里随便设置了一个宽高撑开盒子容器体积，方便查看效果*/
	width: 600px;
	height: 500px;
	background: #222222;
	position: relative;
}
.child{
	width: 150px;
	height: 200px;
	background: goldenrod;
	position: absolute;
	left: 0;
	right: 0;
	top: 0;
	bottom: 0;
	margin: auto;
}
</style> 
```

<h4>
	2.使用transform属性实现【浏览器兼容性：Safari 3.1+、 Chrome 8+、Firefox 4+、Opera 10+、IE10+】
</h4>

<p>
	同上，设置好定位。然后添加样式{left: 50%;top: 50%;transform: translateX(-50%) translateY(-50%);}便好了。
	其中的translateX(-50%)表示将此元素在X轴上向左移50%元素宽度的距离，同理translateY(-50%)将元素在Y轴上向上移50%元素高度的距离。
</p>

``` 代码区
<style type="text/css">
.parent{
	/*子元素和父元素宽高随意，都可以实现水平垂直居中，这里随便设置了一个宽高撑开盒子容器体积，方便查看效果*/
	width: 600px;
	height: 500px;
	background: #222222;
	position: relative;
}
.child{
	width: 150px;
	height: 200px;
	background: goldenrod;
	position: absolute;
	left: 50%;
	top: 50%;
	transform: translateX(-50%) translateY(-50%);
}
</style> 
```

<h4>
	3.使用flex布局实现【浏览器兼容性：Safari 9+、 Chrome 29+、Firefox 28+、Opera 17+、IE10+】
</h4>

<p>
	首先给父元素设置flex布局{display: flex;}，然后父元素再设置align-items: center;
	可以使其包裹的子元素在水平方向上水平居中排列，
	再就是{justify-content: center;}属性规定了子元素在Y轴垂直方向上是居中排列。这样便实现了使用flex完成水平垂直居中的布局。
</p>

``` 代码区
<style type="text/css">
.parent{
	/*子元素和父元素宽高随意，都可以实现水平垂直居中，这里随便设置了一个宽高撑开盒子容器体积，方便查看效果*/
	width: 600px;
	height: 500px;
	background: #222222;
	display: flex;
	align-items: center;
	justify-content: center;
}
.child{
	width: 150px;
	height: 200px;
	background: goldenrod;
}
</style> 
```


------------------

<p style="font-size: 2rem;font-weight:600;text-align:center;">
	END
</p>