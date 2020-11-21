---
title: QGIS源码编译
date: 2020-11-18 21:14:18
tags: QGIS
categories: GIS
---

<!--more-->

### 下载软件包

| Tool    | Website                                                      |
| ------- | ------------------------------------------------------------ |
| CMake   | https://cmake.org/files/v3.7/cmake-3.7.2-win64-x64.msi       |
| cygwin  | http://cygwin.com/setup-x86.exe (32bit) or http://cygwin.com/setup-x86_64.exe (64bit) |
| OSGeo4W | http://download.osgeo.org/osgeo4w/osgeo4w-setup-x86.exe (32bit) or http://download.osgeo.org/osgeo4w/osgeo4w-setup-x86_64.exe (64bit) |
| ninja   | https://github.com/ninja-build/ninja/releases/download/v1.7.2/ninja-win.zip |

对于cygwin和OSGeo4W，下载完后都是选择高级安装。

在选包界面的搜索栏输入文档中给出的包名，目前官方文档给出的是：

cygwin

\- bison
\- flex

OSGeo4W:

国内镜像：http://gwmodel.whu.edu.cn/mirrors/osgeo4w

\- qgis-rel-deps另外之后编译的过程中如果发现有缺失的包也是可以重新在这里补充下载的。

![img](J:\B_我的资料\site\11wy11.github.io\source\_posts\qgis-develop-2\70)

直接下一步完成安装即可。

安装完cygwin和OSGeo4W后，将ninja.exe复制到之前安装OSGeo4W目录的OSGeo4W64\bin\下。、

![img](J:\B_我的资料\site\11wy11.github.io\source\_posts\qgis-develop-2\22)

### 编译源码

找到OSGeo4W的安装路径，在下面新建一个文本文档，输入并修改加粗部分为你的源码路径。

@echo off
 call **X:\src\qgis**\ms-windows\osgeo4w\msvc-env.bat x86_64
 @cmd

```
@echo off
 call X:\src\qgis\ms-windows\osgeo4w\msvc-env.bat x86_64
@cmd
```

（【X:\src\qgis】即从GitHub上下载的源码包解压后的位置，实在找不到也可以试试搜索msvc-env.bat这个文件然后根据其路径修改）

将这个文本文档的文件名修改为【OSGeo4W-dev.bat】保存在OSGeo4W的安装目录下，然后运行它。

这是官方文档给出的方法，但是如果直接照做，之前的安装路径又有所修改的话，很可能会报错，例如找不到文件，其实这是因为环境变量没有修改的原因，其实官方文档的方法就是直接调用了msvc-dev.bat这个批处理文件而已，根据这个提示右键编辑查看msvc-dev.bat这个文件。

不难发现，其中涉及到的重要的环境变量主要有：

OSGEO4W_ROOT（OSGeo4W的根目录）

PF86（软件默认安装目录）

VS140COMNTOOLS（调用VS的vcvarsall.bat批处理文件）

GRASS7（这个的路径中是【/】而不是【\】，要注意）

PYTHONPATH（SIP包所在路径）

LIB（OSGeo4W依赖库头文件）

INCLUDE（OSGeo4W静态库文件）

如果之前更改了路径，修改相应的环境变量即可。

其中，VS140COMNTOOLS是VS2015的变量名，如果是像笔者一样使用VS2017的话，还需要将变量名VS140COMNTOOLS改为VS150COMNTOOLS。

------

修改方法：

1、利用批处理文件修改

创建一个文本文件，命名path.bat,内容参考如下，路径换成相应安装路径即可

```
@echo off
set VS150COMNTOOLS = C:\Program Files (x86)\Microsoft Visual Studio\2017\Community\VC\Auxiliary\Build\vcvarsall.bat" x64
set OSGEO4W_ROOT=E:\QGISdevelop\OSGeo4W64
call "%OSGEO4W_ROOT%\bin\o4w_env.bat"
path %PATH%;E:\QGISdevelop\CMAKE\bin;E:\QGISdevelop\cygwin\bin;E:\QGISdevelop\OSGeo4W64\apps\Python36
@set GRASS_PREFIX=E:/QGISdevelop/OSGeo4W64/apps/grass/grass-7.4.1
@set INCLUDE=%INCLUDE%;%OSGEO4W_ROOT%\include
@set LIB=%LIB%;%OSGEO4W_ROOT%\lib;%OSGEO4W_ROOT%\lib
@cmd
```

