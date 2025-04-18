# Chapter 9.2 充分必要原因：识别条件

## 9.2.1 定义、符号和基本关系

```admonish check
### <a id="def9.2.1">定义9.2.1 (必要性概率，PN)</a>
&emsp;&emsp;设 x 和 y 是因果模型M中的两个二值变量， x 和 y 分别代表命题 \\( X = true 和 Y = true，x'与y'表示它们的反值\\)。必要性概率定义为：

$$
\begin{aligned}
    PN &\triangleq P(Y_{x'} = false | X = true, Y = true)  \\\\
       &\triangleq P(y'_{x'} | x,y) 
\end{aligned}
\tag{9.1}
$$
```

&emsp;&emsp;换言之，假设x和y实际上确实已经发生，**PN**代表 \\(y'_{x'}\\)，如若没有事件x，那么事件y不会发生的概率。  
&emsp;&emsp;与7.1节中使用的符号相对比，这里的符号有些细微的变化。小写字母(例如 x 和 y )在7.1节中表示变量的值，但现在表示命题(或事件)。还要注意 \\(y_x\\) 表示 \\(Y_x = true\\) 的简写, \\( y'\_{x} \\) 表示 \\(Y_x = false\\) 的简写。  

```admonish check
### <a id="def9.2.2">定义9.2.2 (充分性概率，PS)</a>  
  
$$
\begin{align}
    PS &\triangleq P(y_x|x',y') \tag{9.2} 
\end{align}
$$

&emsp;&emsp;**PS**度量 x 产生 y 的能力，并且"产生"意味着 x 和 y 从不存在到存在的变换，因此我们对概率 \\(P(y_x)\\)设置了 x 和 y 不存在的条件。于是，**PS**给出了在 x 和 y 不存在的情况下"如若 x 发生， 那么产生 y"的概率，这也反映了 x 的某种必要性(由 **PN**度量)。
```

```admonish check
### <a id="def9.2.3">定义9.2.3 (充分必要性概率，PNS)</a>
&emsp;&emsp;**PNS** 代表 y 在两种情况下对 x 作出响应的概率， 
```

```admonish check
### <a id="cor9.2.6">引理9.2.6 </a>  
因果关系的概率(PNS、PN、PS)满足以下关系：
\\[ PNS = P(x,y)*PN + P(x',y')*PS \tag{9.5} \\] 
**证明**  
用我们的符号可以将一致性条件 \\(X=x \Rightarrow Y_x = y\\) 翻译成  
\\[ x \Rightarrow (y_x=y), x' \Rightarrow (y_{x'}=y) \\]  
因此我们可以写出  

$$
\begin{aligned}
y_x \wedge y'_{x'} &= (y_x \wedge y'{_x{'}}) \wedge (x \vee {x'})  \\\\
                   &= (y \wedge x \wedge y'{_x{'}}) \vee (y_x \wedge y' \wedge x')
\end{aligned}
$$

利用两边取概率和`x与x'`的互斥性，我们得到  

$$
\begin{aligned}
P(y_x , y'_{x'}) &= P(x,y, y'{_x{'}}) + P(y_x , x', y')  \\\\
                 &= P(y'{_x{'}} | x,y )*P(x,y) + P(y_x | x',y')*P(x',y')  \\\\
                 &= PN * P(x,y) + PS * P(x',y')
\end{aligned}
\tag *{$\blacksquare$}
$$
```

## 9.2.2 外生性下的界限与基本关系
[**外生性**](./chapter_7_4.md#def_exogeneity)的重要性依赖于允许识别\\(\\{P(y_x),P(y_{x'})\\}\\)，即 *X* 对 *Y* 的因果效应。

## 9.2.3 单调性和外生性下的可识别性

## 9.2.4 单调性和非外生性下的可识别性

