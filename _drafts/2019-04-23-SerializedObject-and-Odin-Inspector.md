---
layout: post
title: Odin Inspector and SerializedObject.
date: 2019-04-23 19:40:04
updated:
comments:
tags:
categories: Game Develop
permalink:
---

Odin 是我最喜欢的 Unity Asset 之一，但我目前只喜欢用 Odin 的 Inspector, 而不爱用它的 Serializer, 规避风险。

<!--more-->

我也很喜欢用 SerializedObject 来做数据存取，这比用 Excel, CSV, JSON, XML 等好用很多。用 SerializedObject 存取数据可以做到很多使用外部数据格式做不到的事情，比如支持像曲线、资源引用这样的数据类型，比如方便地使用自定义数据结构等。而且使用起来非常直观，可以查找 SerializedObject 的引用情况，也不再需要在运行时进行外部数据格式的反序列化，而且运行效率也高，还可以作为资源进行热更新。简直无敌了。

默认情况下 SerializedObject 的 Inspector 界面，贯彻了 Unity Inspector 一贯的丑。这个丑不单只看起来丑，这个丑已经影响到了它的易用性。那丑陋的数组，完全做不了表格的展示。

{% asset_img Unity_inspector_array.png Unity inspector array %}

而 Odin Inspector 的 TableList 正好解决了这个问题：

{% asset_img Odin_TableList.png Odin TableList %}

不论是增查删改，Odin 的 TableList 都比原生的 Inspector 方便很多。

TableList 还有一些比较隐晦的方便之处，比如 SerializedObject 的嵌套。假如你有很多不同种类的子弹，每个子弹上都挂有对应子弹数据的 SerializedObject, 这些 SerializedObject 继承于同一个基类，但是它们是不同的类，它们有不同的字段。多个 SerializedObject 的管理需要一个一个去操作，这样就很繁琐。但是你可以创建一个新的 SerializedObject, 它拥有一个子弹数据基类的数组。默认情况下它的 Inspector 会是这样：

{% asset_img SerializedObject_reference_default.png SerializedObject Reference Default %}

但是如果你给这个数组加上 TableList, 它就变成了：

{% asset_img Odin_TableList.png Odin TableList %}

对 TableList 中的字段进行修改，会应用到嵌套引用的 SerializedObject 中，非常的方便。

TableList 有一个特性，它的列是按照字段名进行排列的，同一个字段名下的每行的数据可能是不同的类型。这有什么用呢？还是在每行是继承于同一个子类的不同类型时有用。比如你有些子弹的速度是恒定的，就是一个 float, 而有些子弹的速度是随时间变化的，那就会是一个曲线。如果把这样的字段都以不同名称列下来，那么这个表格会有很多很多列。但实际上这些字段在同一行只会有一列有数据，虽然说不是一定要这样做，但是可以用这样的方式把它们放在同一列，就像上图的 Speed 和 Damage.

说了这么多 TableList 的用法，再讲一个 Odin 对于数组的改善。假如你设置了很多出生点 transform，你需要把它们序列化到一个数组中，在 Unity 默认情况下，你需要一个一个的进行拖拽。而用了 Odin 之后，你可以将这些出生点 transform 一起拖进 Odin 的数据，它就把所有的 transform 放进数组中了：

{% asset_img Odin_array.png Odin array %}

实际上我对 Odin 并没有太深入的研究，上面就是我平时用得多的一些用法。我认为 Odin Inspector 具有一些优秀插件应该有的特性：

1. 不修改开发者使用 Unity 的方式，而是对 Unity 进行加强；
2. 作为一个编辑器插件，可以轻松插拔，不产生额外的自定义数据；
3. 在细节方面变现出色，把功能做到易用性中，而不是写到文档里。

