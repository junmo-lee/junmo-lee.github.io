---
title: "Lifting The Exponents"
date: 2023-06-08 12:11
description: "None"
categories: [Blog, math]
tags: [math]     #lowercase
author: me
math: true
#pin: true
#img_path: /imgs/
#mermaid: true

---

[페르마 두 제곱수 정리 - 위키백과, 우리 모두의 백과사전](https://ko.wikipedia.org/wiki/%ED%8E%98%EB%A5%B4%EB%A7%88_%EB%91%90_%EC%A0%9C%EA%B3%B1%EC%88%98_%EC%A0%95%EB%A6%AC)
[Sum of two squares theorem - Wikipedia](https://en.wikipedia.org/wiki/Sum_of_two_squares_theorem)
$v_p(x)$ : p로 x를 몇 번 나눌 수 있는지
$v_p(a) + v_p(v) = v_p(ab)$ (소인수분해, 당연)
$v_p(n!) = \lfloor \frac{n}{ p}\rfloor+\lfloor \frac{n}{ p^{2}}\rfloor+\lfloor \frac{n}{ p^{3}}\rfloor$

인수들의 min을 통하어 빼낼 수 있음

p : odd prime
$p \nmid a,b \quad p\mid a-b$
$v_p(a^n-b^n)=v_{p}(a-b)+v_p(n)$
그냥 빼내면 됨

승수를 인수분해하여 쪼개나가야함
$a - b \rightarrow a^4 - a^4 \rightarrow a^{12}-b^{12}$

$p \nmid a,b \quad p\mid a-b$
$a=b+kp$
$(b+kp)^{p} - b^{p} = pb^{p-1}kp + {p\choose 2} b^{p-2}(kp)^{2}+...+$
$v_p(a^p-b^p) = 2 + v_p(k) = 1+v_p(pk) = 1+v_p(a-b) = v_p(a-b)+v_p(p)$
LTE(Lifting The Exponents)
[Lifting-the-exponent lemma - Wikipedia](https://en.wikipedia.org/wiki/Lifting-the-exponent_lemma)

$p\nmid a-b$ 일 경우 적절히 떨어트림

$v_{p}(a+d)^{k} - a^{k} = v_p(d)+v_p(k) >= 1$

[18496번: Euclid’s Algorithm](https://www.acmicpc.net/problem/18496)
$M = p_{1}^{a_{1}}p_{2}^{a_{2}}...p_{k}^{a_{k}}$

```python
import math
d,k=map(int,input().split())
ans=1
# p=2
# x-y = d, 2|d 이면서 k가 짝수라면 = v2(d) + v2(2a + d) + v2(k)- 1, 원래식보다 1큼, 2로 시작
# 4|d 일때는 v2(x+y) = 1, 넘어가도 됨
if d%4==2 and k%2==0 and k>2:
	ans=2

# Lifting-the-exponent_lemma의 조건이
# p | d 이면 되므로, gcd(p,d)가 1이 아닐때까지 반복가능
# ans*d에서 d안에 g들이 있으므로 한번씩만 곱하면됨
while True:
	g=math.gcd(d,k)
	if g == 1:
		break
	ans*=g
	k//=g
print(ans*d)
```

