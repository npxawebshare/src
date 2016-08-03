---
title: 开始在 hexo 上书写文章 
date: 2016-04-27 15:56:02
categories: 

- 教程
- hexo

tags:

- hexo

---


Welcome to [Hexo](https://hexo.io/)! This is your very first post. Check [documentation](https://hexo.io/docs/) for more info. If you get any problems when using Hexo, you can find the answer in [troubleshooting](https://hexo.io/docs/troubleshooting.html) or you can ask me on [GitHub](https://github.com/hexojs/hexo/issues).

## Quick Start

### Create a new post

``` bash
$ hexo new "My New Post"
```

More info: [Writing](https://hexo.io/docs/writing.html)

### Run server

``` bash
$ hexo server
```

More info: [Server](https://hexo.io/docs/server.html)

### Generate static files

``` bash
$ hexo generate
```

More info: [Generating](https://hexo.io/docs/generating.html)

### Deploy to remote sites

``` bash
$ hexo deploy
```

More info: [Deployment](https://hexo.io/docs/deployment.html)



## 问题

### 其他软件的4000端口占用问题

> hexo 有默认的端口号4000 一般不用修改，但是有时候跟系统端口号有冲突（目前发现的冲突软件就福昕阅读器一个，最好卸了），这就需要解决下：

	查看指定端口的进程
	netstat -ano|findstr 4000
	
	以进程编号查找程序
	tasklist|findstr 1640
	
	查看所有进程
	netstat -n|-a
	
	结束冲突的进程 启动你的hexo服务即可



### hexo 中创建md文件

命令行中输入（不需要后缀名）：

    $ hexo new "new article"

之后在source/_posts目录下面，多了一个new-article.md的文件。

打开之后我们会看到：
	
	=========================
	
	title: new article 
	
	date: 2016-04-25 11:10:33 
	
	tags: 
	
	=========================

文件的开头是属性，采用统一的`yaml`格式，用三条短横线分隔。下面是文章正文。

文章的正文支持markdown格式

新建、删除或修改文章后，不需要重启hexo server，刷新一下即可预览。

**文章可以拥有如下属性**：

	Setting Description Default
	
	layout    Layout    post或page    
	
	title    文章的标题    
	
	date    创建日期    文件的创建日期    
	
	updated    修改日期    文件的修改日期    
	
	comments    是否开启评论    true    
	
	tags    标签    
	
	categories    分类    
	
	permalink    url中的名字    文件名    

动态博客中通过发布文章页面设置的各种属性，在hexo里要这样设置。

**分类和标签**

例如：

	===========
	
	categories: 
	
	- 日记 
	
	tags: 
	
	- Hexo 
	
	- node.js
	
	===========

**摘要**
同wordpress一样，`<!--more-->`之上的内容为摘要。

**layout**
如果你修改了layout，在scaffolds文件夹里一定要有名字对应的模版文件，否则会采用默认模版。

**文件名**
在配置文件中的`new_post_name`项可以设置文件名，默认为:title，也就是你在命令行输入的名字。

文件名可以为下面几个变量和字符串常量的任意组合：

	Variable Description
	
	:title	Escaped title (lower case and replace spaces with dash)    
	
	:year	Created year (4-digit)    
	
	:month	Created month (2-digit)    
	
	:i_month	Created month (Without leading zeros)    
	
	:day	Created day (2-digit)    
	
	:i_day	Created day (Without leading zeros)    

草稿
草稿相当于很多博客都有的“私密文章”功能。

	$ hexo new draft "new draft"



会在source/_drafts目录下生成一个new-draft.md文件。但是这个文件不被显示在页面上，链接也访问不到。也就是说如果你想把某一篇文章移除显示，又不舍得删除，可以把它移动到_drafts目录之中。

如果你希望强行预览草稿，更改配置文件：

	render_drafts: true


或者，如下方式启动server：

	$ hexo server --drafts


下面这条命令可以把草稿变成文章，或者页面：


	$ hexo publish [layout] <filename>

---
### hexo命令大全

	$ hexo help
	Usage: hexo <command>
	
	Commands:
	  clean     Removed generated files and cache.
	  config    Get or set configurations.
	  deploy    Deploy your website.
	  generate  Generate static files.
	  help      Get help on a command.
	  init      Create a new Hexo folder.
	  list      List the information of the site
	  migrate   Migrate your site from other system to Hexo.
	  new       Create a new post.
	  publish   Moves a draft post from _drafts to _posts folder.
	  render    Render files with renderer plugins.
	  server    Start the server.
	  version   Display version information.
	
	Global Options:
	  --config  Specify config file instead of using _config.yml
	  --cwd     Specify the CWD
	  --debug   Display all verbose messages in the terminal
	  --draft   Display draft posts
	  --safe    Disable all plugins and scripts
	  --silent  Hide output on console
	
	For more help, you can use 'hexo help [command]' for the detailed information
	or you can check the docs: http://hexo.io/docs/


## 代码高亮

目前的办法是：在你的md文件主题内容前加上代码段，引入highlight插件帮助高亮显示（联网）

	<link href="http://cdn.bootcss.com/highlight.js/8.0/styles/monokai_sublime.min.css" rel="stylesheet">  
	<script src="http://cdn.bootcss.com/highlight.js/8.0/highlight.min.js"></script>  
	<script>
		hljs.initHighlightingOnLoad();
	</script> 

## 主题　

> [参考](http://www.jianshu.com/p/db7e64d86067)

### 主题库

- [wiki](https://github.com/hexojs/hexo/wiki/themes)
- [Hexo官方主题](https://hexo.io/themes/)

### 安装命令

	$ git clone <repository> themes/<theme-name>
	比如：$ git clone https://github.com/wuchong/jacman.git themes/jacman

然后就可以在hexo/theme下看到下载的主题文件夹

###　启用主题

修改主目录下配置文件`_config.yml`中的theme设置项，将其值设置为你下载的主题名称


## 文章中本地图片的配置

1. 在主目录配置文件中找到`post_asset_folder`配置项，其值改为`true`。
2. 编写md文件时，需要的文件放在文件同目录下的同名文件夹下，比如`_posts`文件夹下`hello.md`使用的图片全部放在`_posts`文件夹下新建的`hello`文件夹(`hexo new "hello"`命令之后会自动创建hello文件夹)下。
3. md书写直接时用`![图片说明](图片名称)`即可，不用写图片路径。
4. 其他资源使用方法类似



