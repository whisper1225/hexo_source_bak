---
layout: post
title: github+hexo搭建个人博客实录.md
date: 2016-01-21 13:03:24
comments: true
tags:
	- hexo和github搭建博客
---
安装过程中遇到不少问题，具体的步骤就不详细介绍了，主要记录遇到的坑，以及没有解决的问题。
<!--more-->

## **一、前言**
之前有两篇博客莫名被csdn给删除了，一时兴起，想想要不搭建一个个人博客。于是选择了比较常见的github+hexo。
自己的电脑是mac air，由于以前驱动一些硬件的需要，安装了windows，后来一直没有换回来。搞github +  hexo，前途凶险。看小伙伴的搭建过程，感觉还是在mac 系统下安装应该更加省事。当然网最重要，网一定要好。
> 这是自己的搭建个人博客的第一篇，正好记录搭建过程，纪念一下。

## **二、安装支持软件和新建仓库**
### **1、安装node.js和git**
安装之后最好在命令窗口测试一下；git版本还是有讲究的，这个后面再说。
### **2、建立github.io项目**
注意名字和github名称一致，这个影响到后来难呢过不能通过username.github.io访问的问题-
生成ssh key 添加公钥到github上。可以使用 ssh -T git@github.com测试--》Git会根据用户的名字和邮箱来记录提交。GitHub也是用这些信息来做权限的处理，输入下面的代码                 进行个人信息的设置，把名称和邮箱替换成你自己的，名字必须是你的真名，而不是GitHub的昵称。
    $ git config --global user.name "name"//用户名
    $ git config --global user.email  "your eamil"//填写自己的邮箱

## **三 、安装hexo**
安装一般建立一个github文件目录，里面再建立一个hexo文件夹（名字随便可以叫hexo或者blog之类的）。后面很多操作都在此文件夹之下。
### 1. 用npm安装hexo一般使用国内淘宝镜像（如果默认镜像能行就没什么问题）
    npm install -g cnpm --registry=https://registry.npm.taobao.org
    但是我竟然连这个也安装不成功。我的网是可以科学上网的啊，不科学啊。
    应该说整个过程最麻烦的地方就在联网安装。这个在天朝真的没办法。如果这个不能安装，我们可以在每次npm命令之后指定这个淘宝镜像。
### 2. 修改镜像地址
    安装了好多次，始终不能成功（当时都快哭了）。后来发现只要把协议改成http协议就能安装成功，而且速度很快（原理就不说了），这个是参考安卓的加速jcenter下载的解决办法。联网安装成功。
