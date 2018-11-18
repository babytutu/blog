---
title: Install DOClever on CentOS
date: 2018-11-18 22:12:44
tags:
  - DOClever
categories:
  - CentOS
---

# DOClever

DOClever是一个商业化开源产品，完全免费。无论你是前端工程师，还是后端工程师，接口永远都是两者交互的桥梁，所以DOClever专为中小型团队量身打造，旨在解决接口的管理，测试与数据生成，实现真正的一体化解决方案。

[github](https://github.com/sx1989827/DOClever)

<!--more-->

# 如何部署

## 首先本地要安装node环境，推荐8.11.1版本(下载页面)

## 安装[mongodb](https://www.mongodb.com/)

可使用[robomongo](https://robomongo.org/)来作为mongodb的客户端工具，启动mongodb后（如何启动），用robomongo来连接，新建一个database作为DOClever的数据库（名称随意）

## 源码部署
将DOClever的源码down到本地，在命令行下运行node DOClever的根目录/Server/bin/www（如果是windows环境下，请修改目录分隔符)，第一次启动，会出现命令行提示符，按照提示符输入即可完成相关的配置，等到DOClever启动成功后， 在浏览器里输入localhost:DOClever启动的端口号,出现首页表示部署成功。

## npm部署
在命令行下运行npm install doclever -g，等doclever包安装成功后，运行doclever进行第一次配置（如果有问题，就运行doclever --installwithsetup）