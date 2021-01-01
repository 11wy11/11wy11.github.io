---
title: QGIS二次开发-配置python环境
date: 2020-12-07 14:42:14
tags: QGIS
categories: GIS
---

使用QGIS PluginBuilder 来创建Python模板的qgis 插件

<!--more-->

## Plugin Builder 创建插件

创建完成后，如果提示没有pyrcc5，

```
pyuic5 -o WYFirstPlugin_dialog.py WYFirstPlugin_dialog_base.ui
pyrcc5 -o resources.py resources.qrc
```

#### 使用QGIS控制台脚本 python查看application

查看安装路径

QgsApplication.prefixPath()