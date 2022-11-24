---
layout: _post
title: 博客集成评论功能---Gitalk
date: 2022-11-17 16:53:51
tags:
- blog
---

# 博客集成评论功能---Gitalk

## 一、什么是 Gitalk

`Gitalk` 的官方网站地址是: [gitalk.github.io](https://link.zhihu.com/?target=https%3A//gitalk.github.io/)，是一个基于 `GitHub Issue `和 `Preact` 开发的评论插件。

## 二、特性

* 使用 GitHub 登录
* 支持多语言 [en, zh-CN, zh-TW, es-ES, fr, ru, de, pl, ko, fa, ja]
* 支持个人或组织
* 无干扰模式（设置 distractionFreeMode 为 true 开启）
* 快捷键提交评论 （cmd|ctrl + enter）

## 三、安装

#### 两种方式

- 直接引入

```yml
  <link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/gitalk@1/dist/gitalk.css">
  <script src="https://cdn.jsdelivr.net/npm/gitalk@1/dist/gitalk.min.js"></script>

  <!-- or -->

  <link rel="stylesheet" href="https://unpkg.com/gitalk/dist/gitalk.css">
  <script src="https://unpkg.com/gitalk/dist/gitalk.min.js"></script>
```

- npm 安装

```bash
npm i --save gitalk
import 'gitalk/dist/gitalk.css'
import Gitalk from 'gitalk'
```

## 四、使用	

1. 首先，您需要选择一个公共github存储库（已存在或创建一个新的github存储库）用于存储评论，

   ![image-20221117161922198](image-20221117161922198.png)

2. 创建完成后，点击`Settings` 打开 `Issues` 功能，默认是打开的

3. 然后需要创建 **GitHub Application**，如果没有 [点击这里申请](https://github.com/settings/applications/new)，`Authorization callback URL` 填写当前使用插件页面的域名。

4. 开创建应用程序页面，填写信息，两个 URL 就是你网站的域名。应用名称与描述可自起。 可参考下图

   ![image-20221117162810692](image-20221117162810692.png)

5. 应用程序创建成功后跳转到了以下页面，图中 `Client ID` 和 `Client Secret`是我们需要的东西

   ![image-20221117163158794](image-20221117163158794.png)

## 五、集成 Gitalk



### 方式一

只需要将如下代码引入你想添加评论的 html 或者 jsp 页面中就可以使用了

~~~js
<!-- 引入 -->
<link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/gitalk@1/dist/gitalk.css">
  <script src="https://cdn.jsdelivr.net/npm/gitalk@1/dist/gitalk.min.js"></script>

<!-- 在页面中添加一个容器-->
<div id="gitalk-container"></div>
~~~

使用下面的 Javascript 代码生成 gitalk 插件

~~~js
 var gitalk = new Gitalk({   
     clientID: 'GitHub Application Client ID',   //GitHub Application Client ID
     clientSecret: 'GitHub Application Client Secret',   //GitHub Application Client Secret
     repo: 'GitHub repo',   //仓库名称(GitHub repo)
     owner: 'GitHub repo owner',   //仓库拥有者(GitHub repo owner) 
     admin: ['GitHub repo owner and collaborators, only these guys can initialize github issues'],   
     id: location.pathname,      // 请确保你的 location 连接小于 50 个字符，否则，插件会生成失败   
     distractionFreeMode: false // 专注模式 
})  

    gitalk.render('gitalk-container')
~~~

### 方式二 

使用react的组件：

```js
import GitalkComponent from 'gitalk/dist/gitalk-component'

<GitalkComponent
 options={{
 clientID: '223232323adawdawd',
 clientSecret: 'ddadawdadaddawdawdawdawdwadawd',
 repo: 'dailyProject',
 owner: 'Mrrabbitan',
 admin: ['Mrrabbitan'],
 id: location.pathname, // Ensure uniqueness and length less than 50
 distractionFreeMode: false, // Facebook-like distraction free mode
        }}
 ></GitalkComponent>
```

## 总结

以上就是添加gitalk详细步骤，具体操作可参考官方文档：https://github.com/gitalk/gitalk/blob/master/readme-cn.md



### 注意

1. 如若第一次进入时评论模块加载不出来，需要注册 `Github Application` 的账号登录评论模块后刷新页面，就可以正常使用了。
2. GitHub 对 Issue 的 label 存在限制，不能超过 50 个字符。
   1. PS: label 标签就是文章页面的链接地址，如果地址过长，会导致加载 Gitalk 插件失败。
   2. 解决方案，可参考链接：https://github.com/gitalk/gitalk/issues/102



参考文章：

[平酱的填坑札记](https://www.zhihu.com/column/c_1089178309891493888)：博客集成评论功能---Gitalk

[超Ren专属](https://blog.csdn.net/qq_39052513)：超 Nice 的评论组件 —— Gitalk

[官方文档](https://github.com/gitalk/gitalk/blob/master/readme-cn.md)：https://github.com/gitalk/gitalk/blob/master/readme-cn.md