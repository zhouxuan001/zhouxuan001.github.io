---
title: 使用jQuery中hover事件时遇到的一个小问题
date: 2018-05-26 16:52:00
categories:
  - 前端开发	# 文章分类
tags:
  - jQuery	# 文章标签
# sidebar: none # 默认启用右侧sidebar侧边栏，none：不启用
mathjax: true # markdown渲染引擎
# toc: true # 启用内容索引,搭配h1-h6使用右侧形成章节目录索引
---
<p>
	在jQuery中有一个hover()方法，它可以实现模拟css中：hover这个伪类的效果。
</p>

<p>
	css伪类写法如下：
</p>

```
<style type="text/css">
	a:hover{  
	    color: #ccc;  
	}  
</style>
```

<p>
	jQuery中hover()方法如下 ：
</p>

```
<script type="text/javascript">
	$("a").hover(function(){  
	    $(this).css({"color":"#ccc"});  
	    console.log(1);  
	}) 
</script>
```

<p>
	如上所示，两种方法都可以完美的实现我们想要的效果。
</p>

<p>
	但是，在这其中其实还隐藏着一个很难发现的bug。
</p>

<p>
	如上，在hover()这个函数中，我们写了一个function方法，
	但是我们不知道的是，我们写在这个function中的代码其实一直都会被重复执行两次。
	它在鼠标移入的时候执行了一次，移出的时候又会执行一次(通过控制台查看可以看到我们代码中的console.log(1)中的1总共被输出了两次)。
</p>

<p>
	而我们的本意是只想让它在鼠标移入的时候执行我们的代码，这与我们想要的效果不一样，那么这到底是什么原因导致的呢？
</p>

<p>
	搜索官方jQuery文档中hover()方法的说明我们就会发现，其实这是jQuery中hover()内置方法的问题。
	jQuery中的hover()方法中一共封装有两个function函数，第一个是在移入时执行，
	第二个是在移出时执行的，而当我们像上面一样只写了一个function函数的时候，
	它就会默认这个function函数就是我们想让它在移入和移出时都被执行的函数，
	也就相当于将这个函数执行了两遍。
</p>

<p>
	当然，这个bug对于执行一些普通的效果是没什么影响的。
	但是，当触及到跟时间有关的一些动画效果（例如：jQuery中的animate()函数）的时候，
	就会出现问题。如下：
</p>

```
<script type="text/javascript">
	$(".box").hover(function(){  
	    var this_h=$(this).height()+50; 
	    $(this).animate({"height":this_h+"px"},1000);//每次高度在上一次数值的基础上用动画形式增加50 
	})  
</script>
```

<p>
	在上面的代码中，我们想要实现的效果是，当鼠标移入到class为box的这个元素的时候，我们先获取它的高度，
	再将这个高度数值增加50赋予一个变量this_h，
	然后用jQuery内置的animate()动画方法使这个元素1000毫秒内高度在原先的基础上增加50px。
	之后其它每次移入时都将box这个元素的高度在原先的基础上增加50，下次再移入，再增加50的高度。
	但是实际执行效果却是：一开始移入时，增加了50的高度，然后移出的时候，又增加了50高度，之后再次移入移出又陆续增加了100的高度。
</p>

<p>
	那这样的话明显不对啊，那么，怎么解决这个问题呢？
</p>

<p>
	很简单，我们在hover事件中写入两个function函数就好了，其中第一个是我们要让它在移入的时候执行的效果，
	第二个是让它在移出的时候执行的效果。像我们上面这种情况的话就可以在第二个函数里面什么都不写就好了，如下：
</p>

```
<script type="text/javascript">
	$(".box").hover(function(){  
	    var this_h=$(this).height()+50;
	    $(this).animate({"height":this_h+"px"},1000);//每次高度在上一次数值的基础上用动画形式增加50 
	},function(){  
	    //我是第二个函数，什么都不写的时候，在移出的时候hover方法什么都不会执行。  
	})  
</script>
```

<p>
	当然，像这些效果的话，其实也有很多别的方法可以完成的，
	比如我们也可以使用jQuery中的一些其他鼠标事件（例如：onmouseover、onmouseout、onmouseenter、onmouseleave等）来实现，
	没必要一味地使用hover()来进行事件的编写。
</p>



------------------

<p style="font-size: 2rem;font-weight:600;text-align:center;">
	END
</p>