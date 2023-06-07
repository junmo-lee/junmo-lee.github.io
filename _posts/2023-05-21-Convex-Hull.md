---
title: "Convex Hull"
date: 2023-05-21 14:24
description: "None"
categories: [Blog, algorithm]
tags: [math]     #lowercase
author: me
math: true
#pin: true
#img_path: /imgs/
#mermaid: true

---


Convex Hull : 모든 주어진 점을 포함하는 가장 작은 블록 다각형 [그레이엄 스캔](https://ko.wikipedia.org/wiki/%EA%B7%B8%EB%A0%88%EC%9D%B4%EC%97%84_%EC%8A%A4%EC%BA%94) → 조금 복잡함

### 알고리즘 
![](https://i.imgur.com/ONOvWmd.gif)


1.  두 점 A와 B 선택
    
    먼저, leftmost and rightmost points A, B를 찾는다.
    
    만약 그러한 점들이 여러 개 존재한다면, Y 좌표가 가장 작은 것을 A로 선택하고, Y 좌표가 가장 큰 것을 B로 선택한다.
    
    이러면 자명하게 A와 B는 convex hull을 이루게 된다. 왜냐하면 그들은 가장 멀리 떨어져 있으므로 주어진 점 중 한 쌍에 의해 형성된 어떤 선으로도 포함할 수 없기 때문이다.
    
2.  선분 AB를 기준으로 점들을 2개의 집합으로 구분한다.
    
    두 점 A와 B를 선택한 이후, 선분 AB를 긋는다.
    
    이 선분은 다른 모든 점들을 2개의 부분으로 나누게 될 것이다. 선분 AB 위에 있는 점들은 만약 convex hull을 구성할 시 S1에 속하게 되고, 아래에 있는 점들은 만약 convex hull을 구성할 시 S2에 속하게 된다.
    
    선분 AB 위에 존재하는 점들은 둘 중 어느 집합에 포함되어도 무관하다.
    
    점 A와 B는 두 집합에 모두 속한다.
    
3.  정렬
    
    모든 점들을 X 좌표를 기준으로 정렬한다. (A, B 포함)
    
    S1과 S2에 각각 A를 넣는다.
    
4.  S1
    
    그 후 모든 점들에 대해서 아래 사항을 확인한다.
    
    1.  현재의 점이 마지막 점인가? == B인가?
    2.  점 A와 현재의 점으로 이루어진 선분과, 현재의 점과 점 B로 이루어진 선분이 이루는 방향(orientation)이 시계 방향인가?
    
    만약 위와 같은 상황이라면,우리는 S1의 second last 점과 last 점이 이루는 선분과, last 점과 현재의 점이 이루는 각을 확인해야 한다.
    
    만약 그 각이 clockwise가 아니라면, 우리는 S1의 last 점을 지운다. 현재의 점이 S1의 last 점을 포함할 수 있기 때문이다. (그림을 그려보면 쉽게 이해할 수 있다.)
    
    우리가 S1의 last 점을 지울 수 없을 때까지 last 점을 지우는 과정을 반복한 후, 현재의 점을 S1에 추가한다.
    
    모든 점에 대해 위 과정을 마치면, S1에는 convex hull에 포함되는 점들만 남게 된다.
    
5.  S2
    
    S2에 대해서도 S1에서와 유사한 논리를 적용할 수 있다.
    
    모든 점들에 대해서 아래 사항을 확인한다.
    
    1.  현재의 점이 B인가?
    2.  점 A와 현재의 점이 이루는 선분과, 현재의 점과 점 B가 이루는 선분의 orientation이 시계반대 방향인가?
    
    만약 위와 같은 상황이라면, 우리는 S2의 second last 점과 last 점이 이루는 선분과, last 점과 현재의 점이 이루는 각을 확인해야 한다.
    
    만약 그 각이 counterclockwise가 아니라면, 우리는 S2의 last 점을 지운다. 현재의 점이 S2의 last 점을 포함 할 수 있기 때문이다. (마찬가지로, 그림을 그려보자.)
    
    우리가 S2의 last 점을 지울 수 없을 때까지 last 점을 지우는 과정을 반복한 후, 현재의 점을 S2에 추가한다.
    
6.  union
    
    S1과 S2를 합치면 convex hull이 완성된다.
    
    이 때, S1과 S2에 모두 점 A와 점 B가 포함되어 있으며, S1은 clockwise, S2는 counterclockwise 방향으로 점들이 나열되어 있음을 주의해야 한다.
    
    따라서 만약 점들을 점 A를 시작으로 clockwise로 나열하고 싶다면, S2의 양끝(점 A, B)를 제외한 나머지 점들을 뒤에서부터 S1의 뒤에 추가해주면 된다
    

분할정복을 이용해 조금 더 쉽게 구현할 수 있음

### 왼쪽과 오른쪽으로 나뉘 두개의 convex hull을 합치는 방법 
![](https://i.imgur.com/5v4CU4p.png)

-   상위 접선과 하위 접선을 찾는다.
-   찾는 방법
    -   a의 가장 오른쪽 친구를 찾는다.(양쪽다 자기보다 작을 때까지)
    -   b의 가장 왼쪽을 찾는다.
    -   두 점을 잇고 그 점이 왼쪽과 겹치면 왼쪽을 위로, 오른쪽과 겹치면 오른쪽 위로 한다

![](https://i.imgur.com/Khbeg1J.png)

### 분할정복 방법

-   점을 x기준 정렬한다(스위핑)
-   반반 나눠가면서 분할정복(머지소트처럼)

### 시간복잡도 

-   맨 처음 정렬 : $O(n)$
-   각 단계별로 $t$개의 점을 합칠때
    -   먼저 a의 가장 왼쪽과 b의 가장 오른쪽 : $O(t)$
    -   상위와 하위접선 찾는 것 : $O(t)$
    -   합치기 : $O(t)$
-   각 depth별 총 $O(n)$
-   depth $O(\lg n)$
-   즉, $O(n\lg n)$

반평면?
[Half Plane Intersection](https://junh0.tistory.com/7)

[로그인](https://www.acmicpc.net/group/workbook/view/15702/57522)

