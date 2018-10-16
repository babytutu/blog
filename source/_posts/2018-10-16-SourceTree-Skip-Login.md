---
title: SourceTree 安装跳过登录账号
date: 2018-10-16 10:08:02
tags:
  - sourcetree
categories:
  - soft
---

Sourcetree-免费的git图形化管理工具 - [官网](https://www.sourcetreeapp.com/)

# 跳过登录账号

> *因不可描述的原因，软件安装过程中的注册账号可能有问题*，windows下有特殊技巧
> 安装包和相关文件已放入[百度网盘](https://yun.baidu.com/s/1kXd9gIoVx_oBHxD2v8WqYw)

<!--More-->

## Step1

下载安装包，双击安装，遇到提示登录账号，关闭安装界面

- [官方安装包下载地址，版本2.6.10](https://downloads.atlassian.com/software/sourcetree/windows/ga/SourceTreeSetup-2.6.10.exe)
- 如果无法下载，可以[百度网盘](https://yun.baidu.com/s/1kXd9gIoVx_oBHxD2v8WqYw)


## Step2
打开`我的电脑`，在最上方的地址栏直接输入以下地址
```
%LocalAppData%\Atlassian\SourceTree\
```
在这个目录下新建一个名为 `accounts.json` 的文件

```json
[
  {
    "$id": "1",
    "$type": "SourceTree.Api.Host.Identity.Model.IdentityAccount, SourceTree.Api.Host.Identity",
    "Authenticate": true,
    "HostInstance": {
      "$id": "2",
      "$type": "SourceTree.Host.Atlassianaccount.AtlassianAccountInstance, SourceTree.Host.AtlassianAccount",
      "Host": {
        "$id": "3",
        "$type": "SourceTree.Host.Atlassianaccount.AtlassianAccountHost, SourceTree.Host.AtlassianAccount",
        "Id": "atlassian account"
      },
      "BaseUrl": "https://id.atlassian.com/"
    },
    "Credentials": {
      "$id": "4",
      "$type": "SourceTree.Model.BasicAuthCredentials, SourceTree.Api.Account",
      "Username": "",
      "Email": null
    },
    "IsDefault": false
  }
]
```

## Step3
再次双击安装，会发现跳过了登录账号的界面并直接进入了主界面，就可以正常使用了