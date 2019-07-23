---
title: 关于一些动态创建的节点无法绑定事件的问题
date: 2018-05-25 10:02:09
categories:
  - 前端开发	# 文章分类
tags:
  - JS	# 文章标签
# sidebar: none # 默认启用右侧sidebar侧边栏，none：不启用
mathjax: true # markdown渲染引擎
# toc: true # 启用内容索引,搭配h1-h6使用右侧形成章节目录索引
---
<h4 style="text-indent: 2em;">
	在我们HTML页面中有时候一些DOM元素节点（例如：一些页面加载的新闻公告列表[如下图]）是需要通过AJAX请求接口数据动态创建的，
	而当我们想在JS中想为这些节点绑定事件（如：click,hover...等）时便会出现无法绑定的情况，使用window.onload方法在页面加载后才执行也不行。
</h4>

![新闻公告列表图片](new_list.png)

#### 解决办法：

<p>
	使用JQ提供的.on()和.delegate()方法可以解决解决此问题，给动态加载的元素成功绑定上事件，但是在这两种方法的参数中一定得写上我们需要绑定事件的那个元素选择器。
</p>

 > <p style="font-size: 1.8rem;">如:$("#parent").on("click",".list",function(){ }) 和  $("#parent").delegate("click",".list",function(){ }) 。</p>
 
<p>
	这两种方法内的参数 .list 就是我们动态加载出来需要绑定事件的那个元素，前面的 #parent 是 .list 元素的父元素。
</p>

``` javascript代码引用
//javascript 代码
//.list为新闻里的每一条公告，是我们动态创建的;#parent是一个包裹着里的这一行行公告的一个div。
//一般来说，我们绑定事件的写法都是用下面的第一和第二种写法。但是这种写法是绑定不上的。
$('#parent .list').click(function(){//1.直接使用click(fn)方法绑定不上
    console.log($(this).html());
})
$('#parent .list').on('click',function(){//2.使用on("click",fn)方法还是绑定不上
    console.log($(this).html());
})
$('#parent').on('click','.list',function(){//3.此种写法可以成功绑定
    //使用on("click","...",fn),在on里面增加一个参数（需要绑定的那个节点），同时前面调用.on方法的元素改为该节点的父元素即：$('#parent')
    console.log($(this).html());
})
$('#parent').delegate('click','.list',function(){//4.此种写法可以成功绑定
    //使用delegate("click","...",fn),在delegate里面增加一个参数（需要绑定的那个节点），同时前面调用.delegate方法的元素改为该节点的父元素即：$('#parent')
    console.log($(this).html());
})
```

------------------

<p style="font-size: 2rem;font-weight:600;text-align:center;">
	END
</p>