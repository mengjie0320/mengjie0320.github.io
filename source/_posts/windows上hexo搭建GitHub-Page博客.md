---
title: windows上hexo搭建GitHub Page博客
date: 2019-01-25 09:44:59
tags: Github Page博客、hexo、git
---
#### 1. 分别下载并安装git、node.js、hexo
##### [git推荐下载地址](https://git-for-windows.github.io/)，下载之后按步骤安装即可；
##### [node.js推荐下载地址](https://nodejs.org/en/)，建议下载稳定版而不是最新版；
##### 安装hexo
###### 任意位置，鼠标右键，选择Git bash here，输入以下命令
`npm install hexo -g`
检查方法 `npm root -g`
#### 2. 安装好，开始创建本地hexo网页
##### 在合适的位置创建你的博客文件夹，自己起名即可。然后进入该文件夹，分别执行
```
	hexo init //初始化文件
	npm install //安装依赖包
	hexo g //生成静态文件 g => generate缩写
	hexo s //在本地预览 s => server缩写
```
##### hexo s执行完之后，会显示项目运行在哪个端口即可直接在浏览器访问，访问即可看到
![hexo home页](http://39.106.9.2/blogImg/2019-01-25hexo_homePage.jpg "hexo homePage")
#### 3. 部署博客
- ##### 先到github注册一个账号，建立一个repository
##### 你的博客名称是与你的用户名一致的，最好是提前想好自己的用户名。如果已经注册过了，相信你的用户名应该也有自己的意义。
##### 用来与博客相关的repository的名称必须要填写：“你的用户名”+“.github.io”。比如我的用户名是zhangsan，那么我的博客的repository的名称就是：zhangsan.github.io
- ##### 生成SSH密钥
##### git bash here输入`ssh-keygen -t rsa -C "你的邮箱地址"`，然后根据提示按三遍回车即可成功，在你的用户文件.ssh下会看到两个文件id_rsa密钥、id_rsa.pub公钥
- ##### 在GitHub中选择setting -> SSH and GPG keys -> 右上角的New SSH key，title随意配置，密钥黏贴公钥
![github密钥](http://39.106.9.2/blogImg/2019-01-25github_isa.png "github密钥")

- ##### 全局配置git账号信息
```
	git config --global user.name "你的github用户名"
	git config --global user.email "你的github注册邮箱"
```

+ ##### 配置本地文件
##### 打开你创建的博客根目录文件下的_config.yml
```
	deploy:
		type: git
		repo: https://github.com/user.name/user.name.github.io //user.name就是全局配置的github用户名，我的也就是https://github.com/zhangsan/zhangsan.github.io
		branch: master //这里的三行后面的空格都是必须的
```

+ ##### hexo部署
```
	hexo g //生成静态文件
	hexo d //deploy部署的意思，出现INFO Deploy done:git字样，表示成功，如果没有成功error字样，输入下一行
	npm install hexo-deployer-git --save //然后再g、d就可以了。如果还是失败，建议重新安装一次hexo
```

+ ##### 在浏览器输入你的新建仓库名即可看到与本地看到一致的hexo页面了
https://user.name.github.io 即 https://zhangsan.github.io

#### 4. 搭建好博客后编写并挂载：
##### 博客文件一般均在source_posts下，文件格式.md，也就是说用对程序员来说简单方便的markdown来编辑网页；一般引入图片的话，需要一个可以在网上访问到的地址，你可以有一些服务器管理，也可以上传到"七牛"（多人推荐）等在线管理的网站，然后加链接即可；
###### 编辑完，一般在本地预览调试之后，上传：
```
	hexo new "title" //新建文章，编辑完执行以下命令
	hexo clean //每次重新上传都需要clean一下
	hexo g //生成静态文件
	hexo s --debug //以debug模式启动，刷新即可看效果。
	// hexo s -p 5000 可以更改预览端口，一般用不到
	hexo d //部署
```

