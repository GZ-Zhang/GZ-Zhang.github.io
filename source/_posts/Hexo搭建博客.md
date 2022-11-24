---
layout: _post
title: Hexo搭建博客
date: 2022-11-16 16:45:34
tags:
- blog
---

参考官方文档：https://hexo.io/zh-cn/

## 前言

​		作为技术人员，都希望拥有一个自己的技术博客，在查阅资料选择Hexo+Github的博客系统，这里将其过程记录下来。

> 博客部署在linux环境下, CentOS 7.x

### 安装前提

安装 Hexo 相当简单，只需要先安装下列应用程序即可：

- [Node.js](http://nodejs.org/) (Node.js 版本需不低于 10.13，建议使用 Node.js 12.0 及以上版本)
- [Git](http://git-scm.com/)

如果您的电脑中已经安装上述必备程序，那么恭喜您！你可以直接前往 [安装 Hexo](https://hexo.io/zh-cn/docs/#安装-Hexo) 步骤。

如果您的电脑中尚未安装所需要的程序，请根据以下安装指示完成安装。

![image-20221116153041011](image-20221116153041011.png)

#### 安装 Git

**两种方式**：在线安装（不推荐），解压安装。

1. 在线安装（使用[yum](https://so.csdn.net/so/search?q=yum&spm=1001.2101.3001.7020)安装的版本为1.8.3，这个版本太老）

   ~~~
   yum install git
   git --version
   ~~~

2. 解压安装

   想要使用最新版的git，进入git 在GitHub上发布版本页面：https://github.com/git/git/tags  选择最新的tar.gz包下载即可。

   ~~~bash
   # 1. 上传到指定目录 /opt/software
   # 2. 解压到当前目录
   tar -zxvf git-2.38.1.tar.gz
   rm -rf git-2.9.5.tar.gz 
   # 进入到解压后的文件夹
   cd  ./git-2.38.1
   # 3. 解压后的源码需要编译源码，不过在此之前需要安装编译所需要的依赖。中途出现提示的时候输入y即可
   yum install curl-devel expat-devel gettext-devel openssl-devel zlib-devel gcc perl-ExtUtils-MakeMaker
   # 4. 安装依赖时，自动安装了Git，因此需要卸载旧版本Git
   git --version
   yum remove git
   # 5. 编译git源码
   make prefix=/usr/local/git all
   # 6. 安装git至/usr/local/git路径
   make prefix=/usr/local/git install
   
   # 配置环境变量配置
   vim /etc/profile
   
   # 在最底部加上
   PATH=$PATH:/usr/local/git/bin
   export PATH
   
   # 刷新环境变量
   source /etc/profile
   # 查看Git是否安装完成
   git --version
   ~~~

   参考文章：

   https://blog.csdn.net/w_shimmer/article/details/124342141

   https://blog.csdn.net/weixin_43847283/article/details/124781559

#### 安装 node

1. 查看系统位数

```bash
uname -a
```

2. [官网下载对应文件](http://nodejs.cn/download/)

![image-20221116153606803](image-20221116153606803.png)



3. 下载下来的tar文件上传到服务器并且解压，然后通过建立[软连接](https://so.csdn.net/so/search?q=软连接&spm=1001.2101.3001.7020)变为全局

   ~~~bash
   cd /opt/software
   # 上传文件
   tar -zxvf node-v16.18.0-linux-x64.tar.xz 
   # 删除压缩包
   rm -rf node-v16.18.0-linux-x64.tar.xz 
   # 重命名
   mv node-v16.18.0-linux-x64/ node
   # 确认一下nodejs下bin目录是否有node 和npm文件
   cd node/bin
   ls
   
   
   # 建立软连接，变为全局
   ln -s /opt/software/node/bin/npm /usr/local/bin
   ln -s /opt/software/node/bin/node /usr/local/bin
   ~~~

4. 检验

   ~~~bash
   node -v
   npm -v
   ~~~

   参考文章：

   https://blog.csdn.net/weixin_43847283/article/details/124781443



### 安装Hexo

1. 所有必备的应用程序安装完成后，即可使用 npm 安装 Hexo。

```bash
cd /opt/software
mkdir hexo
cd hexo/
npm install -g hexo-cli
```

2. hexo在nodejs的nodejs/bin目录可以找到hexo命令，采用**软连接**把hexo命令添加到全局

~~~
# 根据个人nodejs路径进行配置
ln -s /opt/software/node/bin/hexo   /usr/local/bin/hexo
# 配置错了可以删除再重新配置
rm -rf  /usr/local/bin/hexo
ln -s /opt/software/node/bin/hexo   /usr/local/bin/hexo


npm install hexo-cli -g
hexo init blog
cd blog
npm install
hexo server
~~~

查看是否生效

~~~bash
hexo -v
~~~

3. 部署hexo

~~~bash
hexo init blog
cd blog
npm install
# 启动
hexo s
~~~

参考链接：

https://blog.csdn.net/weixin_43847283/article/details/124781731