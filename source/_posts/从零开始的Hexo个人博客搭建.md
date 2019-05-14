---
title: 从零开始的Hexo个人博客搭建
copyright: true
date: 2019-01-10 13:40:15
categories: Hexo
tags:
---


>之前搭建的个人博客，但是各种各样的原因导致好久没有更新自己的博客，现在年底想写点东西保存下来，为明年找新工作做准备，但是好久没来，对Hexo博客的使用有点遗忘，特此从零开始，对Hexo搭建的步骤进行一次记录。
此次写作，完全参考了[吴小龙同学-手把手教你建github技术博客by hexo][1]一文，说是转载也不为过，但是也有我从其他地方查找到的资料，特此声明。

##环境准备
####安装Git
[git官网][2]下载并执行即可完成安装。
####安装Node.js
在Windows环境下安装[Node.js][3]非常简单，仅须下载安装文件并执行即可完成安装。
####安装hexo
利用npm命令即可安装。（在任意位置点击鼠标右键，选择Git bash）
```npm install -g hexo```
***问题***

  - npm ERR!registry error parsing json错误

可能需要设置npm代理，执行命令
```npm config set registry  http://registry.cnpmjs.org```

 - hexo:command not found
  删除刚刚安装的npm目录，重新执行命令：
```npm install -g hexo```
来安装hexo。
####创建hexo文件夹
安装完成后，在你喜欢的文件夹下（如：H:\hexo），执行以下指令（在H:\hexo内点击鼠标右键，选择Git bash），Hexo即会自动在目标文件夹建立网站所需要的所有文件。
```hexo init```
####安装依赖包
```npm install```
####本地查看
现在我们已经搭建起本地的hexo博客了，执行以下命令（在H:\hexo），然后到浏览器输入localhost:4000看看。
```
hexo generate
hexo server
```
至此，本地博客已经搭建起来了，当然，现在只是本地的，接下来我们要部署在Github。
***问题***

 - 执行hexo server提示找不到该指令
解决办法：
在Hexo 3.0后server被单独出来了，需要安装server，安装的命令如下：
```npm install hexo -server --save```
安装此server后再试，问题解决
##Github创建博客
####创建页面仓库
这个仓库的名字需要和你的账号对应，格式：yourname.github.io
输入基本信息，然后点击创建仓库![此处输入图片的描述][4]
**注意**
命名规则:你的Github账号.github.io
####查看SSH
SSH公钥默认储存在账户的主目录下的~/.ssh目录。
进如.ssh目录下，命令行：
```ls```
查看，如果返回something和something.pub，说明已经有SSH公钥。
####生成SSH公钥
没有的话，生成，还是在.ssh目录下，命令行：
ssh-keygen -t rsa -C "你的邮箱地址"
按3个回车，密码为空。
在 C:\Users\Administrator.ssh 下，得到两个文件 id_rsa 和 id_rsa.pub。
####在Github上添加SSH密钥
打开id_rsa.pub，复制全文到[https://github.com/settings/ssh][5]，Add SSH key粘贴进去
##hexo使用
####目录结构
```
├── .deploy       #需要部署的文件
├── node_modules  #Hexo插件
├── public        #生成的静态网页文件
├── scaffolds     #模板
├── source        #博客正文和其他源文件，404、favicon、CNAME 都应该放在这里
|   ├── _drafts   #草稿
|   └── _posts    #文章
├── themes        #主题
├── _config.yml   #全局配置文件
└── package.json
```
全局配置_config.yml
```
# Hexo Configuration
# Docs: http://hexo.io/docs/configuration.html
# Source: https://github.com/hexojs/hexo/
# Site #站点信息
title:  #标题
subtitle:  #副标题
description:  #站点描述，给搜索引擎看的
author:  #作者
email:  #电子邮箱
language: zh-CN #语言
# URL #链接格式
url:  #网址
root: / #根目录
permalink: :year/:month/:day/:title/ #文章的链接格式
tag_dir: tags #标签目录
archive_dir: archives #存档目录
category_dir: categories #分类目录
code_dir: downloads/code
permalink_defaults:
# Directory #目录
source_dir: source #源文件目录
public_dir: public #生成的网页文件目录
# Writing #写作
new_post_name: :title.md #新文章标题
default_layout: post #默认的模板，包括 post、page、photo、draft（文章、页面、照片、草稿）
titlecase: false #标题转换成大写
external_link: true #在新选项卡中打开连接
filename_case: 0
render_drafts: false
post_asset_folder: false
relative_link: false
highlight: #语法高亮
  enable: true #是否启用
  line_number: true #显示行号
  tab_replace:
# Category & Tag #分类和标签
default_category: uncategorized #默认分类
category_map:
tag_map:
# Archives
2: 开启分页
1: 禁用分页
0: 全部禁用
archive: 2
category: 2
tag: 2
# Server #本地服务器
port: 4000 #端口号
server_ip: localhost #IP 地址
logger: false
logger_format: dev
# Date / Time format #日期时间格式
date_format: YYYY-MM-DD #参考http://momentjs.com/docs/#/displaying/format/
time_format: H:mm:ss
# Pagination #分页
per_page: 10 #每页文章数，设置成 0 禁用分页
pagination_dir: page
# Disqus #Disqus评论，替换为多说
disqus_shortname:
# Extensions #拓展插件
theme: landscape-plus #主题
exclude_generator:
plugins: #插件，例如生成 RSS 和站点地图的
 - hexo-generator-feed
 - hexo-generator-sitemap
# Deployment #部署，将 lmintlcx 改成用户名
deploy:
  type: git
  repo: 刚刚github创库地址.git
  branch: master
```
***注意***

 - 配置文件的冒号“:”后面有一个空格
 - repo: 刚刚 GitHub 创库地址.git

####hexo命令行使用
常用命令
```

```

简写：
```
hexo n == hexo new
hexo g == hexo generate
hexo s == hexo server
hexo d == hexo deploy
```

####编辑文章
新建文章
```hexo new "标题"```
在 _posts 目录下会生成文件标题.md：
```
title: Hello World
date: 2019-01-10 07:56:29 #发表日期，一般不改动
categories: hexo #文章文类
tags: [hexo,github] #文章标签，多于一项时用这种格式
---
正文，使用 Markdown 语法书写
```
编辑完后保存，hexo server预览

####hexo部署
执行下列指令即可完成部署
```
hexo generate
hexo deploy
```
hexo deploy 问题：Deployer not found:git
执行
```
npm install hexo-deployer-git --save
```
再重新hexo deploy，以下提示说明部署成功:
```
o[info] Deploy done: git
```
点击Github上项目的Settings，Github Pages，提示 Your site is published at [http://allenlucas.ml][6](这是我自己申请的域名)

##图床
~~之前使用的七牛云存储来做图床，但是测试域名一个月后被收回，而我的域名是未备案的，pass。~~
目前再网上使用的[又拍图片管家][7]，目前是免费用户，感觉效果还可可以，后续有更好的再更新。
##域名
我是在国外申请的一年免费域名，将就用
##DNS设置
使用[CloudXNS][8]来进行解析，效果不错。


  [1]: http://wuxiaolong.me/2015/07/31/build-blog-by-hexo/ "手把手教你建github技术博客by hexo"
  [2]: https://git-scm.com/ "Git官网"
  [3]: https://nodejs.org/en/ "Node.js官网"
  [4]: http://pic.yupoo.com/l476849560/dcb1f3f3/45658191.png
  [5]: https://github.com/settings/ssh
  [6]: http://allenlucas.ml
  [7]: https://x.yupoo.com/http://allenlucas.ml
  [8]: http://www.cloudxns.net/