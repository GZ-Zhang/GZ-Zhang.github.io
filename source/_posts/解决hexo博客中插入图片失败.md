---
layout: _post
title: 解决hexo博客中插入图片失败
date: 2022-11-17 18:15:39
tags:
  - blog
categories:
  - blogs
---
# 解决hexo博客中插入图片失败

## 前言：

​		搭建博客后按照[官方文档](https://hexo.io/zh-cn/docs/asset-folders)配置后，图片一直无法显示，在网上百度一直没有解决方案，最终在官方文档评论区发现解决方案。思考了一下，遇到问题如果有评论区还是要优先查看一下再去百度，大家遇到相似问题概率比较大，还是要感谢评论区大神，推荐详细阅读第一个参考链接，启发很大。

> 参考链接：
>
> [hexo博客中插入图片失败——解决思路及个人最终解决办法](https://blog.csdn.net/m0_43401436)
>
> [hexo+github快速搭建html5静态网页全过程](https://alvincr.com/2021/01/hexo-with-github_pages/#wang_ye_wu_fa_xian_shi_tu_pian)

## 解决方案：

### 1. 官网解决方案

> 官方文档：https://hexo.io/zh-cn/docs/asset-folders

#### 使用 Markdown 嵌入图片

[hexo-renderer-marked](https://github.com/hexojs/hexo-renderer-marked) 3.1.0 引入了一个新的选项，其允许你无需使用 `asset_img` 标签插件就可以在 markdown 中嵌入图片

如需启用：

```yml
_config.yml
post_asset_folder: true
marked:
  prependRoot: true
  postAsset: true
```

启用后，资源图片将会被自动解析为其对应文章的路径。
例如： `image.jpg` 位置为 `/2020/01/02/foo/image.jpg` ，这表示它是 `/2020/01/02/foo/` 文章的一张资源图片， `![](image.jpg)` 将会被解析为 `<img src="/2020/01/02/foo/image.jpg">`

### 2. 百度搜索得到解决方案	

* 方法1：设置图片直接引用网络资源
* 方法2：使用hexo-asset-image插件

`方案一`可以选择将markdown图片文件存放在云中，编写时直接引用云资源，考虑目前暂时还不需要所以放弃，选择`方案二`

#### 方法2：使用hexo-asset-image插件

1. 打开根目录下_config.yml文件找到post_asset_folder: true 设置为true,在下面添加(可参靠上文，官网解决方案：使用 Markdown 嵌入图片)：

   ~~~yml
   marked:
     prependRoot: true
     postAsset: true
   ~~~

2. 安装插件

   ~~~bash
   npm install https://github.com/CodeFalling/hexo-asset-image --save
   ~~~

3. 可以选择将Typora设置为./${filename} ，目的是自动在目录下建立与文件同名的文件夹方便存取

   ![image-20221117180553792](image-20221117180553792.png)

至此就解决图片无法加载问题，就已解决

## 注意

1. 若要上传服务器，图片引用链接应直接保存文件名即可，放入博客同名文件下即可。

   ![image-20221117181857969](image-20221117181857969.png)

