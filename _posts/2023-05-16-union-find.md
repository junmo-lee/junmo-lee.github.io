---
title: "union find"
date: 2023-05-16 16:04
description: "None"
categories: [Blog, algorithm]
tags: [matkor]     #lowercase
author: me
#math: true
#pin: true
#img_path: /imgs/
#mermaid: true

---

유니온 파인드

A. 재우가 스케이트는 Pass를 받을 수 있을까?
time limit per test 2 s.
memory limit per test 256 MB
input standard input
output standard output

"오늘의 삼단논법 : 재우는 스케이트를 수영보다 못한다. 그런데 재우는 수영이 F이다. 따라서 재우는 스케이트 초보자이다."

스케이트 초보자인 재우는 상하좌우로만 움직일 수 있으며, 얼음 위에서 방향을 바꿀 줄 모른다. 그래서 재우는 스케이트를 탈 때, 중간 중간 놓여있는 고무 패킹에서만 방향을 상하좌우로만 바꿀 수 있다. 또한, 한 고무 패킹에서 방향을 정해 출발하면 다음 고무 패킹을 만날 때 까지 그 방향으로 나아간다.

스케이트 장은 무한히 크며, 현재의 고무 패킹의 위치들이 있다. 재우는 임의의 고무 패킹에서 임의의 다른 고무 패킹으로 모든 쌍에 대해 갈 수 있고 싶지만, 현재 고무 패킹으로는 그러지 못한다.

스케이트장 큰 손인 재우를 위해 스케이트장에서는 고무 패킹을 추가로 놓으려고 한다. 임의의 고무 패킹에서 임의의 다른 고무 패킹으로 모든 쌍에 대해 갈 수 있도록 하기 위해 놓아야 하는 최소 고무 패킹의 개수를 구해보자.

Input

첫 줄에 고무 패킹의 수를 나타내는 정수 𝑛� (1≤𝑛≤1001≤�≤100)이 주어진다.

이어지는 𝑛� 개의 줄에는 𝑖�번 째 고무 패킹의 좌표를 나타내는 두 정수 𝑥𝑖��와 𝑦𝑖�� (1≤𝑥𝑖,𝑦𝑖≤10001≤��,��≤1000)가 주어진다.

모든 고무 패킹의 좌표는 다르다.

Output

첫 줄에 재우가 임의의 고무 패킹에서 임의의 다른 고무 패킹으로 모두 갈 수 있도록 추가로 배치해야 하는 최소의 고무 패킹의 개수를 출력한다.

Examples

input
2  
2 1  
1 2  
output
1  

input
2  
2 1  
4 1  
output
0

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

## B. 마니또와 재우의 의심
time limit per test 2 s.
memory limit per test 256 MB
input standard input
outputstandard output

MatKor 부원 𝑛�명은 마니또를 하기로 했다. 𝑛�명의 부원이 11번 부터 𝑛�번까지 번호를 정한 뒤 각자 자신의 번호에 해당하는 수가 적힌 종이를 가지고 있다. 또한, 각자 𝑖�번째 사람이 본인이 가장 좋아하는 수 하나 𝑑𝑖��를 정했다.

이제 마니또를 정하기 위해 각자 종이를 교환하기로 했다. 종이 교환은 |𝑖−𝑗|=𝑑𝑖|�−�|=��를 만족할 때, 𝑖�번째와 𝑗�번째 사람이 현재 가진 종이를 교환할 수 있다. 𝑖�와 𝑗� 두 명 중 한 명만 만족해도 된다. 교환 횟수는 무제한이며, 순서도 정해져있지 않다. 최종 교환 후 각자 본인이 가진 종이의 번호의 부원의 마니또를 하면 되며, 운이 안 좋아 본인이 본인의 마니또를 할 수도 있다.

재우는 마니또가 조작되었는지 알기 위해 최종 마니또의 상태와 𝑑𝑖��를 받아 여러번 교환해 가능한 상태인지 알고 싶다.

Input

첫줄에 부원의 수를 나타내는 양의 정수 𝑛� (1≤𝑛≤1001≤�≤100)이 주어진다.

두번째 줄에는 11부터 𝑛�까지 총 𝑛�개의 서로 다른 자연수가 주어진다. 이는 각자 자신이 맡은 마니또의 번호를 의미한다.

마지막 줄에는 𝑛�개의 11 이상 𝑛�이하의 정수 𝑑𝑖��가 주어진다.

Output

만약 교환을 통해 가능한 상태이면 YES, 아니면 NO를 출력하시오.

Examples

input
5  
5 4 3 2 1  
1 1 1 1 1  
output
YES  

input
7  
4 3 5 1 2 7 6  
4 6 6 1 6 6 1  
output
NO  

input
7  
4 2 5 1 3 7 6  
4 6 6 1 6 6 1  
output
YES

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