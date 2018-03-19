---
title: Mac效率神器Alfred
date: 2017-04-15 12:37:23
tags:
    - soft
---

## 懒人进击版
> 作为一个偶尔勤奋下的懒人，还是要不断进步的，一切为了让将来的自己能更懒，美其名曰：“晋级”

<!--more-->

## 更少的输入

### 前阵子对终端情有独钟，现在开始讲[Alfred](https://www.alfredapp.com/)
> Alfred是啥，是一个提升效率的软件，里面可以装很多东东，可以省略很多步骤，把大象塞冰箱分几步？1步！！！Alfred会做个[workflow](https://www.alfredapp.com/workflows/)让整个步骤变成一步！！！

#### 快速获取ip来了
> 获取当前ip，复制ip或直接打开ip:port(默认8080)

虽然终端用命令获取ip也挺方便的，复习下

```bash
ipconfig getifaddr en1
```

但也要经过打开终端然后输入命令，Alfred快捷键是option+空格，输入‘ip’

![img](/images/20170415/ip1.png)

回车，就直接把本地ip拷贝好了

那要直接打开ip:9001怎么办办呢？打开Alfred，输入‘loc 9001’

![img](/images/20170415/ip2.png)

回车，就在默认浏览器打开页面啦，是不是很神速？

> 相关下载：[LocalPort](http://www.packal.org/workflow/localport)

### 杀死死不了的端口

> 原理还是找到被占用的端口然后kill

复习下终端方法，2步走，略麻烦

```bash
lsof -i:9001
COMMAND   PID USER   FD   TYPE             DEVICE SIZE/OFF NODE NAME
node    92239 tutu   30u  IPv4 0xb8e1ecea1bd5ab81      0t0  TCP *:terabase (LISTEN)
kill 92239
```

Alfred就方便多了，比如我们要杀掉9001，输入‘kp 9001’

![img](/images/20170415/portkiller.png)

回车，就可以千里之外取上将首级，还会飘出个提醒信息

![img](/images/20170415/killer.png)

> 相关下载：[portkiller](http://www.packal.org/workflow/portkiller)


## 推荐几个比较常用的

[Github Search](http://www.packal.org/workflow/github-search)

> Alfred workflow to search for Github repository.——顾名思义，就是快速搜索github呗

![img](/images/20170415/github-search.png)

[Alfred npm search](http://www.packal.org/workflow/alfred-npm-search)

> Alfred workflow to search for npm package using npms API.——对，搜素npm包的。。。

![img](/images/20170415/npm-search.png)

[Youdao Dict](http://www.packal.org/workflow/youdao-dict)

> 使用有道翻译你想知道的单词和语句,其实我觉得翻译也不太准

![img](/images/20170415/youdao.png)

[MDN Search](http://www.packal.org/workflow/mdn-search)

> 我心里只有学习。。。

![img](/images/20170415/mdn.png)

[Jenkins](http://www.packal.org/workflow/jenkins)

> 工作中超实用的，这个就不截图