在CMD中运行这个BAT

官方提供了两种方法，使用Trugonly.cmd创建MSVC解决方案文件或者使用cmake-gui

由于各种路径设置的原因，笔者建议还是使用传统的cmake进行编译

打开之前创建的OSGeo4W-dev.bat

![img](J:\B_我的资料\site\11wy11.github.io\source\_posts\qgis-develop-2\1)

打开cmake-gui，设置好源码路径和要输出的路径，然后点击Configure

![img](J:\B_我的资料\site\11wy11.github.io\source\_posts\qgis-develop-2\2)

另外在CMAKE卡中设置项目要安装的路径，推荐设置在一个新的空目录中，避免导致混乱

![img](J:\B_我的资料\site\11wy11.github.io\source\_posts\qgis-develop-2\3)

出现错误也是正常的，关键还是路径的问题，所以说前面环境变量的设置十分重要。另外在WITH中去掉一些不必要的组件，最最最重要的是DESKTOP，然后就是GUI等一些组件，当然直接使用默认的也基本上可以了。

![img](J:\B_我的资料\site\11wy11.github.io\source\_posts\qgis-develop-2\4)

![img](J:\B_我的资料\site\11wy11.github.io\source\_posts\qgis-develop-2\5)

一步一步的指定缺失的路径，首先是flex和bison

![img](J:\B_我的资料\site\11wy11.github.io\source\_posts\qgis-develop-2\6)

![img](https://img-blog.csdn.net/20180801151521772?watermark/2/text/aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzM0MzU3NzE3/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70)

然后是各个库

![img](J:\B_我的资料\site\11wy11.github.io\source\_posts\qgis-develop-2\7)

我遇到了这个spatialite版本过旧的问题

![img](J:\B_我的资料\site\11wy11.github.io\source\_posts\qgis-develop-2\8)

这时再次打开之前的OSGeo4W安装程序，搜索这个包并进行安装

![img](J:\B_我的资料\site\11wy11.github.io\source\_posts\qgis-develop-2\9)

问题还是没有解决，这时才发现原来是版本选成了VS17的，这里还是要选择VS2015 64位的版本

![img](J:\B_我的资料\site\11wy11.github.io\source\_posts\qgis-develop-2\10)

设置完成后继续点Configure，有错误则设置好需要的路径直到出现

![img](J:\B_我的资料\site\11wy11.github.io\source\_posts\qgis-develop-2\11)

然后点击Generate，其实这三个按钮点依次点过去，没问题的话就OK了，成功的话可以在指定的文件夹中看到编译成功的项目，用VS打开项目并且重新生成就可以了，当然这可能需要比较长的一段时间。

 

![img](J:\B_我的资料\site\11wy11.github.io\source\_posts\qgis-develop-2\12)![img](J:\B_我的资料\site\11wy11.github.io\source\_posts\qgis-develop-2\13)

将活动解决方案设置为RelWithDebInfo，带有调试信息的Release版本。

![img](J:\B_我的资料\site\11wy11.github.io\source\_posts\qgis-develop-2\14)

 

将启动项目设置成【qgis】，选择核心的项目生成即可，这里我参考了https://blog.csdn.net/quinta_2018_01_09/article/details/79084001这篇博客。但通过查看看依赖项我发现【qgis】还需要依赖【qgis_native】这个项目，因此也把它加上去了。

![img](J:\B_我的资料\site\11wy11.github.io\source\_posts\qgis-develop-2\15)

![img](https://img-blog.csdnimg.cn/2018122716553618.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzM0MzU3NzE3,size_16,color_FFFFFF,t_70)

然后单独编译生成【qgis_core】,如果出现以下问题，定位到出问题的cpp文件，利用记事本对其进行编辑（其他方法亦可），将其编码改为【Unicode】，虽然错误看起来很多，但是实际上几条错误都是在同一个文件中的，实际上需要修改的文件并不多，逐一修改即可。成功生成【qgis_core】后，生成其它项目，出现语法错误处理方式同上，最后生成【qgis】项目。

![img](https://img-blog.csdnimg.cn/20181227175610298.png)

![img](https://img-blog.csdnimg.cn/20181227175756127.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzM0MzU3NzE3,size_16,color_FFFFFF,t_70)