---
date: 2023-08-30
share: true
title: Aproksymacja Pade
parent: Matematyka
mathjax: "true"
---
# Aproksymacja Pade
---

Klasyczna aproksymacja $n$-tego rzędu funkcji \(f(x)\) w okolicy punku $a$ za pomocą szeregu Taylora, ma tendencje do zwiększania niedokładności ekstrapolacji wartośći do + lub - nieskończoności.

$$
g(x) = f(a) + \frac{x-a}{1!}\cdot \left.\frac{\partial f}{\partial x}\right|_{x=a}+\frac{\left(x-a\right)^2}{2!}\cdot \left.\frac{\partial^2 f}{\partial x^2}\right|_{x=a}+\cdots + \frac{\left(x-a\right)^n}{n!}\cdot \left.\frac{\partial^n f}{\partial x^n}\right|_{x=a}
$$

Aproksymacją które jest żadziej stosowana i posiada lepsze właściwości przy oddalaniu się od okolicy punktu $a$ (ekstrapolacji) jest aproksymacja Pade rzedu $N+M$ za pomocą ilorazu dwóch wielomianów. 

$$g(x)=\frac{\sum_{i=0}^N A_i \cdot x^i}{\sum_{j=0}^M B_j \cdot x^j}$$
Współczynniki aproksymacji wyznacza się przyrównująć wzory na aproksymację szeregiem Taylora rzeczy N+M z aproksymacją Pade rzeduę N+M

$$ \frac{\sum_{i=0}^N A_i \cdot x^i}{\sum_{j=0}^M B_j \cdot x^j} = f(a) + \sum_{k-1}^{N+M} \frac{\left(x-a\right)^k}{k!} \cdot \left.\frac{\partial^k f}{\partial x^k}\right|_{x=a}$$
Mnożąc obiestrony przez wielomian $B$ otrzymujemy rownanie który aby było spełnione współczynniki przy kolejnych potęgach wielomianu po obu strona muszą być sobie równe aż do rzędu $N+M$

Bez utraty ogólności można przyjąć iż $B_1=1$ ponieważ w aproksymacji Pade móżna podzielić oba wielomiany przez wartość $B_1$ 

$$g(x)=\frac{\sum_{i=0}^N \frac{A_i}{B_1} \cdot x^i}{\sum_{j=0}^M \frac{B_j}{B_1} \cdot x^j}$$
i zmianić oznaczenia uzyskanych wartośći na orginalne

$$g(x)=\frac{\sum_{i=0}^N A_i \cdot x^i}{1+\sum_{j=1}^M B_j \cdot x^j}$$
## Przykład
---
Dla przykładu wyznaczmy aproksymację funksi $sinus$ w okolicy $0$
$$f(x) = sin(x)$$
$$g(x) = x-\frac{x^3}{6} + O(x^5)$$
gdzie notacja $O(x^5)$ oznacza iż ignorujemy w aproksymacji wszystkie czynniki większe równe piątej potędzę
$$\frac{A_0+A_1 \cdot x +A_2 \cdot x^2}{1 + B_1 \cdot x + B_2 \cdot x^2} = x-\frac{x^3}{6} + O(x^5)$$
Mnożąc obie strony przez wielomian B otrzymujemy
$$A_0+A_1 \cdot x +A_2 \cdot x^2 = \left(1 + B_1 \cdot x + B_2 \cdot x^2\right)\cdot \left(x-\frac{x^3}{6} + O(x^5)\right)$$
$$A_0+A_1 \cdot x +A_2 \cdot x^2 == x + B_1 \cdot x^2 + B_2 \cdot x^3 - \frac{x^3}{6} - B_1 \cdot \frac{x^4}{6} - B_2 \cdot \frac{x^5}{6})$$
gdzie czynniki powyżej $x^4$ możmy pominąć
$$A_0+A_1 \cdot x +A_2 \cdot x^2 == x + B_1 \cdot x^2 + B_2 \cdot x^3 - \frac{x^3}{6} - B_1 \cdot \frac{x^4}{6}$$
Równość wielomianów po lewej i prawej stronie prowadzi do następującego układu równań
$$\left\{\begin{matrix}
A_0&=0\\
A_1&=1\\
A_2&=B_1\\
0&=B_2 - \frac{1}{6}\\
0&=B_1
\end{matrix}\right.$$
Czyli aproksymacja Pade stopnia $2+2$ dana jest wzorem
$$g(x)=\frac{x}{1+\frac{x^2}{6}}$$

```tikz
\usepackage{tikz}
\usetikzlibrary{math}
\begin{document}
  \begin{tikzpicture}
  \tikzmath{
    function funtest(\x) {
      return 1.0*sin((\x*180/3.141592));
    };
    function funtest2(\x) {
      return \x / (1 + \x*\x / 6.0);
    };
    function funtest3(\x) {
      return \x - (\x*\x*\x / 6.0);
    };
  }
  %===========================================
  \draw[->] (-2.5,+0.0) -- (+5.0,+0.0) node[below right] {$x$};
  \draw[->] (+0.0,-1.5) -- (+0.0,+2.0) node[above] {$f(x)$};
  
  \draw[scale=1.0,domain=-2.0:4.5,smooth,variable=\x,red,thick] plot ({\x},{funtest(\x*2.0)});
  \draw[scale=1.0,domain=-2.0:4.5,smooth,variable=\x,red,dashed] plot ({\x},{funtest2(\x*2.0)});
  \draw[scale=1.0,domain=-1.5:1.5,smooth,variable=\x,green,dashed] plot ({\x},{funtest3(\x*2.0)});
  
  %\draw[-] (-1.0,-0.1)--(-1.0,+0.1) node[above left] {$t_0$};
  %\draw[-,dashed] (-1.0,0.0) -- (-1.0,-0.6);
  %\draw[<->] (-1.0,-0.6) -- (0.0,-0.6) node[midway,below] {$\phi_0$};
  \end{tikzpicture}
\end{document}
```



