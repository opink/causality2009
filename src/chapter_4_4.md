# Chapter 4.4 动态计划的可识别性
&emsp;&emsp;本节基于[Pearl和Robins(1995)](#PearlandRobins1995)的内容，讨论涉及存在无法观测(或不可测量)变量的情况下对计划的概率评估。其中，<a style="color:blue" id = "plan">**计划(planning)**</a> 由若干个并发和贯序行动(concurrent or sequential actions)组成，并且每个行动都可能受该计划中前一个行动的影响。我们建立了一套基于图的准则，用于识别在什么情况下可以仅从可测变量的观测值中预测计划的结果。当满足这个准则时，计划达到既定目标的概率率将以解析解的方式给出。

## 4.4.1 动机
&emsp;&emsp;多数情况下，我们的问题相当于通过观察(已有的)其他计划的表现来评估一个新计划，其中其他计划的决策依据无从知晓。...在流行病学中，计划评估问题称为"带有时变混杂因子的时变治疗(Robins, 1993)"。在人工智能应用中，对这些计划的评估能够使一个主体(Agent)通过观察其他主题的表现进行学习从而完成行动，即使在其他主体行动原因未知的情况下也可以完成学习。如果允许Agent做出行动和观察，那么任务就变得容易得多。在这种情况下，因果图的拓扑结构可以被推断出来(至少部分可被推断出来)，一些以前无法识别的行动结果也可以被确定。  
  
## 4.4.2  识别计划：符号和假设

&emsp;&emsp;我们的目标是通过计算概率\\(P(y|\hat{x}\_{1}, \hat{x}\_{2}, ..., \hat{x}\_{n})\\)来评估无条件计划(条件计划将在11.4.1节中进行分析, 通过重复使用定理4.4.1予以识别)，这个概率代表计划\\( (\hat{x}\_{1}, \hat{x}\_{2}, ..., \hat{x}\_{n}) \\)对结果变量 *Y* 的影响程度。如果对于每个赋值 \\( (\hat{x}\_{1}, \hat{x}\_{2}, ..., \hat{x}\_{n}) \\)，概率\\(P(y|\hat{x}\_{1}, \hat{x}\_{2}, ..., \hat{x}\_{n})\\)可由可观测的变量 \\( \\{X,Y,Z\\} \\)组合的联合分布唯一确定，那么\\(P(y|\hat{x}\_{1}, \hat{x}\_{2}, ..., \hat{x}\_{n})\\)在图G中可识别，控制问题就可识别。

## 4.4.3 识别计划：贯序后门准则
### <a id="thm4.4.1">定理4.4.1 ([Pearl and Robins, 1995](#PearlandRobins1995))</a>
```admonish check
&emsp;&emsp;对于每个1≤k≤n，存在满足以下(贯序后门)条件的协变量集合 *Z<sub>k</sub>* ：  
$$ Z_{k} \subseteq N_{k}  \tag{4.4}$$
(即，*Z<sub>k</sub>* 由 *{X<sub>k</sub>, X<sub>k+1</sub>,..., X<sub>n</sub>}* 的非后代节点组成) 并且  
$$ (Y \perp X_{k} | X_{1}, ... , X_{k-1}, Z_{1}, Z_{2}, ... , Z_{k})_{G\_{\underset{\bar{}}X\_{k} , \bar{X}\_{k+1} ,..., \bar{X}\_{n}}}  \tag{4.5}$$

则概率\\(P(y | \hat{x}\_{1}, \hat{x}\_{2}, ..., \hat{x}\_{n})\\)可识别。当这些条件满足时，该计划的结果为：  
$$
\begin{aligned}
P(y | \hat{x}\_{1}, \hat{x}\_{2}, ..., \hat{x}\_{n}) &= \sum_{z_1,...,z_n} P(y|z_1, ... , z_n , x_1 , ... , x_n) \\\\
& * \prod_{k=1}^{n} P(z_k | z_1,... , z_{k-1}, x_1, ... , x_{k-1})  \\\\
\end{aligned}
\tag{4.6}
$$

```

```admonish check title="定理4.4.1的证明"
&emsp;&emsp;此处给出的证明是基于 *do算子* 的推断规则([定理3.4.1](./chapter_3_4.md#thm3.4.1))，这个规则便于将因果效应公式约简为无hat表达式。
    
&emsp;&emsp;**步骤1**  对于所有 \\(j≥k\\)，条件 **(4.4)** 蕴含\\(Z_{k} \subseteq N_{j}\\)。因此我们可以得到

$$
P(z_k | z_1,... , z_{k-1}, x_1, ... , x_{k-1}, \hat{x}\_{k},\hat{x}\_{k+1}, ..., \hat{x}\_{n}) \\\\
= P(z_k | z_1,... , z_{k-1}, x_1, ... , x_{k-1}) 
$$

因为\\(\\{Z_1 , ... , Z_{k-1}, X_1, ... , X_{k-1}\\}\\)中的任何节点都不可能是集合\\(\\{X_k , ..., X_{n}\\}\\)中任何节点的后代。于是，利用 *do算子* 的 **规则3** ，允许我们从表达式中删除带帽变量。  
  
&emsp;&emsp;**步骤2**  条件 **(4.5)** 允许我们引入 *do算子* 的 **规则2** 并改写为：

$$
P(y | z_1,... , z_{k}, x_1, ... , x_{k-1}, \hat{x}\_{k},\hat{x}\_{k+1}, ..., \hat{x}\_{n}) \\\\
= P(y | z_1,... , z_{k}, x_1, ... , x_{k-1},x_k, \hat{x}\_{k+1}, ..., \hat{x}\_{n}) 
$$

因此，我们得到：

$$
\begin{aligned}
P(y | \hat{x}\_{1}, ..., \hat{x}\_{n}) &= \sum_{z_1} P(y|z_1, \hat{x}\_1, \hat{x}\_2, ..., \hat{x}\_{n}) * P(z_1 | \hat{x}\_1, ..., \hat{x}\_{n}) \\\\
& = \sum_{z_1} P(y|z_1, x_1, \hat{x}\_2, ..., \hat{x}\_{n}) * P(z_1) \\\\
& = \sum_{z_2}\sum_{z_1} P(y|z_1, z_2, x_1, \hat{x}\_2, ..., \hat{x}\_{n}) * P(z_1) * P(z_2 | z_1, x_1, \hat{x}\_2, ..., \hat{x}\_{n}) \\\\
& = \sum_{z_2}\sum_{z_1} P(y|z_1, z_2, x_1, x_2,\hat{x}\_3, ..., \hat{x}\_{n}) * P(z_1) * P(z_2 | z_1, x_1) \\\\
& \vdots \\\\
& = \sum_{z_n} \cdots \sum_{z_2} \sum_{z_1} P(y|z_1, ..., z_n, x_1, ..., x_{n}) \\\\
& * P(z_1) * P(z_2 | z_1, x_1) * \cdots * P(z_n | z_1, x_1, z_2, x_2, ..., z_{n-1}, x_{n-1}) \\\\
& = \sum_{Z_1,...,Z_n} P(y|z_1, ..., z_n, x_1, ..., x_{n}) \prod_{k=1}^{n} P(z_k | z_1, ..., z_{k-1}, x_1, ..., x_{k-1}) \\\\
\end{aligned}
\tag*{$\blacksquare$}
$$
```


***

<span id="PearlandRobins1995">**Pearl and Robins(1995),** Probabilistic evaluation of sequential plans from causal models with hidden variables. *Uncertainty in Artificial Intelligence 11*, pages 444-453. Morgan Kaufmann, San Francisco, 1995.</span>