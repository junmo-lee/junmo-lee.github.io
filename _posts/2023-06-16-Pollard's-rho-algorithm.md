---
title: "Pollard's rho algorithm"
date: 2023-06-16 20:37
description: "None"
categories: [Blog, algorithm]
tags: [matkor]     #lowercase
author: me
math: true
#pin: true
#img_path: /imgs/
#mermaid: true
---

- $n$ 제한이 매우 크므로 더 빠른 알고리즘 필요
- 생일 문제 : $n$명의 사람이 모였을 때 생일이 같은 두 명이 존재할 확률은?
    - $23$명만 모여도 확률이 $50\%$를 넘고, $57$명이 모이면 확률이 $99\%$보다 큼
    - 비둘기 집의 원리에 의해 $367$명 이상의 사람이 모이면 $100\%$의 확률로 존재
- 어떤 수 $n$에 대해 $2$부터 $n-1$까지의 수 중 하나를 무작위로 뽑았을 때, 그 수가 $n$의 약수일 확률은 매우 낮음
    - $100$의 경우 $7 \over 98$, $1040257(=127 \times 8191)$의 경우 $2 \over 1040255$
- 이를 개선 → $n$과 서로소가 아닌 수를 찾는다면 최대공약수를 계산하여 $n$의 약수를 찾을 수 있음
- 폴라드 로 알고리즘은 소인수분해 알고리즘이 아니라 인수분해 알고리즘임 → 그러나, 이를 소수가 나올 때까지 반복해서 재귀적으로 적용하면 결국 소인수분해 가능
- 어떤 수 $n$에 대해 $1, n$이 아닌 $n$의 약수 $d$를 찾는 것이 목표 → $d, {n \over d}$에 대해 반복 적용

- 폴라드 로 알고리즘의 과정
    - $n$이 소수인 경우는 실행시간이 매우 느려지므로, 밀러-라빈 소수 판별법을 통해 소수 여부 판별 [2023-05-23-Miller-Rabin](_posts/2023-05-23-Miller-Rabin.md)
    - $n$이 약수 $d$를 가진다고 가정
    - 함수 $f$를 $f(x)=x^2+c$로 정의, 시작값 $s$ ($c,\ s$는 임의의 정수)
    - $s, f(s), f(f(s)), \cdots$를 반복하여 계산 (단, 수가 커질 수 있으므로 $\mod n$을 반복하여 취해줌 → $d$가 $n$의 약수이므로 $\mod n$을 취해도 이후 논의를 이어갈 수 있음)
    - 각 항의 값들에 대해 모두 $\mod d$를 취했다고 가정
    - 비둘기 집의 원리에 의해 $d$개 이하의 개수를 갖는 cycle 형성 (값이 $0$부터 $d-1$까지 가능하므로)
    - cycle을 형성하므로 어떤 두 수 $a,\ b$에 대해 $a \equiv b \mod d$ 만족
    - $\gcd(a-b,\ n)$을 통해 약수 $d$를 찾을 수 있음
    - 다만, 이 과정을 우리는 $d$를 모른 채로 진행해야 함
    - 어떤 두 수가 $\mod d$에 대해 같은 값을 가진다는 사실을 어떻게 판별할까?
 - Hint 1. 플로이드 순환 찾기 알고리즘
    - 투 포인터 방식으로 진행
    - 하나는 매번 한 칸씩 앞으로 가고, 하나는 매번 두 칸씩 앞으로 감 → 사이클이 존재한다면 언젠가는 만나게 됨
- Hint 2
    - 두 개의 포인터 $p, q$가 각각 첫 노드를 가리킴
    - $p$는 두 칸씩, $q$는 한 칸씩 진행
    - $\gcd(a-b, n) \neq 1$을 만족하면 약수 $d$를 찾는데 성공
    - 아니라면 계속 진행
    - 만약 약수 $d$가 찾아지지 않는다면 $c$와 $s$를 다른 수로 바꿔 다시 알고리즘 반복

- $x=2,\ f(x)=x^2+1,\ d=317$인 경우
![](https://i.imgur.com/DRcnCwN.png)
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

ll pollard_rho(ll n) {
	random_device rd;
	mt19937 gen(rd());
	uniform_int_distribution <ll> dis(1, n - 1);
	ll x = dis(gen);
	ll y = x;
	ll c = dis(gen);
	ll g = 1;
	while (g == 1) {
		x = (modmul(x, x, n) + c) % n;
		y = (modmul(y, y, n) + c) % n;
		y = (modmul(y, y, n) + c) % n;
		g = gcd(abs(x - y), n);
	}
	return g;
}

void factorize(ll n) {
	if (n == 1) {
		return;
	}
	if (n % 2 == 0) {
		result.push_back(2);
		factorize(n / 2);
	}
	else if (is_prime(n)) {
		result.push_back(n);
	}
	else {
		ll f = pollard_rho(n);
		factorize(f);
		factorize(n / f);
	}
}
```