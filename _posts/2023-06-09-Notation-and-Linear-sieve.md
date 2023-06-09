---
title: "Notation-and-Linear-sieve"
date: 2023-06-09 09:15
description: "None"
categories: [Blog, math]
tags: [tag]     #lowercase
author: me
math: true
#pin: true
#img_path: /imgs/
#mermaid: true

---
## Notation
[Notation](https://ahgus89.github.io/algorithm/Notation/)

$\sigma(n)$ : n의 모든 약수들의 합
$\tau(n)$ : 약수의 개수의 합


$\epsilon(n) = [n=1]$  n이 1일 때 1, 아닐 때 0을 나타내는 함수이다.
$\gamma(n) := 1(n), 0(otherwise)$
$e(n) \sum_{d\mid n} \gamma(d)$
$\gamma(n) = \sum_{d\mid n} \mu(d)$
$\phi(n) = n\displaystyle \prod_{i=1}^k (1-\frac{1}{p_i})$ n이하의 n과 서로소인 수의 개수

모두 곱셈적 함수

## Linear-sieve
[Linear-sieve](https://ahgus89.github.io/algorithm/Linear-sieve/)

[2960번: 에라토스테네스의 체](https://www.acmicpc.net/problem/2960)
```c
bool isp[sz];
void era(int n)
{
	memset(isp, 1, sizeof isp);
	for(int i=2;i<=n;i++)
		if(isp[i])
			for(int j=2;i*j<=n;j++)
				isp[i*j]=0;
}
```
연산횟수 $n \sum\limits^{n}_{i=1}\frac{1}{i}$
$\ln n=\int_1^n {1\over x}dx\lt\sum_{i=1}^n {1\over i} = 1+\sum_{i=2}^n {1\over i} \lt 1+\int_1^n {1\over x}dx = 1+\ln{n}$
O(n ln n)안에 해결됨
![](https://i.imgur.com/E1tQhk3.png)




## SPF(Smallest Prime Factor)
이와 같이 인수가 많은 합성수는 여러번 합성수라고 판별
지금까지 구한 소수들을 보면서, p가 특정 조건을 만족하지 않는 순간 반복을 멈추면 될 것이다. 이런 조건을 만족하는 좋은 소인수는 **최소소인수**
폴라드 로 알고리즘


즉, 2i,3i,5i,7i,…를 보다가, p가 ip의 최소소인수가 아닌 순간 판별을 멈추면 된다. i의 최소소인수는 p이상이어야 하므로, p∣i일 때 판별을 하고 나면, 그 다음부터는 고르는 소수가 i의 최소소인수보다 크게 되므로 ip의 최소소인수가 될 수는 없다. 따라서 판별을 종료해주면 된다

이렇게 되면, 모든 합성수에 대해서 딱 한번씩만(최소소인수는 유일하니까) 판별을 해주게 되고, O(n)의 시간복잡도를 얻을 수 있다. 과정을 요약하면 다음과 같다.

i가 합성수가 아니면 소수 목록에 i를 추가한다. 소수 목록에 있는 j에 대해, ij는 합성수이고, i가 j의 배수이면 멈춘다.
```c
vector<bool>isprime(n+1,true);
vector<int> primes;
vector<int> SPF(n+1,1);
isprime[0]=isprime[1]=false;
for(i=2;i<=n;i++){
	if(isprime[i]){
		primes.push_back(i);
		SPF[i]=i;
	}
	for(int p:primes){
		if(i*p>N && p<=SPF[i]){
			break;
		}
		else{
			isprime[i*p]=false;
			SPF[i*p]=p;
		}
	}
}
```

정수론적 계산에서 liner sieve 사용
곱셈함수 f(n)에 대해 f(i)를 채워 넣을때
f(nm) = f(n)f(m) 이므로 

```c
#include<bits/stdc++.h>
using namespace std;
typedef long long ll;
typedef pair<int, int> pii;
int n, m, k, ans, mod=1e9+7;
int pw(int a, int b)
{
	int ret=1;
	while(b)
	{
		if(b&1) ret*=a;
		a*=a;
		b>>=1;
	}
	return ret;
}

vector<int> p;
const int sz=101010;
int sp[sz], e[sz], phi[sz], mu[sz], tau[sz], sigma[sz];

int main()
{
	ios_base::sync_with_stdio(false);
	cin.tie(0);
	int i, j, temp=0;
	phi[1]=mu[1]=tau[1]=sigma[1]=1;
	for(i=2;i<sz;i++)
	{
		if(!sp[i])
		{
			p.push_back(i);
			e[i]=1;
			phi[i]=i-1;
			mu[i]=-1;
			tau[i]=2;
			sigma[i]=i+1;
		}
		for(auto j:p)
		{
			if(i*j>=sz) break;
			sp[i*j]=j;
			if(i%j==0)
			{
				e[i*j]=e[i]+1;
				phi[i*j]=phi[i]*j;
				mu[i*j]=0;
				tau[i*j]=tau[i]/e[i*j]*(e[i*j]+1);
				sigma[i*j]=sigma[i]*(j-1)/(pw(j, e[i*j])-1)*(pw(j, e[i*j]+1)-1)/(j-1);//overflow
				break;
			}
			e[i*j]=1;
			phi[i*j]=phi[i]*phi[j];
			mu[i*j]=mu[i]*mu[j];
			tau[i*j]=tau[i]*tau[j];
			sigma[i*j]=sigma[i]*sigma[j];
		}
	}
	for(i=2;i<sz;i++)
		cout<<i<<' '<<e[i]<<' '<<phi[i]<<' '<<mu[i]<<' '<<tau[i]<<' '<<sigma[i]<<'\n';
}
```


