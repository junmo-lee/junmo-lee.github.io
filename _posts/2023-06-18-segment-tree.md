---
title: "segment tree"
date: 2023-06-18 10:27
description: "None"
categories: [Blog, algorithm]
tags: [tag]     #lowercase
author: me
#math: true
#pin: true
#img_path: /imgs/
#mermaid: true

---
##  Segment Tree

- Fenwick Tree는 구간 합에 대한 문제만 해결 가능
- Segment Tree는 최솟값, 최댓값 등 다양한 대푯값에 응용 가능
 
 ![](https://i.imgur.com/n14BT9x.png)

- 이진 트리의 구조를 이룸 → 보통 구현할 때, 일차원 배열로 구현함 : $segment[x]$의 양쪽 자식을 각각 $segment[x * 2], segment[x * 2 + 1]$로 표현
- 완전 이진 트리의 구조를 이루기 때문에 높이가 $\lg n$에 bound 됨
- 구간 대푯값 계산
    - 루트 노드부터 시작
    - 현재 노드의 범위에 완벽하게 포함된다면 값 리턴, 아니라면 자식들에게 전파
        - 만약 두 자식들에게 모두 전파되었다면, 마지막에 도달할 때까지 최대 두 개의 노드만 보게 됨(두 노드가 연속해야 하므로)
        - 한 자식에게만 전파되었다면, 위의 논리가 재귀적으로 성립
        - 따라서, 총 시간복잡도는 트리의 높이인 $O(\lg n)$이 됨
- 배열 값 업데이트
    - 리프 노드부터 시작
    - 자신의 값을 바꾸고, 바뀐 값을 부모에게 전파
    - 총 시간복잡도는 트리의 높이인 $O(\lg n)$

[27379번: 산유국](https://www.acmicpc.net/problem/27379)

- 구간 합, 투 포인터를 이용하여 전처리를 한 후 최댓값 세그먼트 트리 이용 (세그먼트 트리 구현 코드 참고)
```cpp
#include<bits/stdc++.h>
using namespace std;
typedef long long ll;

vector<ll> a, b;
ll n, m, i, edone = 1, cnt, assist, res = -1e18;
vector<ll> max_tree(4000000);

void init(ll node, ll st, ll ed)
{
	if (st == ed) {
		max_tree[node] = a[st - 1];
		return;
	}
	else {
		init(node * 2, st, (st + ed) / 2);
		init(node * 2 + 1, (st + ed) / 2 + 1, ed);
		max_tree[node] = max(max_tree[node * 2], max_tree[node * 2 + 1]);
		return;
	}
}

ll query(ll node, ll st, ll ed, ll left, ll right)
{
	if (left > ed || right < st)return -1e18;
	else if (left <= st && ed <= right)return max_tree[node];
	else {
		ll l, r;
		l = query(node * 2, st, (st + ed) / 2, left, right);
		r = query(node * 2 + 1, (st + ed) / 2 + 1, ed, left, right);
		return max(l, r);
	}
}

int main()
{
    ios_base::sync_with_stdio(false);
    cin.tie(NULL);
    cout.tie(NULL);

    cin >> n >> m;
    a.resize(n * 2);
    b.resize(n * 2);
    for(i = 0; i < n; i++) {
        cin >> a[i];
        a[n + i] = a[i];
    }
    for(i = 0; i < n; i++) {
        cin >> b[i];
        b[n + i] = b[i];
    }
    n *= 2;
    for(i = 1; i < n; i++)a[i] += a[i - 1];

    init(1, 1, n);

    cnt = b[0];
    for(i = 0; i < n / 2; i++) {
        if(edone == i) {
            edone++;
            cnt = b[i];
        }
        while(cnt < m) {
            cnt += b[edone];
            edone++;
        }
        assist = query(1, 1, n, edone, i + n / 2);
        if(i != 0)assist -= a[i - 1];
        res = max(res, assist);
        cnt -= b[i];
    }
    cout << res;

    return 0;
}
```


[1777번: 순열복원](https://www.acmicpc.net/problem/1777)
예제 입력에서 주어지는 inversion의 개수를 풀어서 설명하자면, 나보다 작은 숫자가 뒤에 몇 개나 있느냐를 의미합니다. 

순열의 총 크기를 안다면, 나보다 작은 숫자가 앞에 몇 개가 있는지 또한 구할 수 있습니다. 이는 k�번째가 어디에 위치한 지를 묻는 쿼리와 동등합니다.


