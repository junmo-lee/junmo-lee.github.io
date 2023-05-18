---
title: "union_find"
date: 2023-05-16 00:00
description: "None"
categories: [Blog, algorithm]
tags: [math]     #lowercase
author: me
#math: true
#pin: true
#img_path: /imgs/
#mermaid: true

---

유니온 파인드


고무패킹 사이에서 상하좌우로 갈 수 있음
모든 쌍에 대해 가기 위해 필요한 최소 고무패킹수는?

각 패킹(점) 들 사이에서 x,y 좌표가 겹치면 같은 그룹으로 볼 수 있음
그룹과 그룹을 연결하기 위해 패킹하나가 필요하므로
답은 그룹 수 - 1

```c
#include <bits/stdc++.h>
using namespace std;

int arr[1001]; //각각에 x,y root
int x[101]; //i번째 고무패킹의 위치
int y[101];
int cnt[1001];

int find_root(int n){
    if(arr[n] == n) return n;
    else return arr[n] = find_root(arr[n]);
}

void union_tree(int x,int y){
    int px = find_root(x);
    int py = find_root(y);
    if(px != py) arr[px] = py;
}

int main(){
    ios::sync_with_stdio(false);
    cin.tie(0);

    int n;
    int res =0;
    cin >> n;
    for(int i=0;i<1001;i++) {
        arr[i] = i;
    }

    for(int i=0;i<n;i++) cin >> x[i] >> y[i];

    for(int i=0;i<n;i++){
        for(int j=i+1;j<n;j++){
            if(x[i] == x[j] || y[i] == y[j])
                union_tree(i,j);
        }
    }
    for(int i=0;i<n;i++){
        cnt[find_root(i)]++;
    }

    for(int i=0;i<n;i++){
        if(cnt[i]) res++;
    }
    cout << res - 1;
}

```

res 구현 부분이 map으로 했는데 틀림


 |𝑖−𝑗|=𝑑𝑖  만족할 때, 𝑖번째와 𝑗번째 사람이 현재 가진 종이를 교환가능, 조작되었는지 확인
```c
#include <bits/stdc++.h>
using namespace std;

int arr[101]; 
int d[101];
int fin[101];
int cnt[101];

int find_root(int n){
    if(arr[n] == n) return n;
    else return arr[n] = find_root(arr[n]);
}

void union_tree(int x,int y){
    int px = find_root(x);
    int py = find_root(y);
    if(px != py) arr[px] = py;
}

int main(){
    ios::sync_with_stdio(false);
    cin.tie(0);

    int n;
    int res =0;
    cin >> n;
    for(int i=1;i<=101;i++) {
        arr[i] = i;
    }

    for(int i=1;i<=n;i++) cin >> fin[i];
    for(int i=1;i<=n;i++) cin >> d[i];

    for(int i=1;i<=n;i++){
        if( i+d[i] <= n) union_tree(i,i+d[i]);
        if( i-d[i] >= 1) union_tree(i,i-d[i]);
    }

    for(int i=1;i<=n;i++){
        if(find_root(fin[i]) != find_root(arr[i])){
            cout << "NO";
            return 0;
        }
    }
    cout << "YES";
    
}
```