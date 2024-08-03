---
title: QR分解求矩阵特征值
copyright_author: 找不到服务器
categories:
- 笔记
tags:
- 笔记
- 学习
---
# 豪斯霍尔德变换
&emsp;&emsp;豪斯霍尔德(Householder)变换又称作镜像变换，作用是将任何非零向量$x$变换成另一个向量$y$，且两个向量关于某个平面镜像对称。变换矩阵
$$H=I-\omega\omega^\text{T}$$
称为豪斯霍尔德矩阵，即$Hx=y$，满足
$$H^\text{T}=H^{-1}=H,\ H^\text{T}H=I$$
其中$\omega$是对称平面的单位法向量，从图中可直观看出$x-y=2\omega(\omega^\text{T}x)$。
&emsp;&emsp;因为任何两个长度相等的向量肯定关于一个平面对称，所以可以把任何向量镜像到任何位置，现在要做的是将向量镜像到x轴上，对应的镜像矩阵为
$$H=I-\rho^{-1}uu^\text{T}$$
令$\sigma=\pm||x||_2$即向量$\vec{x}$的长度，则矩阵$H$可以将向量$\vec{x}$变换到x轴上，用$-\sigma\vec{e}_1$表示，如右图所示。$\vec{e}_1$表示x轴上的单位向量。此时$\vec{u}=\vec{x}+\sigma\vec{e}_1$为两个镜像向量的差，$\rho=0.5||u||_2^2=\sigma(\sigma+\alpha_1)$，$\alpha_1$是$\vec{x}$的第一个元素，$\sigma+\alpha_1$是$\vec{u}$的第一个元素。

# 海森堡矩阵
$$\left[\begin{matrix}
x & x & x & x \\
x & x & x & x \\
0 & x & x & x \\
0 & 0 & x & x \\
\end{matrix}\right]$$
&emsp;&emsp;形如上面的矩阵称为海森堡(Hessenberg)矩阵，也就是上三角阵下面再多一排斜对角的元素，也称作拟上三角阵。左下角为0的称为上海森堡阵，右上角为0的称为下海森堡阵。
&emsp;&emsp;任何实的$n$阶方阵$A$可通过镜像变换化为上海森堡阵，变换思路是，每一步把矩阵$A$的每一列的下半部分清零。
&emsp;&emsp;豪斯霍尔德矩阵在具体的迭代中可用于简化迭代所需的矩阵乘法。左乘H矩阵：
