---
title: test LaTex
date : 2023-05-12
description: "None"
categories: [Blog, writing]
tags: [writing,LaTex]
author: me
math: true
---
```
기본 헤더
---
title: TITLE
date: YYYY-MM-DD HH:MM:SS +/-TTTT
categories: [TOP_CATEGORIE, SUB_CATEGORIE]
tags: [TAG]     # TAG names should always be lowercase
---
```
테그의 문법이 조금 다르니까 나중에 변환해서 하는것도 ㄱㅊ을듯

imgur... 굳이 안써도 그냥 로컬로 가능하다.. 그저 빛
일단 imgur를 계속 써보고 나중에 cdn 만들기
img_path: /img/path/
author: me



latex가 어떨때 되는지 실험

1.in-line
reference
```
Lorem ipsum $$ f(x) = x^2 $$.
```
Lorem ipsum $$ f(x) = x^2 $$
test 1 :  $$test \ no \ space$$

test 2: $$ start \ and \ end \ space $$
```
$$ start \ and \ end \ space $$
```

test 3:
$$ test \ α / \beta  $$

```
$$ test \ α / \beta  $$
```

2.block 
reference
```
$$
\begin{aligned} %!!15
  \phi(x,y) &= \phi \left(\sum_{i=1}^n x_ie_i, \sum_{j=1}^n y_je_j \right) \\[2em]
            &= \sum_{i=1}^n \sum_{j=1}^n x_i y_j \phi(e_i, e_j)            \\[2em]
            &= (x_1, \ldots, x_n)
               \left(\begin{array}{ccc}
                 \phi(e_1, e_1)  & \cdots & \phi(e_1, e_n) \\
                 \vdots          & \ddots & \vdots         \\
                 \phi(e_n, e_1)  & \cdots & \phi(e_n, e_n)
               \end{array}\right)
               \left(\begin{array}{c}
                 y_1    \\
                 \vdots \\
                 y_n
               \end{array}\right)
\end{aligned}
$$
```
$$
\begin{aligned} %!!15
  \phi(x,y) &= \phi \left(\sum_{i=1}^n x_ie_i, \sum_{j=1}^n y_je_j \right) \\[2em]
            &= \sum_{i=1}^n \sum_{j=1}^n x_i y_j \phi(e_i, e_j)            \\[2em]
            &= (x_1, \ldots, x_n)
               \left(\begin{array}{ccc}
                 \phi(e_1, e_1)  & \cdots & \phi(e_1, e_n) \\
                 \vdots          & \ddots & \vdots         \\
                 \phi(e_n, e_1)  & \cdots & \phi(e_n, e_n)
               \end{array}\right)
               \left(\begin{array}{c}
                 y_1    \\
                 \vdots \\
                 y_n
               \end{array}\right)
\end{aligned}
$$

그냥 시작 :
$$
\overline{GH}=\left[ \dfrac{2}{3}\left( x_{i}+x_{j}\right) \right] ^{2} + \left[ \dfrac{2}{3}\left( y_{i}+y_{j}\right) \right] ^{2}
$$
```
$$
\overline{GH}=\left[ \dfrac{2}{3}\left( x_{i}+x_{j}\right) \right] ^{2} + \left[ \dfrac{2}{3}\left( y_{i}+y_{j}\right) \right] ^{2}
$$
```
start \\begin{aligned}

$$
\begin{aligned}
\overline{GH}=\left[ \dfrac{2}{3}\left( x_{i}+x_{j}\right) \right] ^{2} + \left[ \dfrac{2}{3}\left( y_{i}+y_{j}\right) \right] ^{2}
\end{aligned}
$$

```
$$
\begin{aligned}
\overline{GH}=\left[ \dfrac{2}{3}\left( x_{i}+x_{j}\right) \right] ^{2} + \left[ \dfrac{2}{3}\left( y_{i}+y_{j}\right) \right] ^{2}
\end{aligned}
$$
```

워크플로우?
(로컬 이미지가 있다면 로컬이미지도 같이)
마크다운 rsyn로 넣기
태그 형태가 달라서 tag: a,b,c → tag: \[a,b,c] 로 감싸는 스크립트 만들어서 실행시킨다음(항상 6번째줄)
bundle exec jekyll serve
