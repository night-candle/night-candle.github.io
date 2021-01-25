---
title: 基于Hexo的GitHub博客搭建
top: true
cover: false
toc: true
mathjax: true
date: 2020-08-28 17:24:54
password:
summary: 文本是使用Hexo框架和GitHub pages服务搭建简单个人博客的教程
tags:
- 前端
- Hexo
categories:
- 教程
typora-copy-images-to: GitHub-blog-for-Hexo
---


## 0.前言

**Github Pages**

Github Pages允许用户的任何一个Repo的gh-pages分支上的代码可以经由HTTP访问到，类似提供了静态文件服务。不仅可以方便的为项目建立介绍站点，也可以用来建立个人博客。

- 优点：

1. 轻量级的博客系统，没有麻烦的配置
2. 无需自己搭建服务器
3. 博客内容可以轻松打包、转移、发布到其它平台；
4. 可以绑定自己的域名

- 缺点：

1. 使用[Jekyll](https://github.com/mojombo/jekyll)模板系统，相当于静态页发布，适合博客，文档介绍等，动态程序的部分受限
2. 基于Git，很多东西需要动手，不像Wordpress有强大的后台



**Hexo**

Hexo是一款基于Node.js的高效静态站点生成框架，可以通过Hexo直接使用Markdown语法来撰写博客而无需关心网页源代码的具体细节，只需要用心写好你的博客内容就好了。



- 快速开始

``` cmd
$ hexo s				# 本地预览博客
$ hexo g		  		# 生成博客网页文件
$ hexo d				# 上传网页文件到github
$ hexo new post "article title"
```

参考材料：

[Hexo-Github地址](https://github.com/hexojs/hexo)

[Hexo帮助文档](https://hexo.io/zh-cn/docs/)



## 1.环境准备

### 1.1 安装Node.js

[Node.js下载地址](https://nodejs.org/dist/v9.11.1/node-v9.11.1-x64.msi)

- 安装了Node.js会自动安装npm

- cmd窗口输入`node -v`和`npm -v`验证是否安装成功

- 可以使用阿里的国内镜像进行加速

  ```bash
  npm config set registry https://registry.npm.taobao.org
  ```

### 1.2 安装Git

为了把本地的网页文件上传到github上面去，我们需要用到分布式版本控制工具

[Git下载地址](https://git-scm.com/download/win)

- 为了把本地的网页文件上传到github上面去，我们需要用到分布式版本控制工具Git
- 最后一步添加路径时选择Use Git from the Windows Command Prompt，这样能直接在命令提示符里打开
- 安装完成后在命令提示符中输入git --version验证是否安装成功

### 1.3 安装Hexo

- cmd窗口输入`npm install -g hexo` 
- 安装完后输入hexo -v验证是否安装成功



## 2.本地部署Hexo

### 2.1 初始化目录

在想创建的目录下执行`hexo init`，这个命令会初始化博客的目录

<img src="clip_image002.gif" alt="博客根目录" style="zoom:80%;" />

### 2.2 全局配置

在根目录`_config.yml`里进行全局配置

### 2.3 本地启动

```bash
hexo g #生成本地public静态文件

hexo s #启动本地服务器
```

​	进入http://localhost:4000/ 已经可以看到一篇helleworld的博客



## 3.个性化主题

### 3.1 推荐主题

https://github.com/litten/hexo-theme-yilia（一个简洁优雅的主题）

https://github.com/TryGhost/Casper（幽灵主题）

https://github.com/blinkfox/hexo-theme-matery（炫酷，响应式更友好）

### 3.2 使用步骤

1. 安装主题

   在根目录下`git clone`你喜欢的主题的代码

	```bash
	hexo clean
	git clone https://github.com/litten/hexo-theme-yilia.git
	```
	
2. 启用主题

   修改根目录的`_config.yml`配置文件中的theme属性，将其设置为yilia（默认是landscape）<img src="image-20200828183406777.png" style="zoom:80%;" />

3. 本地启动

   ```bash
   hexo g
   hexo s
   ```



## 4.部署到GitHub

### 4.1 创建远程仓库

1. GitHub新建一个仓库,仓库名为	`用户名.github.io`

   **名称一定要和github用户名完全一样，比如你github用户名叫`abc`，那么仓库名为`abc.github.io`。**

2. 修改根目录下的`_config.yml`配置文件

   url：GitHub Pages网址`https://GitHub用户名.github.io`



### 4.2 连接Github与本地

1. 右键打开git bash，输入命令：

   ```bash
   git config --global user.name "" #用户名和邮箱根据注册github的信息修改
   git config --global user.email ""
   ```

2. 生成密钥SSH key：

   ```bash
   ssh-keygen -t rsa -C ""
   ```

​	将生成的公钥添加到github中（头像下面点击`settings`，再点击`SSH and GPG keys`，新建一个SSH进行添加）

3. 测试，输入命令，如果如下图所示，出现用户名则成功

   ```bash
   ssh -T git@github.com
   ```

   <img src="image-20200828192040358.png" alt="设置成功" style="zoom:80%;" />

4. 打开根目录下`_config.yml`文件，修改最后一行deploy的配置，repository修改为自己的github项目地址

   ```bash
   deploy:
   - type: git
     repository:
       github: git@github.com:night-candle/night-candle.github.io.git
       # coding: git@e.coding.net:godweiyang/godweiyang.git
     branch: master
   ```

5. 将本地推送到GitHub远程仓库，在git bash输入以下指令

   ```
   hexo clean
   hexo g
   hexo d
   ```

   ​	

## 4.补充

### 4.1 添加文章

1. git bash安装扩展`npm i hexo-deployer-git`

2. 然后输入`hexo new post "article title"`，新建一篇文章

3. 然后打开`\source\_posts`的目录，多了一个文件夹和一个`.md`文件，一个用来存放图片等数据，另一个是文章

4. 编写完markdown文件后，根目录下输入`hexo g`生成静态网页，最后输入`hexo d`上传到github上

5. 文件头如下

   ```
   toc: true    # 是否有目录
   reward: true  # 是否有打赏
   title: vuex   # 标题名称
   tags:     # 小标签
   - 随笔
   - vue
   ```



### 4.2 绑定域名

打开github项目，点击`settings`，拉到下面`Custom domain`处，填上你自己的域名，保存

项目根目录会出现一个名为`CNAME`的文件。（如果没有，手动创建`CNAME`文件，注意没有后缀，然后在里面写上域名保存）



### 4.3 添加评论功能

1. 获取Client ID和Client Secret

   https://github.com/settings/applications/new

<img src="clip_image018.jpg" alt="注册" style="zoom:80%;" />

2. 在Settings/Developer settings/OAuth Apps中可以找到Client ID和Client Secret

<img src="clip_image020.jpg" alt="" style="zoom:80%;" />

3. 修改配置文件

### 4.4 备份博客源文件

[教程](https://lvraikkonen.github.io/2016/05/31/%E5%88%A9%E7%94%A8Github%E5%88%86%E6%94%AF%E5%A4%87%E4%BB%BDHexo%E6%BA%90%E6%96%87%E4%BB%B6/)



### 4.5 解决文章预览显示过长

手动在文章内部加上`<!-- more -->`

<img src="clip_image014.jpg" alt="" style="zoom:80%;" />

### 4.6 个性化设置

文章头设置、添加404页面、文章头设置、“关于”页面增加、解决mathjax与代码高亮的冲突、增加建站时间（略）

