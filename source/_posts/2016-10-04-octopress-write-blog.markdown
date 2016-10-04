---
layout: post
title: "使用Octopress搭建静态博客网站"
date: 2016-10-04 13:13:34 +0800
comments: true
categories: [Octopress,Blog,Git]
---

一直想建个属于自己的博客，但是又不想依托于某种平台来写博客，因为这种无法自己掌控的感觉是我所讨厌的。恰巧在自学Android的过程中，遇到了[stormzhang](http://stormzhang.com/posts/)的博客，于是开始照葫芦画瓢，立马开始学习用Octopress搭建博客，下面简单梳理一下搭建过程中的要点。

##1.环境准备
首先要在GitHub上面创建一个帐号，之后在本地系统上安装Git，生成一个SSH Key，并添加到GitHub帐号里面的SSH Keys。

接下来是Ruby和DevKit两个软件的安装并且使两者相关联，注意Ruby安装的时候要把`Add Ruby executables to your PATH`勾选上。

最后便是安装Octopress，这一步我出现的问题最多，卡了我很久，最后是通过Google解决了，下面说一下我自己的解决过程。

首先克隆Octopress至本地：
```
git clone git://github.com/imathis/octopress.git octopress
cd octopress
```
接下来是安装依赖项，这一步受限于国内的网络环境，搭建的时候遇到了各种问题，本人的安装过程如下：
```
$ gem sources -a http://rubygems.org
$ gem sources -r https://rubygems.org
```
然后把octopress文件夹下`Gemfile`文件中的`source "https://rubygems.org"`更改为`source "http://rubygems.org"`，然后进行安装
```
$ gem install bundler
$ bundle install
$ rake install
```
##2.生成博客与单页面
生成静态网页：
```
$ rake generate
```
本地预览：
```
$ rake preview  
```
新建博客：
```
$ rake new_post["title"]  #http://localhost:4000
```
新建单页面：
```
$ rake new_page["name"]  #http://localhost:4000/name
```
##3.部署博客、托管源码至GitHub
###部署博客：
GitHub新建仓库：`username.github.io`
与本地Octopress目录绑定：
```
$ rake setup_github_pages
$ rake deploy
```
###托管源码：
将source目录更新到远程仓库：
```
$ git add .
$ git commit -m 'your message'
$ git push origin source
```