---
title: QGIS改造源代码
date: 2021-03-02 22:24:51
tags: QGIS
categories: QGIS
---

<!--more-->

1、利用uic.exe 手动生成ui头文件

配置过环境变量QTDIR之后，可以在命令行中使用uic命令

uic "src\ui\qgisapp.ui" -o ".\ms-windows\osgeo4w\build-qgis-test-x86_64\src\ui\ui_qgisapp.h"

2.利用moc.exe 编译出cpp文件

**moc.exe" "自定义的.h" -o "moc_xxx.cpp"**