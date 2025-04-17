# Chapter 9.2 充分必要原因：识别条件

## 9.2.1 定义、符号和基本关系

```admonish check
### <a id="def9.2.1">定义9.2.1 (必要性概率，PN)</a>
&emsp;&emsp;设 *x* 和 *y* 是因果模型 *M* 
```

```admonish check
### <a id="def9.2.2">定义9.2.2 (充分性概率，PS)</a>
&emsp;&emsp;**PS**度量 *x* 产生 *y* 的能力，并且
```

```admonish check
### <a id="def9.2.3">定义9.2.3 (充分必要性概率，PNS)</a>
&emsp;&emsp;**PNS** 代表 *y* 在两种情况下对 *x* 作出响应的概率， 
```

```admonish check
### <a id="thm9.2.6">引理9.2.6 </a>  
因果关系的概率(PNS、PN、PS)满足以下关系：
\\[ PNS = P(x,y)*PN + P(x',y')*PS \\]
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
\end{aligned}
\tag *{$\blacksquare$}
$$
```

## 9.2.2 外生性下的界限与基本关系
[**外生性**](./chapter_7_4.md#def_exogeneity)的重要性依赖于允许识别\\(\\{P(y_x),P(y_{x'})\\}\\)，即 *X* 对 *Y* 的因果效应。

## 9.2.3 单调性和外生性下的可识别性

## 9.2.4 单调性和非外生性下的可识别性

