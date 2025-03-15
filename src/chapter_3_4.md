# Chapter 3.4 干预的计算
&emsp;&emsp;本节建立了一套推断规则，通过这些规则，可以将包含干预和观察的概率性命题转换成其他此类命题，从而提供一种推导(或验证)干预断言的句法方法。每个推断规则都将*do*(·)操作一种修改底层模型中某些选择函数的干预。从这种解释中产生的推断规则称为*do算子*(*do* calculus, *do*演算)公理。  
&emsp;&emsp;假定我们有一个因果图G的结构，其中一些节点是可观测的，而另一些节点是不可观测的。我们的目标是要得到形如\\(P(y|\hat{x})\\)的因果效应表达式的语句推导，其中*X*和*Y*代表观测变量的任意子集。对于“推导”，我们的意思是将表达式\\(P(y|\hat{x})\\)逐步约减为包含观察值的标准概率等式。只要这种约减可行，*X*对*Y*的因果效应是可识别的(参见[定义3.2.4](./chapter_3_2.md#def3.2.4))。
## 3.4.1 符号准备

## 3.4.2 推断规则
下面的定理陈述了本节提出的演算的三个基本推断规则。[Pearl(1995a)](#Pearl1995a)给出了证明。
### <a id="thm3.4.1">定理3.4.1(*do*算子准则)</a>
令G表示如[式(3.2)](./chapter_3_2.md#form3.2)定义的与因果模型对应的有向无环图，令P(·)表示该模型蕴含的概率分布。对于任何不相交的变量子集*X*, *Y*, *Z*, *W*, 我们有以下三条规则：

```admonish check
#### 规则1 (插入 / 删除 观测变量)
&emsp;&emsp;当\\( (Y \perp Z | X , W)_{G\_\bar{X}}\\) 时,  \\(P(y | \hat{x}, z, w) = P(y | \hat{x}, w)\\) &emsp;&emsp; ...... &emsp;&emsp; (3.3.1)

#### 规则2 (行为 / 观察 交换)
&emsp;&emsp;当\\( (Y \perp Z | X , W)_{G\_{\bar{X} , \underset{\bar{}}{Z} } }\\) 时,  \\(P(y | \hat{x}, \hat{z}, w) = P(y | \hat{x}, z, w)\\) &emsp;&emsp; ...... &emsp;&emsp; (3.3.2)


#### 规则3 (插入 / 删除 行为)
&emsp;&emsp;当\\( (Y \perp Z | X , W)_{G\_{\bar{X} , \overline{Z(W)} } }\\) 时,  \\(P(y | \hat{x}, \hat{z}, w) = P(y | \hat{x}, w)\\) &emsp;&emsp; ...... &emsp;&emsp; (3.3.3)  

&emsp;&emsp;其中Z(W)是在\\(G_\bar{X}\\)中属于*Z*但不属于*W祖代*的节点集合。  

```

&emsp;&emsp;每一条推断规则都遵循"带帽"操作符\\(\hat{x}\\)的基本解释，即将连接*X*与干预前父代变量的因果机制替换为干预后引入的新机制X=x，得到由子图\\(G_\bar{X}\\)刻画的*子模型(submodel)*(Spirtes等人(1993)将其命名为"操作后的图")。  
&emsp;&emsp;规则1重申了 *d-分离* 是干预 *do(X = x)* (因此得到图\\(G_\bar{X}\\))所产生的分布中条件独立性的有效检验。这一规则遵循这样的事实：从系统中删除方程不会在剩余的干扰项之间引入任何依赖关系。


<span id="Pearl1995a">**Pearl 1995a,** Causal diagrams for empirical research.*Biometrika*, 82(4):669-710,December 1995.</span>

<span id="Pearl1995b">**Pearl 1995b,** Causal inference from inderect experiments.*Artificial Interlligence in Medicine*, 7(6):561-582, 1995.</span>