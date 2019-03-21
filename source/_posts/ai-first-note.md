---
title: AI组件开发（一）--注记旋转矩阵
date: 2019-03-14 10:56:02
tags: 
  - AI  
categories: AI组件开发
---
## SDK官方帮助文档
AIAPI void(* AIRealMathSuite::AIRealMatrixSet)(AIRealMatrix *m, AIReal a, AIReal b, AIReal c, AIReal d, AIReal tx, AIReal ty)
Sets the scale, rotation, and translation values of a transformation matrix. 
Parameters:
m The matrix object.   
a New a value.   
b New b value.   
c New c value.  
d New d value.   
tx New horizontal translation value.   
ty New vertical translation value.  
## 参数及原理分析 
ad缩放bc旋转tx,ty位移，基础的2D矩阵
 公式
 
    x=ax+cy+tx
    y=bx+dy+ty
为了把二维图形的变化统一在一个坐标系里，引入了齐次坐标的概念，即把一个图形用一个三维矩阵表示，其中第三列总是(0,0,1)，用来作为坐标系的标准。所以所有的变化都由前两列完成
以上参数在矩阵中的表示为：

 |a    b    0|

 |c    d    0|

 |tx   ty   1|

 

运算原理：原坐标设为（X,Y,1）;

                            |a    b    0|

       [X，Y,  1]           |c    d    0|     =     [aX + cY + tx   bX + dY + ty  1] ;

                            |tx    ty  1|

通过矩阵运算后的坐标[aX + cY + tx   bX + dY + ty  1]，我们对比一下可知：

1. 第一种：设a=d=1, b=c=0.  平移

[aX + cY + tx   bX + dY + ty  1] = [X  + tx  Y + ty  1];

可见，这个时候，坐标是按照向量（tx，ty）进行平移

2. 第二种：设b=c=tx=ty=0.  缩放

[aX + cY + tx   bX + dY + ty  1] = [aX    dY   1];

可见，这个时候，坐标X按照a进行缩放，Y按照d进行缩放，a，d就是X，Y的比例系数

3. 第三种：设tx=ty=0，a=cosɵ，b=sinɵ，c=-sinɵ，d=cosɵ。旋转

[aX + cY + tx   bX + dY + ty  1] = [Xcosɵ - Ysinɵ    Xsinɵ + Ycosɵ  1] ;

                            |cosɵ    -sinɵ   0|

                            |sinɵ    cosɵ    0|    

                            | 0       0      1 |


可见，这个时候，ɵ就是旋转的角度，逆时针为正，顺时针为负
4. 第四种：设tx=ty=0，a=1，b=0，c=-sinɵ，d=cosɵ。倾斜
[aX + cY + tx   bX + dY + ty  1] = [ - Ysinɵ    Ycosɵ  1] ;

                            |1        0       0|

                            |-sinɵ    cosɵ    0|    

                            | 0       0       1 |

可见，这个时候，ɵ就是倾斜的角度，逆时针为正，顺时针为负
