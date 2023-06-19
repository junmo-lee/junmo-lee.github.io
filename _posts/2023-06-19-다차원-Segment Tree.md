---
title: "다차원 Segment Tree"
date: 2023-06-19 18:12
description: "None"
categories: [Blog, algorithm]
tags: [tag]     #lowercase
author: me
math: true
#pin: true
#img_path: /imgs/
#mermaid: true

---
 다차원 Segment Tree, 다차원 Fenwick Tree,

- 이차원 Prefix Sum과 비슷하게 생각하면 됨
- 이차원에 대해서는 어떻게 할까?
- $s[i][j]$ : $a[0][0]$부터 $a[i][j]$까지의 합
- $a[x][y]$부터 $a[z][w]$까지의 합 : $s[x][y] - s[z - 1][y] - s[x][w - 1] + s[z - 1][w - 1]$
- 
- $s$배열을 채우는 원리도 위와 같다!
- 업데이트와 계산에 모두 $O(\lg n)$ 대신 $O((\lg n)^2)$이 소요
- 일차원에서와 마찬가지로 Fenwick의 구현이 Segment보다 쉬우나, 일차원에서 이차원이 되는 원리 자체는 비슷


[11658번: 구간 합 구하기 3](https://www.acmicpc.net/problem/11658)
```cpp
#include<bits/stdc++.h>
using namespace std;
typedef long long ll;

vector<vector<ll>> a(2100, vector<ll>(2100)), fenwick(2100, vector<ll>(2100));
ll n, m, i, j, p, q, r, s, t;

ll query(ll x, ll y)
{
	ll ret = 0, rem = y;
	while(x > 0) {
        y = rem;
        while(y > 0) {
            ret += fenwick[x][y];
            y -= (y & -y);
        }
        x -= (x & -x);
	}
	return ret;
}

void update(ll x, ll y, ll val)
{
    ll rem = y;
    while(x <= n) {
        y = rem;
        while(y <= n) {
            fenwick[x][y] += val;
            y += (y & -y);
        }
        x += (x & -x);
    }
}

int main()
{
    ios_base::sync_with_stdio(false);
    cin.tie(NULL);
    cout.tie(NULL);

	cin >> n >> m;
	for(i = 1; i <= n; i++) {
        for(j = 1; j <= n; j++) {
            cin >> a[i][j];
            update(i, j, a[i][j]);
        }
	}

	for(i = 0; i < m; i++) {
        cin >> p;
        if(p == 0) {
            cin >> q >> r >> s;
            update(q, r, s - a[q][r]);
            a[q][r] = s;
        }
        else {
            cin >> q >> r >> s >> t;
            cout << query(s, t) - query(q - 1, t) - query(s, r - 1) + query(q - 1, r - 1) << "\n";
        }
	}

	return 0;
}
```