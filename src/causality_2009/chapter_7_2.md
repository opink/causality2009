# Chapter 7.2 结构模型的应用与解释

## 7.2.1 线性经济计量模型政策分析：示例
&emsp;&emsp;在[1.4节中，我们利用供需均衡的典型经济问题说明结构方程建模的性质](./chapter_1_4.md#def1.40)。在本章中，我们将使用该问题来回答与策略相关的问题。

...

&emsp;&emsp;... 但是，本书的重点不是参数估计，而是[(因果)参数](#因果参数)在策略预测中的作用。因此，我们将说明如何评估以下三个问题。

- 问题一：如果价格 *被控制* 在 \\(P=p_0\\)，需求Q的期望值是多少？
- 问题二：如果价格 *被报告* 为 \\(P=p_0\\)，需求Q的期望值是多少？
- 问题三：假设当前价格为 \\(P=p_0\\)，如果价格被控制在 \\(P=p_1\\)，那么需求Q的期望值是多少？

&emsp;&emsp;读着应该认识到这三个问题分别代表了行动、预测和反事实。问题二在统计文献中是一个标准的预测问题，可以利用协方差矩阵(线性、正态和独立的假设下)直接进行回答，不涉及因果关系、结构或者不变性的概念。问题一和问题三取决于方程的结构性质，正如预料，在经济学的有关结构方程的文献中没有提及这两个问题的处理方法。

...

## 7.2.2 反事实的实证性内容
&emsp;&emsp;"反事实"这个自然语义的用词是不恰当的，因为它指的是一种与事实相反的说法，或者至少是一种逃避实证性验证的说法。因果结构里的反事实不属于这两类，它是科学思想的基础，与任何科学规律一样具有明确的实证性信息。  
&emsp;&emsp;考虑欧姆定律\\(V = IR\\)。该定律的实证性内容可以用以下两种形式进行描述：
1. 预测形式：如果在时间 t<sub>0</sub> 测得的电流 I<sub>0</sub> 和电压 V<sub>0</sub> ，那么在人和将来的时间 \\(t>t_0\\)，如果电流为\\(I(t)\\)，则电压将为\\[V(t) = \frac{V_0}{I_0} *I(t)\\]
2. 反事实形式：如果在时间 t<sub>0</sub> 测得的电流 I<sub>0</sub> 和电压 V<sub>0</sub> ，那么，如若在时间 t<sub>0</sub> 的电流是\\(I'\\)而不是\\(I_0\\)，则电压应为\\[V' = \frac{V_0*I'}{I_0} \\]  
&emsp;&emsp;从表面上看，预测形式提出了有意义且可检验的实证性内容，而反事实形式则仅仅是对没有(也不可能)发生的事情进行推测，因为不可能同时将两种不同的电流加到同一个电阻上。但是，如果我们将反事实形式恰恰解释为预测形式的简记方式，则反事实的实证性内容就会很清晰地展现出来。这两种方法都使我们能够仅根据一个测量值\\( (I_0, V_0) \\)进行无限次的预测，并且都能从一个科学定律中得出他们的有效性，该定律将随时间不变的特性(比率\\(V/I\\))归因于任何导电物体都存在的现象。  
&emsp;&emsp;但是，如果反事实语句仅仅是一种用于表达预测的迂回方式，那么为什么我们要求助于这种复杂的表达方式而不直接使用预测模式呢？一个显而易见的答案是，我们经常使用反事实来表达的不是预测本身，而是这些预测的逻辑结果。例如，"如若A不开枪，那么囚犯仍将活着"这句话的意图可能仅仅是传达B没有开枪的事实信息。在这种情况下，反事实语气表达的是对一般规律的逻辑论证进行事实补充。此外，一个不太明显的答案在于预测要求其余情况均相同(或均保持不变)，而这并非完全没有歧义。当我们改变电阻器中的电流时，应保持什么条件恒定呢？温度？实验室设备？一天中的时间？当然不是电压表上的读数！  
&emsp;&emsp;当我们对预测的要求作出判断时，必须仔细说明一些条件并认真对待。当我们使用反事实表达式时，有许多条件都是隐含的(因此是多余的)，特别是当我们利用潜在因果模型时。例如，我们不需要指明在什么温度和压力下，这些预测才是正确的。这是由语句"在时间 t<sub>0</sub> 处的电流是 I' 而不是 I<sub>0</sub> "所蕴含的。换句话说，我们所指的是在时间 t<sub>0</sub> 处实验室中普遍存在的条件。这句话还暗示，我们并不是真正想让任何人维持电压表的读数不变。电压应该按照其自然过程运行，根据我们的因果模型，我们所能设想的变化取决于当前决定电流的机制。  
&emsp;&emsp;总而言之，反事实语句可以很好的被解释为在一系列明确定义的条件下所做出的预测，这些条件存在于该语句中的事实部分。为了使这些预测有效，必须保持两个组成部分不变：定律(或机制)以及边界条件。用结构模型语言来说，定律对应于方程{ f<sub>i</sub> }，边界条件对应于背景变量 *U* 的状态(值)。因此，对一个反事实语句进行预测性解释，其有效性的前提条件是假设当我们的预测在应用或检验时， *U* 不会改变。  

## 7.2.3 因果解释、表达及其理解
&emsp;&emsp;众所周知，解释能增进理解力，懂得多的人能更有效地推断和学习。同时，人们普遍认为，解释的概念不能脱离因果的概念。... 

...

&emsp;&emsp;为了解决这一难题，我们必须跨过概率的度量，专注于 <a id="因果参数" style="color:blue">**因果参数**</a> ，例如，因果效应\\( P(y|do(x)) \\) 和反事实概率 \\( P(Y_x = y'|x,y) \\) ，作为定义解释力的基础。...

&emsp;&emsp;这些可能性引出一个重要的本质问题："解释"到底是一个基于一般因果的概念(例如"喝毒药导致死亡")，还是基于特例因果(singular cause)的概念(例如"苏格拉底喝毒药导致他死亡")？即使分为一般因果和特例因果两种解释，其分界仍然是十分模糊。...

...

&emsp;&emsp;第9章和第10章给出了形式化分析方法，讨论了因果关系的必要和充分条件以及特例事件因果关系的概念。

...


## 7.2.4 从机制到行动再到因果
...  
&emsp;&emsp;结构模型回答了这个问题，它假设在一般推断过程中将施加的行动表述为 *局部手术* 。世界由大量自主的、不变的联系或机制组成，每一个联系或机制都对应一个(局部性的)物理过程，这个过程约束一组相对较少的变量集合的行动。...   
&emsp;&emsp;使这种方式具有可操作性的因素是行动的 *局部性* 。...  

## 7.2.5 Simon因果顺序
...  
&emsp;&emsp;因果关系的不对称性与物理方程的对称性完全不冲突。" *X* 导致 *Y* ，而 *Y* 不会导致 *X* "的意思是，更改一个机制(其中" *X* 是因变量")与更改另一个机制(其中" *Y* 是因变量")对结果的影响不同。由于涉及两种不同的机制，因此该语句与我们在物理方程中发现的对称性是完全一致的。  