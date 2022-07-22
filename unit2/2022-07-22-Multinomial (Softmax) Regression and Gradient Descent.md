---
layout: single
title:  "Multinomial (Softmax) Regression and Gradient Descent"
categories: MachineLearning
tag : 정리
toc : true
use_math : true
---



# Computing Probabilites for Softmax



각 data point  $x^{(i)}$ 에 대하여, $j$ ($j = 0,1,\cdots,k-1$ )로 분류 될 확률을 계산 할 수 있다.

어떤 $x$ 벡터에 대하여 softmax 함수 $h$ 를 다음과 같이 정의하면 각 라벨로 분류될 확률을 계산 할 수 있다.


$$
\begin {eqnarray}
h(x) = \frac{1}{\sum _{j=0}^{k-1} e^{\theta _ j \cdot x / \tau }} \begin{bmatrix}  e^{\theta _0 \cdot x / \tau } \\ e^{\theta _1 \cdot x / \tau } \\ \vdots \\ e^{\theta _{k-1} \cdot x / \tau } \end{bmatrix},
\end {eqnarray}
$$
  

하지만 $e^{\theta_j \cdot x/ \tau}$ 항은 매우 클 수도 작을 수도 있으므로 overflow error를 발생시킬 수 있으므로 적당한 값을 지수에서 빼도록 할 것이다.

$$
\begin {eqnarray}
h(x) = \frac{e^{-c}}{e^{-c}\sum _{j=0}^{k-1} e^{\theta _ j \cdot x / \tau }} \begin{bmatrix}  e^{\theta _0 \cdot x / \tau } \\ e^{\theta _1 \cdot x / \tau } \\ \vdots \\ e^{\theta _{k-1} \cdot x / \tau } \end{bmatrix} \\ = \frac{1}{\sum _{j=0}^{k-1} e^{[\theta _ j \cdot x / \tau ] - c}} \begin{bmatrix}  e^{[\theta _0 \cdot x / \tau ] - c} \\ e^{[\theta _1 \cdot x / \tau ] - c} \\ \vdots \\ e^{[\theta _{k-1} \cdot x / \tau ] - c} \end{bmatrix},
\end {eqnarray}
$$


여기에서 적당한 상수 $c$를 잡아준다.( $c = \max _ j \theta _ j \cdot x / \tau$ )

 