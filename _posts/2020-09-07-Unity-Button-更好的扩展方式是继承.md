---
layout: post
title: Unity Button 更好的扩展方式是继承
date: 2020-09-07 23:31:35
updated:
comments:
tags:
categories:
permalink: 2020-09-07-Unity-Button-更好的扩展方式是继承
---

以前我扩展 Button 组件的方式是再写一个组件，然后在给 Button 组件加上 Event Trigger 组件去处理事件，比如 PointerUp 等。

后来我发现更好的方式是继承 Button 组件，然后重载方法。除了做事件响应外，比如做子对象UI的颜色变换等，也非常方便，

