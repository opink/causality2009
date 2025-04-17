# Chapter 3.5 可识别性的图模型检验

图3.7c展示了另一个有趣的特性是计算联合干预(joint intervention)的效应往往比计算其中单一干预的效应更容易。这里，可以计算\\(P(y|\hat{x},\hat{z}_2)\\)和\\(P(y|\hat{x},\hat{z}_1)\\)，但无法计算\\(P(y|\hat{x})\\) 。  

例如，前者可在  \\(G_{\bar{X}, \underset{\bar{}}{Z}}\\) 中引入`规则2`进行计算：

$$
\begin{aligned}
P(y|\hat{x},\hat{z_2}) &= \sum_{z_1} P(y|z_1, \hat{x}, \hat{z_2}) * P(z_1|\hat{x},\hat{z_2})  \\\\
                       &= \sum_{z_1} P(y|z_1, x, z_2) * P(z_1|x)   \\\\
\end{aligned}
\tag{3.47}
$$


然而,不能使用`规则2`将\\(P(z_1|\hat{x},z_2)\\)转换为\\(P(z_1|x,z_2)\\)，因为当以\\(z_2\\)为条件时，*X* 和 *Z<sub>1</sub>* 在\\(G_{\underset{\bar{}}{X}}\\)中(通过虚线) *d-连通* 。[Pearl和Robins(1995)](#PearlRobins1995)提出的计算联合干预和贯序干预的一般性方法，第4.4节中将会介绍该方法。

## 3.5.1 识别模型
&emsp;&emsp;图3.8展示了 *X* 对 *Y* 的因果效应可识别的简单图(其中 *X* 和 *Y* 是单一变量)。称模型为"识别模型"(identifying model)，因为其结构包含了足够数量的假定(在图上体现为缺失的链接)以使目标值\\(P(y|\hat{x})\\)可识别。  
&emsp;&emsp;通过检查图3.8可以发现如下特性：
1. 由于从因果图中移除人和弧或箭头只能有助于因果效应的可识别性，因此，在图3.8展示的图模型的任何子图上的\\(P(y|\hat{x})\\)仍然可识别。同样的，将观察到的中介变量引入因果图，可能帮助但绝不会阻碍任何因果效应的可识别性。
> (2025-03-20) 上述等价的看：通过实验否定了的因果假定，在相关的图模型中将表达为缺失的链接，引入了[状态转移矩阵的稀疏性【张江组 NPJ Complexity 最新工作：时间倒流和涌现】](https://www.bilibili.com/video/BV1TDfUYgEyA/?share_source=copy_web&vd_source=11141d7b83e628e7a2f8baf703e55130)。  

2. 在图3.8中，现有节点对引入任何额外的弧或剪剪头都会使\\(P(y|\hat{x})\\)不再可识别，从这个意义上讲，这些图是极大的。
## 3.5.2 非识别模型




<span id="PearlRobins1995">**Pearl and Robins 1995,** Probabilistic evaluation of sequential plans from causal models with hidden variables. *Uncertainty in Artificial Intelligence 11*, pages 444-453, Morgan Kaufmann, San Francisco, 1995.</span>