![](http://7xqbxa.com1.z0.glb.clouddn.com/github_recordHexo_mirrorhttps.png)


### 3. 找不到hexo命令
    但是使用命令hexo却提示没有这个命令，我看教程上大家都没有说这个，难道google第一页的教程都是window下安装的？
**这个问题可能是命令行窗口没有报错，但是其实安装失败了，没有执行文件，要么就是安装成功，执行文件没有添加到环境变量。于是准备找到可执行文件，把其所父目录地址添加到环境变量**
我在下面的文件夹中用Everything检索到了几个和hexo相关的文件。但是没有找到相关的执行文件。
![](http://7xqbxa.com1.z0.glb.clouddn.com/github_recordHexo_hexo_containHexoFile.png)
明显已经安装了，hexo，但是威慑么在hexo文件夹下没有可执行文件了？？？
![](http://7xqbxa.com1.z0.glb.clouddn.com/github_recordHexo_hexo_noexecuteFile.png)

然后google，有人说必须启动在hexo（之前新建的）文件夹下面开管理员命令窗口。有人说得 npm cache clean（后来我才明白这个cache为什么这么重要，但是这个clean和我这个错误没有任何关系）。有人说版本问题，我clean重来不行，更换nodejs版本依旧不行。
找人帮忙，小伙伴说window下他当时安装是在nodejs的相关目录下，新建global_module和global_cache文件夹。然后安装时用-g参数指定到这个安装位置，然后将此文件夹添加到环境变量。这种做法是参考博客园 金玉石的一篇文章的（好像是叫这个名字）。但是依然不行啊。我哭瞎了，选择了放弃。
### 4. 运行hexo成功
    吃过晚饭坐在桌前，看看电影，看着看着心里还是不舒坦，又想起这茬，不行我还得鼓捣。我把所有的东西全部卸载，不能卸载的手动清空。凭直觉，大部分人教程都是直接安装hexo，然后就能运行命令。第三条中说的建立的两个文件夹，如果我们不建，必然是安装在某一个目录下默认目录。这么多教程都没说这个问题，想必是可以不建的。
我从零开始走了一遍，依然运行hexo找不到命令，我检索文件系统后发现在nod_cache目录最后居然有一个可执行文件。
![](http://7xqbxa.com1.z0.glb.clouddn.com/github_recordHexo_hasExecuteFile.png)

把改图顶上的位置添加到环境变量，everything is ok。
![](http://7xqbxa.com1.z0.glb.clouddn.com/github_recordHexo_hexoRunOk.png)
>  现在回顾一下，应该在我第三步，新建那两个文件夹时就已经成功了，但是潜意识觉得hexo可执行文件就在hexo文件夹中，但是没想到他居然散落在和各个module文件夹并列的位置。而且当时也很轴了，要是随便试试将node_cache添加到环境变量就ok了。主要是对

## **四、运行hexo**
### **1、步骤**
init-->npm install 安装相关插件--》 hexo s -g 生成静态文件并且启动本地server--》用浏览器查看-》配置yml文件，指定git相关参数
可以在先hexo g 然后 hexo s -p 你的端口号指定端口，现在本地看看效果，然后推送到github上(至于能不能直接hexo s -p 4000 -g 这种形式就没试了)。
### **2、坑**
1. hexo s -g server失败：本来npm install 安装的插件够用了。但是好像是由于版本的原因，比如什么server和deplyoer之类的插件需要单独再次安装（之前由于各种错误，为了保险将nodejs的版本降得较低）。
2. 服务器成功启动了，成功启动的样子各个博客都有就不贴图了。但是浏览器localhost:4000无法访问。有人说要用127.0.0.1，有人说过十分钟就好了，当然也不排除这种可能,推酷上就分析了这个原因<http://www.tuicool.com/articles/uE7FJba>。大部分情况都是端口占用，用netstar查看，是被就127.0.0.1和0.0.0.1使用，这个不太合理。我关机再起，一启动就被0.0.0.0占用。没道理啊，我还没开hexo服务器啊。
算了重启的时候指定端口，ok。
![](http://7xqbxa.com1.z0.glb.clouddn.com/github_recordHexo_hexopushSuccPage1.png)

3.
```xml
    deploy:
  type: git
  repository: git@github.com:whisper1225/whisper1225.github.io.git
  branch: master
```
第一次错误是type后面必须有空格，我没有。。。
第二次是permission deny,public key ，unknown host之类的什么。
我检查了user/.ssh文件夹下的knownhost文件，发现部署了几次之后，notepad++提示known_hosts有变动，然后好像添加了一行什么的。然后就好了 hexo d  -g 依然失败，报错很类似但是没有了没有known_hosts。总之push不成功。有人说是git版本不对，我觉得他扯犊子，我平时都是可以的。但是我还是试了下，直接用最新的git2.7 push成功。这脸打得疼啊，火燎火燎的。
![](http://7xqbxa.com1.z0.glb.clouddn.com/github_recordHexo_hexopushSucc.png)

> **没有解决的问题：**关于hexo d部署应该是调用原生git直接add commit 然后合并提交。但是我不知道怎么使用参数来commit "xxx" 注解。想向github提交的时候能够用git直接管理。
> 其原理就是hexo在执行hexo generate时会在本地先把博客生成的一套静态站点放到public文件夹中，在执行hexo deploy时将其完全复制（文件夹结构都是一样的）到.deploy文件夹中并push。
> 如果直接使用git bash管理，可以直接向服务器提交public文件夹内的代码，问题解决。


## **五、装修**
请原谅我取了个这么土的词，
<https://www.zhihu.com/question/24422335>
首推：yilia 没看太明白，可以用标签来代替一层分类。
然后有个对于这个的升级版带目录的，但是不好看了：<http://hexo.trity.cc/2015/08/24/hexo%E5%8D%9A%E5%AE%A2%E6%8D%A2%E4%B8%BB%E9%A2%98--icarus>
其次Pacman绚丽简洁，带分类。不亚于yilia。
![](http://7xqbxa.com1.z0.glb.clouddn.com/github_recordHexo_hexoGithubIndex.png)
> 对于模板的配置是这配置在主题的_config.yml文件夹下，不是配置在hexo init <folder>的文件夹下。

## **六、总结**
之前所走的许多弯路，主要原因还是因为对nodejs和npm一无所知。对于yilia主题还有一些文章的排序（现有的好像是按照时间顺序进行排序），置顶等功能也很重要，好像主题作者说要完成。

## **七、参考教程**
安装之前找了一堆教程，现在安装成功之后回头来看有一些靠谱的教程。而且这次顺手注册了个七牛，这丫的居然要我手机号、支付宝号、身份证。**而且还要我授权提取支付宝信息**，但是我还填写了，谁让我穷啊。
1. [自带软件下载链接，这个其实没那么重要，但是不能一次安装成功的前提下，还是很重要的](http://blog.csdn.net/jzooo/article/details/46781805)
2. [这个很全面，从域名到装修一条龙](http://www.jianshu.com/p/05289a4bc8b2)
3. [这个是补充的，之前因为这篇博客页面太丑，没细看](http://ibruce.info/2013/11/22/hexo-your-blog/)
但是这个介绍了一个网站所需要的各个方面，包括搜索引擎优化。吐血推荐！
4. [主题优化方面，亮点是右边的那个文章目录toc因为文件夹结构的变化，我没有照着做出来](http://www.voidking.com/2015/05/31/deve-hexo-theme-optimize/#添加头像)

