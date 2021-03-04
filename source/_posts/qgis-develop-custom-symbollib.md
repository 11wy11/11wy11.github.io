---
title: QGIS自定义符号库
date: 2021-03-03 22:05:10
tags: QGIS
categories: QGIS
---

QGIS 资料收集总结

<!--more-->



# 1.qgis自定义符号库

转载:https://blog.csdn.net/wywywywywywy123456/article/details/66971218

地图符号作为地图语言；抽象描述的客观世界并用直观、生动视觉的手段向我们传递地理信息。每款GIS软件都会自带一些常见的地图符号，也可以自定义地图符号。一般做专题地图那些常规符号库就不能满足我们。

在使用qgis时候发现自带地图符号少的可怜而且又不美观。于是我引进第三方地图符号；由于qgis自定义允许svg格式我去mapbox官网下载一套svg格式。svg网上资源还是蛮丰富的；加载qgis里只要设置一下路径可以。

![img](qgis-develop-custom-symbollib/20170327151252041)

右击Properties选择样式类型SVG。

![img](qgis-develop-custom-symbollib/20170327151429451)

当然可以通过lnkscape软件来做符号，然后在保存SVG格式。

![img](qgis-develop-custom-symbollib/20170327152341462)

也可以写XML文件来添加地图符号。
![img](qgis-develop-custom-symbollib/20170327152759185)

![img](qgis-develop-custom-symbollib/20170327153028412)



参考资料

http://docs.qgis.org/2.14/en/docs/training_manual/basic_map/symbology.html

https://www.mapbox.com/maki-icons/
https://thenounproject.com/

https://mapicons.mapsmarker.com/

# 2.QGIS切换在线地图服务的地图样式

转载：https://blog.csdn.net/weixin_29002209/article/details/112558162


底图是栅格瓦片服务，所以我们不能对其内容进行控制，更不能对其标注进行修改。不过这一切，在最新的QGIS中，借助一个插件，就可以实现底图效果的自定义了，不仅可以修改不同图层的样式，还可以直接将不想要的图层、标注直接关掉。

**插件MapTiler**


默认提供了7种地图样式，你可以在这些基础上进行改造。我使用最多的是Basic、Streets和Toner。


需要你输入一个Key才行。点击面板中的地址自己申请一个就可以啦。

申请完毕填上后，数据就可以加载到工程中啦。


此时，我们在图层树上选择所加载的图层，右侧就会出现其对应的设置面板。新添加的底图服务面板中，都是每一个可以设置的图层，可以对其进行开关勾选，更可以对其进行样式设置。然，不仅可以对图层效果进行设置，对图层标注也是可以修改的。


