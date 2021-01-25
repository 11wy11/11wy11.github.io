---
title: QGIS插件开发学习
date: 2020-12-26 23:09:17
tags: QGIS
categories:
---

python PyQGIS插件开发代码学习片段

<!--more-->

#### QGIS设置支持mdb

点击设置》选项》系统，在环境，勾选使用自定义变量，添加两个环境：

OGR_SKIP ODBC，

PGEO_DRIVER_TEMPLATE DRIVER=Microsoft Access Driver (*.mdb, *.accdb);DBQ=%s

![image-20201226231641904](qgis-develop-6\image-20201226231641904.png)



D:\OSGeo4W64\include;D:\OSGeo4W64\apps\Qt5\include\QtXml;D:\OSGeo4W64\apps\Qt5\include\QtWidgets;D:\OSGeo4W64\apps\Qt5\include\QtQml;D:\OSGeo4W64\apps\Qt5\include\QtGui;D:\OSGeo4W64\apps\Qt5\include\QtPrintSupport;D:\OSGeo4W64\apps\Qt5\include\QtQmlDebug;.\;.\qgslib\ui;D:\OSGeo4W64\apps\gdal-dev\include;D:\OSGeo4W64\apps\Qt5\include\qt5keychain;D:\OSGeo4W64\apps\Qt5\include\QtCrypto;D:\OSGeo4W64\apps\Qt5\include\QtSql;D:\OSGeo4W64\apps\Qt5\include\QtCore;.\qgslib\core;.\qgslib\app\layout;.\qgslib\gui;.\qgslib\app;D:\OSGeo4W64\apps\qgis\include;%(AdditionalIncludeDirectories)

