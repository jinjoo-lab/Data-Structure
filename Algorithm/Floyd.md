# 플로이드 - 워셜

### 정의

> **모든 정점**에서 다른 **모든 정점**으로의 최단 경로 탐색 알고리즘
>
- 다익스트라 → **출발지**에서 **다른 모든 목적지**까지의 최단 경로 알고리즘
- 플로이드 워셜 알고리즘은 **음의 간선**에 대한 처리가 가능하다. (하지만 음의 사이클이 있으면 안된다.)

![Untitled](https://user-images.githubusercontent.com/84346055/271289551-d34b2410-f1c6-4b78-8140-408b31e335d0.png)

### 과정

![Untitled](https://user-images.githubusercontent.com/84346055/271289561-069e96a0-ae06-46b5-a89c-18fe21bc0a81.png)

1. 초기 그래프 상태를 **인접행렬**로 설정
- **그래프의 간선이 존재하지 않은 경우**
    - INF 값(충분히 범위 외의 값)을 설정해야 한다.

  ![Untitled](https://user-images.githubusercontent.com/84346055/271289621-952c0333-2da7-4b52-b826-0ee394ec1583.png)

1. Round를 진행 (노드의 개수만큼)
    - **중간 노드를 기준으로 거쳐 가는 경우**의 최솟값 갱신
    1. 1번 노드를 중간 노드로

   ![Untitled](https://user-images.githubusercontent.com/84346055/271289626-95a8dc31-ceba-401b-a3a0-b846cf383c9d.png)

    1. 2번 노드를 중간 노드로

   ![Untitled](https://user-images.githubusercontent.com/84346055/271289628-e4effcac-5799-49d7-a99e-63c8dc168faf.png)


### 시간복잡도

- **O(V^3)**
- **3제곱의 알고리즘**

  효율이 좋지 않을수 있기 때문에 입력값의 제한을 잘 보고 !


### 코드

```
// 초기화
for(int i = 1; i<=n; i++){
    for(int j =1; j<=n; j++){
        if (i == j) dist[i][j] = 0;
        else if (adj[i][j]) dist[i][j] = adj[i][j];
        else dist[i][j] = INF;
    }
}

// 플로이드 워셜 알고리즘
for(int k = 1; k<= n; k++){
    for(int i = 1; i <= n; i++){
        for(int j = 1; j<=n; j++){
            dist[i][j] = min(dist[i][j], dist[i][k]+dist[k][j]);
        }
    }
}
```
