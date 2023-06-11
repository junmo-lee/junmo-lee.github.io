---
title: "Harmonic-Lemma"
date: 2023-06-11 15:46
description: "None"
categories: [Blog, math]
tags: [math]     #lowercase
author: me
math: true
#pin: true
#img_path: /imgs/
#mermaid: true

---

[Harmonic-Lemma](https://ahgus89.github.io/algorithm/Harmonic-Lemma/)

모든 조화수열을 하나씩 구하면 n이지만
조화수열의 서로 다른 값이 $2\sqrt n$ 이하임을 이용하여 
각 값과 개수(구간)을 곱하는 아이디어

$\lfloor \frac{n}{i} \rfloor = \lfloor \frac{n}{j} \rfloor$ 인 최대 정수 $j = \lfloor \frac{n}{\lfloor \frac{n}{i} \rfloor} \rfloor$

[15897번: 잘못 구현한 에라토스테네스의 체](https://www.acmicpc.net/problem/15897)
i=1
1,2,3,4...n
i=2
1,3,5...
i=3
1,4,7....

즉 i=k일때 $\lfloor \frac{n}{i} \rfloor$ 만큼 연산하므로
구하려는 답은 $\sum\limits^{n}_{i=1}\lfloor \frac{n}{i} \rfloor$ 임을 알 수 있다

위의 Harmonic-Lemma를 이용해 $O(\sqrt n)$에 해결가능
```cpp
#include<bits/stdc++.h>
using namespace std;
typedef long long ll;
int main(){
    ll n,i,j;
    ll res = 0;
    cin >> n;
    n--; //문제에서 j가 1부터 시작, 1을 미리 빼고 1씩 더해놔야함
    for(i=1;i<=n;i=j+1){
        j = n/(n/i); //i부터 j까지 같은 수가 나옴
        res += (n/i + 1)*(j-i+1);
    }
    cout << res+1;
}
```

