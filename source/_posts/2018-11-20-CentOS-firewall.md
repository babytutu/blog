---
title: CentOS-firewall
date: 2018-11-20 09:20:31
tags:
categories:
  - CentOS
---

# CentOS 使用firewalld打开关闭防火墙与端口

> 安装完一个服务后，开启了9001端口，网页访问提示无权限，考虑到可能是防火墙导致，关闭防火墙后正常访问，考虑到安全性，开启防火墙，单独开放了9001端口即可

## 单独开启9001端口

查看所有打开的端口：
```bash
firewall-cmd --zone=public --list-ports
```
添加（--permanent永久生效，没有此参数重启后失效）
```bash
firewall-cmd --zone=public --add-port=9001/tcp --permanent
```
重新载入
```bash
firewall-cmd --reload
```
再次查看所有打开的端口已确认效果

<!--more-->

## 所有相关资料

### firewalld的基本使用

启动：
```bash
systemctl start firewalld
```
关闭：
```bash
systemctl stop firewalld
```
查看状态：
```bash
systemctl status firewalld
```
开机禁用：
```bash
systemctl disable firewalld
```
开机启用：
```bash
systemctl enable firewalld
```

### systemctl

启动一个服务：
```bash
systemctl start firewalld.service
```
关闭一个服务：
```bash
systemctl stop firewalld.service
```
重启一个服务：
```bash
systemctl restart firewalld.service
```
显示一个服务的状态：
```bash
systemctl status firewalld.service
```
在开机时启用一个服务：
```bash
systemctl enable firewalld.service
```
在开机时禁用一个服务：
```bash
systemctl disable firewalld.service
```
查看服务是否开机启动：
```bash
systemctl is-enabled firewalld.service
```
查看已启动的服务列表：
```bash
systemctl list-unit-files|grep enabled
```
查看启动失败的服务列表：
```bash
systemctl --failed
```

### 配置firewalld-cmd

查看版本：
```bash
firewall-cmd --version
```
查看帮助：
```bash
firewall-cmd --help
```
显示状态：
```bash
firewall-cmd --state
```
查看所有打开的端口：
```bash
firewall-cmd --zone=public --list-ports
```
更新防火墙规则：
```bash
firewall-cmd --reload
```
查看区域信息:
```bash
firewall-cmd --get-active-zones
```
查看指定接口所属区域：
```bash
firewall-cmd --get-zone-of-interface=eth0
```
拒绝所有包：
```bash
firewall-cmd --panic-on
```
取消拒绝状态：
```bash
firewall-cmd --panic-off
```
查看是否拒绝：
```bash
firewall-cmd --query-panic
```

### 开启一个端口(9001)
添加（--permanent永久生效，没有此参数重启后失效）
```bash
firewall-cmd --zone=public --add-port=9001/tcp --permanent
```
重新载入
```bash
firewall-cmd --reload
```
查看
```bash
firewall-cmd --zone=public --query-port=9001/tcp
```
删除
```bash
firewall-cmd --zone=public --remove-port=9001/tcp --permanent
```