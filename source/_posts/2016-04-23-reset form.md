---
title: reset form
date: 2016-04-23 00:45:58
tags:
  - css
categories:
  - css
---
## reset输入框
```css
input{
  border: none;
  outline: 0;
  background: none;
  box-sizing: border-box;// 固定width & height
  -webkit-tap-highlight-color: rgba(255,255,255,0);// 取消点击高亮默认效果
  -webkit-appearance:none;// 移除原生控件样式
}
```
<!--more-->

## reset select
```css
select{
  display: block;
  width: 100%;
  height: 70px;
  padding: 0 20px;
  font-size: 24px;
  color: #555;
  background-color: #fff;
  background-image: none;
  border: 1px solid #ccc;
  border-radius: 4px;
  box-shadow: inset 0 1px 1px rgba(0,0,0,.075);
  transition: border-color ease-in-out .15s,box-shadow ease-in-out .15s;
}
```