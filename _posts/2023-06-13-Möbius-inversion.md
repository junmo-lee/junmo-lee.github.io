---
title: "Möbius inversion"
date: 2023-06-13 12:42
description: "None"
categories: [Blog, math]
tags: [matkor]     #lowercase
author: me
math: true
#pin: true
#img_path: /imgs/
#mermaid: true

---
[Möbius function - Wikipedia](https://en.wikipedia.org/wiki/M%C3%B6bius_function)
$\mu (n)$ := 0(n이 1이 아닌 제곱수의 약수를 가질 때), 1(제곱수 약수가 아니면서 소인수들이 짝수개)


[Möbius inversion](https://ahgus89.github.io/algorithm/M%C3%B6bius-inversion/)

$f(n) = \sum_{d\mid n} \mu(n)g(\frac{n}{d})$
$when\quad g(n) =\sum_{d\mid n}f(d)$
곱셈적 함수 f
f(mn) = f(m)f(n), gcd(m,n)=1

$f(n) : mult \rightarrow g(n) :=  \sum_{d\mid n}f(d)$
$g(mn) = \sum_{d\mid mn}f(d) = \sum_{d_{1}\mid m} \sum_{d_{2}\mid n}f(d_{1}d_{2})=\sum_{d_{1}\mid m}f(d_{1})\sum_{d_{2}\mid m}f(d_{2})=g(m/g(n))$




[16409번: Coprime Integers](https://www.acmicpc.net/problem/16409)
2023/1] + 2023/2 +...
$\lfloor \frac{2023}{n} \rfloor - \lfloor \frac{2023}{n+1} \rfloor$(구간 차이가) < 1이 되는 최초의 n을 구하면
1부터 n까지는 중간에 floor값이 들어가므로 서로 다르다는 것, 
나머지는 쭈욱.... + 남은게 하나씩은 있으므로

$\frac{n}{i+1}$가 root n에 근접,
따라서
1~root(n)까지는 직접, 나머지는 root(n)보다  작음, 최대값은 2root(n)

[1,a], [1,b] 구간 : p(a,b)라고 하고
$$p(a,b) = \sum\limits^{a}_{i=1}\sum\limits^{b}_{j=1}[gcd(i,j)=1] =  \sum\limits^{a}_{i=1}\sum\limits^{b}_{j=1}\gamma(gcd(i,j)) =  \sum\limits^{a}_{i=1}\sum\limits^{b}_{j=1} \sum\limits_{d\mid gcd(i,j)}\mu (d) =  \sum\limits^{a}_{d=1}\sum\limits^{b}_{j=1}=\sum\limits^{min(a,b)}_{d=1}\mu(d)\lfloor\frac{a}{d}\rfloor\lfloor\frac{b}{d}\rfloor$$


[a,b],[c,d] 이므로 포함 배제를 이용하여 빼야함
p(b,d) - p(a-1,d) - p(b,c-1) + p(a-1,c-1)



[1792번: 공약수](https://www.acmicpc.net/problem/1792)
위 문제에서 Harmonic Lemma를 이용해
$\mu$ 들의  1부터 sum을 구해서
a-b 까지를 O(1)에 빼기를 통해서 구할 수 있음
