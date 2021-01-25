---
title: QGIS 文件结构解析及符号化类结构解析
date: 2021-01-02 11:43:08
tags: QGIS
categories: GIS
---

分析QGS文件格式及符号及注记组织结构

<!--more-->

### QGS 文件结构

#### QGS xml结构

![](qgis-develop-filestruct/qgstoplevel.png)

#### ProjectLayers 结构

包括图层属性，符号规则，注记规则

![](qgis-develop-filestruct\qgsprojectlayers.png)

#### QLR 图层定义文件

![qlr](qgis-develop-filestruct/qlr.png)

#### QML文件

![qml](qgis-develop-filestruct/qml.png)

### MapLayer

StyleCategory

![image-20210103220709620](qgis-develop-filestruct/image-20210103220709620.png)

QgsMapLayerStyleManager

管理与一个地图层一起使用的样式。

存储的样式由其名称标识。管理器始终跟踪当前处于活动状态的已存储样式。更改当前样式后，新样式将应用于关联的图层。

QgsMapLayerStyleManagerWidget

#### QgsSymbolLayer

property

| PropertySize                         | 符号大小。                         |
| ------------------------------------ | ---------------------------------- |
| PropertyAngle                        | 符号角度。                         |
| PropertyName                         | 名称，例如简单标记的形状名称。     |
| PropertyFillColor                    | 填色。                             |
| PropertyStrokeColor                  | 描边颜色。                         |
| PropertyStrokeWidth                  | 行程宽度。                         |
| PropertyStrokeStyle                  | 笔触样式（例如，实线，虚线）       |
| PropertyOffset                       | 符号偏移量。                       |
| PropertyCharacter                    | 字符，例如用于字体标记符号层。     |
| PropertyWidth                        | 符号宽度。                         |
| PropertyHeight                       | 符号高度。                         |
| PropertyPreserveAspectRatio          | 保留宽度和高度之间的长宽比。       |
| PropertyFillStyle                    | 填充样式（例如，实心，点）         |
| PropertyJoinStyle                    | 线联接样式。                       |
| PropertySecondaryColor               | 次要颜色（例如用于渐变填充）       |
| PropertyLineAngle                    | 线角或哈希线符号的哈希线角度。     |
| PropertyLineDistance                 | 行之间的距离，或散列线符号的行长。 |
| PropertyGradientType                 | 渐变填充类型。                     |
| PropertyCoordinateMode               | 渐变坐标模式。                     |
| PropertyGradientSpread               | 梯度扩散模式。                     |
| PropertyGradientReference1X          | 渐变参考点1 x。                    |
| PropertyGradientReference1Y          | 梯度参考点1 y。                    |
| PropertyGradientReference2X          | 渐变参考点2 x。                    |
| PropertyGradientReference2Y          | 梯度参考点2 y。                    |
| PropertyGradientReference1IsCentroid | 渐变参考点1是质心。                |
| PropertyGradientReference2IsCentroid | 渐变参考点2为质心。                |
| PropertyBlurRadius                   | Shapeburst模糊半径。               |
| PropertyShapeburstUseWholeShape      | Shapeburst使用整个形状。           |
| PropertyShapeburstMaxDistance        | 边缘距离处的Shapeburst填充。       |
| PropertyShapeburstIgnoreRings        | Shapeburst忽略环。                 |
| PropertyFile                         | 文件名，例如svg文件。              |
| PropertyDistanceX                    | 点之间的水平距离。                 |
| PropertyDistanceY                    | 点之间的垂直距离。                 |
| PropertyDisplacementX                | 水平位移。                         |
| PropertyDisplacementY                | 垂直位移。                         |
| PropertyOpacity                      | 不透明度。                         |
| PropertyCustomDash                   | 自定义破折号模式。                 |
| PropertyCapStyle                     | 线帽样式。                         |
| PropertyPlacement                    | 线标记放置。                       |
| PropertyInterval                     | 行标记间隔。                       |
| PropertyOffsetAlongLine              | 沿线偏移。                         |
| PropertyAverageAngleLength           | 长度到平均符号角度。               |
| PropertyHorizontalAnchor             | 水平锚点。                         |
| PropertyVerticalAnchor               | 垂直锚点。                         |
| PropertyLayerEnabled                 | 是否启用符号层。                   |
| PropertyArrowWidth                   | 箭头尾巴宽度。                     |
| PropertyArrowStartWidth              | 箭头尾部开始宽度。                 |
| PropertyArrowHeadLength              | 箭头长度。                         |
| PropertyArrowHeadThickness           | 箭头的厚度。                       |
| PropertyArrowHeadType                | 箭头类型。                         |
| PropertyArrowType                    | 箭头类型。                         |
| PropertyOffsetX                      | 水平偏移。                         |
| PropertyOffsetY                      | 垂直偏移。                         |
| PropertyPointCount                   | 点数。                             |
| PropertyRandomSeed                   | 随机数种子。                       |
| PropertyClipPoints                   | 标记是否应修剪到多边形边界。       |
| PropertyDensityArea                  | 密度区域。                         |
| PropertyFontFamily                   | 字体系列。                         |
| PropertyFontStyle                    | 字体样式。                         |
| PropertyDashPatternOffset            | 虚线图案偏移量。                   |

#### QgsSymbol

![dir_66f89767e42cf8b00ce6054c6b00ac7c_dep](qgis-develop-filestruct/dir_66f89767e42cf8b00ce6054c6b00ac7c_dep.png)

![qgssymbol_8h__incl](qgis-develop-filestruct/qgssymbol_8h__incl.png)

#### 整体功能结构

![dir_aebb8dcc11953d78e620bbef0b9e2183_dep](qgis-develop-filestruct/dir_aebb8dcc11953d78e620bbef0b9e2183_dep.png)