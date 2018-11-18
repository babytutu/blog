---
title: Install Nodejs on CentOS
date: 2018-11-18 21:37:13
tags:
  - node
categories:
  - CentOS
---

# Installation instructions

## Run as root on RHEL, CentOS, CloudLinux or Fedora:

<!--more-->
NodeJS 11.x

```bash
curl -sL https://rpm.nodesource.com/setup_11.x | bash -
```

NodeJS 10.x

```bash
curl -sL https://rpm.nodesource.com/setup_10.x | bash -
```
NodeJS 8.x


```bash
curl -sL https://rpm.nodesource.com/setup_8.x | bash -
```

Optional: install build tools

> To compile and install native addons from npm you may also need to install build tools:

```bash
yum install gcc-c++ make
# or: yum groupinstall 'Development Tools'
```

## yum

```bash
yum install -y nodejs
```

## check

```bash
node -v
```

# 参考文档
[nodesource](https://github.com/nodesource/distributions/blob/master/README.md#rpminstall)