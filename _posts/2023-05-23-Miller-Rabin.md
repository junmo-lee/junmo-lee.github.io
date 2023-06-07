---
title: "Miller Rabin"
date: 2023-05-23 23:14
description: "None"
categories: [Blog, algorithm]
tags: [mathkor]     #lowercase
author: me
math: true
#pin: true
#img_path: /imgs/
#mermaid: true

---

[소수 판별법 - 에라토스테네스의 체, 밀러-라빈(Miller-Rabin) 소수판별법](https://rebro.kr/46)
→ 이사이트가 가장 설명이 잘나와있음


1. 페르마의 소정리 $a^{p-1}\equiv 1(mod p)$
2. 소수 p에 대해서 $x^{2}\equiv 1 (mod p)$ 이면 $x\equiv 1 \,or \, x\equiv -1 (mod p)$이다. pf : ($x^{2} - 1 | p,\,x^{2}-1=(x-1)(x+1)$)
짝수인 소수는 2밖에 존재하지 않으므로 홀수인 소수 N에 대해서 $N - 1 = d\times 2^r$
2를 사용하여 계속해서 나누어갈수 있음
따라서 N이 소수라면
1. $a^{d}\equiv 1 (mod N)$
2. $a^{d\times2^{r}}\equiv1(modN) for \,some\, r\,(0\leq r<s)$
중 하나를 만족해야 함
int 범위 : a = 2, 7, 61
long long 범위 : a = 2, 3, 5, 7, 11, 13, 17, 19, 23, 29, 31 (2~31까지의 소수)

matkor에서는
-   $a$가 $37$ 이하의 소수일 때 모두 성립하면 소수
-   a=2, 325, 9375, 28178, 450775, 9780504, 1795265022에 대해 모두 성립하면 소수
 
 [5615번: 아파트 임대](https://www.acmicpc.net/problem/5615)
 N = 2xy + x + y
 4xy + 2x + 2y + 1 = (2x+1)(2y+1) = 2N + 1
 2N+1이 소수라면 가능한 x,y가 존재하지 않음

코드를 뜯어 이해해보자
```cpp
ll modmul(ll a, ll b, ll m) {
	a %= m;
	b %= m; 
	ll r = 0, v = a;
	while (b) {
		if (b & 1) r = (r + v) % m;
		b >>= 1; //b/=2
		v = (v << 1) % m;
	}
	return r;
}
```
a\*b (mod m)을 오버플로우를 방지해 구하는 함수
2. 나머지의 곱과 원래들의 곱의 나머지는 같음
6. `amod + bmod <= amod`로 오버플로우 탐지, $a+b\equiv a+b-n(modn)$ 를 통해 오버플로우가 나지 않도록

![](https://i.imgur.com/PfXXl9D.png)
[오버플로우 없는 나머지 연산 구현하기](https://helloworldpark.github.io/programming/2017/03/14/Modulo_No_Overflow.html)


[[Chapter 3. 컴퓨터 연산] 곱셈](https://eunajung01.tistory.com/112)
![](https://i.imgur.com/TAO0ySx.png)


```cpp
ll modpow(ll n, ll k, ll m) {
	ll ret = 1;
	n %= m;
	while (k) {
		if (k & 1) ret = modmul(ret, n, m);
		n = modmul(n, n, m);
		k /= 2;
	}
	return ret;
}
```
일반적인 거듭제곱을 log n에 계산하는거
곱셈에 modmul 사용

```cpp
bool test_witness(ull a, ull n, ull s) {
	if (a >= n) a %= n;
	if (a <= 1) return true;
	ull d = n >> s;
	ull x = modpow(a, d, n);
	if (x == 1 || x == n - 1) return true;
	while (s-- > 1) {
		x = modmul(x, x, n);
		if (x == 1) return false;
		if (x == n - 1) return true;
	}
	return false;
}
```
각 a에 대해 소수 여부를 판단하는 코드
$x \equiv a^{k} (mod n)\,\, \text{by modpow}$


```cpp
bool is_prime(ull n) {
	if (n == 2) return true;
	if (n < 2 || n % 2 == 0) return false;
	ull d = n >> 1, s = 1;
	for (; (d & 1) == 0; s++) d >>= 1;
#define T(a) test_witness(a##ull, n, s)
	if (n < 4759123141ull) return T(2) && T(7) && T(61);
	return T(2) && T(325) && T(9375) && T(28178)
		&& T(450775) && T(9780504) && T(1795265022);
#undef T
}
```

2. n이 2일때는 소수
3. 2보다 작거나 짝수이면 당연히 합성수
4. d=n/2, s=1 부터 시작해서
5. $n-1 = d\times2^s$ 가 되도록 s를 키워나감
7. int 범위에 들어올 경우 2,7, 61
8. long long 범위에 들어갈 경우, 모두 참이 나와야 소수임