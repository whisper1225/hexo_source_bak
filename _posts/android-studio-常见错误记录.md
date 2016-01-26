---
title: android studio 常见错误记录(持续更新)
date: 2016-01-24 22:51:19
tags:
	- android studio
	- 错误记录
---
android studio 常见错误记录(持续更新)
<!--more-->
### **2016年1月24日22:53:51**
1. 错误现象
我从我们组的git服务器pull代码下来之后出现这个错误
Error:Plugin is too old,
please update to a more recent version, or set ANDROID_DAILY_OVERRIDE envir
> 解决办法： 修改工作空间的gradle文件的classpath的工具版本，我的是从2.0.0.0-alpha3降级到1.5就行了
