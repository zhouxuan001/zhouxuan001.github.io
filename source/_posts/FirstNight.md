---
title: 今天创建了个人博客
sidebar: none # 默认启用右侧sidebar侧边栏，none：不启用
mathjax: true # markdown渲染引擎
# toc: true # 启用内容索引,搭配h1-h6使用右侧形成章节目录索引
---
 > 今天根据网上教程创建了属于自己的个人博客，在这期间遇到了一些问题。

 > 参考博客主题：https://blog.cofess.com/

## 执行**hexo -d**命令时报错

出现类似以下的报错代码：

``` bash
warning: LF will be replaced by CRLF in 2015/12/05/hello-world/index.html.
The file will have its original line endings in your working directory.
...
```

此问题的解决方法是：修改根目录下的配置文件_config.yml，修改deploy节点。

原来的配置为：

``` bash
deploy:
  type: git
  repo: https://github.com/{myname}/{myname}.github.io.git
  branch: master
```

将其修改成如下：

``` bash
deploy:
  type: git
  repo: https://{myname}：{mypassword}@github.com/{myname}/{myname}.github.io.git
  branch: master
```

如此，便解决了执行**hexo -d**命令时报错的问题。

## 每次写完博客后需要执行 $ hexo clean && hexo g && hexo d 命令上传。

不要执行  hexo clean && hexo g 会清除一些自己创建在 public 目录下的文件(自己添加的grace主题的about模块)。
每次修改和上传新博客时，执行 hexo d 命令就行了。

## 博客文件地址在 source/_posts/目录下。

## 网络博客主题模板：

### 更换模板方法(例：更换 grace 模板)

``` bash
$ git clone https://github.com/buhuo00/hexo-theme-grace themes/grace
```

再到_config.yml配置文件中修改模板参数theme为  theme： grace

------------------

<p style="font-size: 2rem;text-align:center;">
	END
</p>