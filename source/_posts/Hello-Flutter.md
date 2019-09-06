---
title: Hello Flutter
copyright: true
date: 2019-09-06 08:08:03
tags:
categories: Flutter
---



[TOC]

> 距离上次的更新又过去了半年，我这个懒癌还真的有点严重呢。时间跨度比较大，那么发生的事情也就比较多，现在的我，跟半年前的我相比，又有了很多变化，尤其是思想和心态上，这次想学一下Flutter，希望能拿出全身100%的努力，来做成这件事


这半年发生了很多事，对我来说也算是一种磨难。之前一些想法现在也慢慢的在改变，感觉到了交流沟通的重要性，想改变自己在人际交往上的一些之前比较消极的观点和做法，我想变成一个全新的我，来迎接接下来遇到的困难和磨难。
目前Flutter正在愈演愈烈，各种文章满天飞，身在其中，我也想尝试下新的技术，今天从入门开始做起

# 新的征程
前人种树，后人乘凉。这次也是在前人的总结基础上，来总结学习Flutter，在Github上找到了开源的Flutter电子书，真的很感谢
[Flutter实战][1]

## 拥抱Flutter

flutter的一些特性就不说了，这里开始搭建flutter的开发环境，让我们拥抱Flutter吧

- 下载FlutterSDK
我这里使用的git `git clone -b master https://github.com/flutter/flutter.git`
- 更新环境变量
在Path下，将 `flutter\bin` 的全路径添加到最后作为它的值，不要忘记与其他值使用；分隔开.
- 运行 flutter doctor命令
在Flutter命令行运行如下命令来查看是否还需要安装其它依赖，如果需要，安装它们
该命令检查你的环境并在命令行窗口中显示报告。Dart SDK已经在打包在Flutter SDK里了，没有必要单独安装Dart。 仔细检查命令行输出以获取可能需要安装的其他软件或进一步需要执行的任务。
- AndroidStudio设置
下载安装Flutter插件和Dart插件，并重新运行

如果一切都ok，那么接下来就可以新建一个Flutter项目并运行了

## 遇到的一些问题
1. 刚开始可能有在flutter项目下无法连接设备的情况出现，这个时候要看一下AndroidSDK是否配置好了


[1]: https://book.flutterchina.club/