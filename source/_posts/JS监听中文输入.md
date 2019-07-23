---
title: JS监听中文输入
date: 2018-05-25 11:28:47
categories:
  - 前端开发	# 文章分类
tags:
  - JS	# 文章标签
# sidebar: none # 默认启用右侧sidebar侧边栏，none：不启用
mathjax: true # markdown渲染引擎
# toc: true # 启用内容索引,搭配h1-h6使用右侧形成章节目录索引
---
<h4 style="text-indent: 2em;">
	当时是在做
	<a href="https://wesbos.com/" target="_blank">Wes Bos</a>的
	<a href="https://javascript30.com/" target="_blank">javascript30</a>的一个
	<span style="color:#333333;background-color:rgb(255,255,255);">挑战</span>。
	在做第六个项目（根据输入框实时调用AJAX古诗匹配）时，当我们输入中文拼音，还在拼音字符状态未选择成中文时，一直在执行我编写的事件监听处理函数（当输入框里的值有变化时执行此函数，
	<strong>调用AJAX在页面显示数据里包含这些字的古诗</strong>）。
	而我想要的是在我们输入拼音未完成中文选择时，不让其执行我们的监听处理函数，
	只有选择完中文后才去执行调用AJAX<strong>判断有没有包含输入的这些字的古诗。
</h4>

<br/>

<p style="color: #ff6600;">
	古诗匹配项目效果图如下：
</p>

<br/>

![古诗词输入搜索匹配](20180518131816676.jpg)

<br/>

<p style="color: #ff6600;">
	此问题解决方法如下：
</p>

<br/>

``` HTML代码片段
<!--HTML代码片段-->
<input type="text" id="this_input" placeholder="中文输入未完成时不执行事件" />  
<script src="http://code.jquery.com/jquery-1.8.3.min.js" type="text/javascript" charset="utf-8"></script>  
<script type="text/javascript">  
        $('#this_input').on('input propertychange', function () {//input propertychange 当输入框里的值有变化时执行此函数  
            if ($(this).prop('cnStart')) return;//如果正在执行中文输入时，此值为true，执行return=>下面代码不执行  
            console.log('当前输入：' + $(this).val());  
            //此处执行AJAX请求判断请求的数据中有没有包含输入的这些字的古诗  
            //如果有，就将所有包含这些字的诗排列出来  
        }).on('compositionstart', function () {//compositionstart 当输入框有非直接的文字输入时触发(如：输入拼音在待选状态时)  
            $(this).prop('cnStart', true);  
            console.log('正在中文输入');//将 cnStart 变为 true，此处执行完后会跳到  
        }).on('compositionend', function () {//compositionend 当输入框有直接的文字输入时触发(如：输入拼音后完成了中文选择时)  
            $(this).prop('cnStart', false);  
            console.log('完成中文输入');  
        });  
</script>
```

<p>
	当我们开始进行input的输入改变了input框里的值时，js会监听到input propertychange事件，
	执行判断(一开始时$(this).prop('cnStart')的值我们没有定义，为undefined，
	在监听了compositionstart和compositionend事件后会相应变为true和false，非true时不会进行return)，
	再输出文本，接下来此时会执行此函数中其它的一些操作(AJAX请求...)。
</p>

<p>
	而当我们输入框输入的文字还在待选状态时（如：输入拼音未选择完成时），便会触发compositionstart事件，
	此时我们通过jquery的prop()方法给这个input元素添加自定义属性（cnStart：自定义名称，表示中文输入开始）和值（true），执行输出语句。
	此时执行完compositionstart事件后，因为输入框内文字有发生变化，会再去调用上面的input propertychange事件=>进行判断，
	此时$(this).prop('cnStart')的值为true，会执行return语句，因此便会截断下面的所有操作，使其不会去执行。
</p>

<p>
	而当我们输入框输入的文字不在待选状态后（如：输入拼音后完成了中文选择时），便会触发compositionend事件，
	此时我们再将cnStart这个自定义属性设置为false，代表我们已经完成了中文输入，执行输出语句。此时执行完了compositionend事件，
	同上会再去调用input propertychange事件=>进行判断，此时$(this).prop('cnStart')的值为false，
	不会执行return语句，那么接下来才会顺利执行我们此函数中的一系列操作。
</p>



------------------

<p style="font-size: 2rem;font-weight:600;text-align:center;">
	END
</p>