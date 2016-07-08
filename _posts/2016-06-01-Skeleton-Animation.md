---
layout: false
title: Skeleton Animation
date: 2016-06-01 16:33:42
updated:
comments:
tags: Animation
categories:
- Game Develop
permalink:
---
骨骼动画是计算机动画中的一种技术，它把角色分为两部分表示：表现外表的蒙皮(skin or mesh)和控制动作的骨架.

<!--more-->

![蒙皮和骨架](http://imgout.ph.126.net/50675181/Skin+26+Skeleton0Ahttp3A.jpg)

骨架由很多骨骼组成，每个骨骼有一个 transformation（其中包括 position, scale, orientation），还可能有一个父骨骼。整个骨架表现为一个层级结构，每个节点的完整 transform 由其父节点的 transform 和自己的 transform 组成。Rig（泛指所有用骨架控制模型的动画制作方式）通常包含正向运动学和反向运动学。骨骼动画是指 rig 中的正向运动学。

![骨骼计算](http://imgout.ph.126.net/50675182/Deriving+the+skeleton+wo.jpg)

每个骨骼跟角色的一部分视觉表现关联，通常一个骨骼要关联一组顶点，这些顶点用来组成多边形, 以供多边形 mesh 使用。部分蒙皮可以与多个骨骼相连，蒙皮对每个骨骼有一个比例因子(vertex weight or blend weight), 比如相连两个骨骼之间的蒙皮就可以与这两个骨骼关联。这个关联的过程称为 skinning, 现在很多引擎是在 GPU 上用 shader 来完成这个过程。

![骨骼和多边形](http://imgout.ph.126.net/50675195/Geometries+26+skeleton0A.jpg)

对一个多边形 mesh, mesh 上的每个顶点可能对每一个骨骼有一个比例因子。为了计算顶点的最终位置，会对每个骨骼创建一个 transformation 矩阵，先将顶点先放入骨骼空间，再将其放回 mesh 空间。矩阵计算完后，再根据比例因子 scale 顶点，这个算法被称为 **matrix palette skinning**.



骨骼动画没有提供真实的肌肉移动和皮肤移动，要实现这个功能需要使用别的方法。



动作捕捉技术（performance capture or motion capture）能够加快骨骼动画开发速度，而且能够提高真实度。
