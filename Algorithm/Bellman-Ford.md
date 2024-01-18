# 벨만-포드 알고리즘

## 벨만 - 포드

- 시작 노드에서 다른 노드까지의 최단 거리를 구하는 알고리즘
- **음수  간선 순환(음수 간선이 포함된 사이클)**이 존재하는 경우 최단 거리를 구하는데 사용하는 알고리즘
- 시간 복잡도 : **O(VE)**
- **다익스트라 ?**

  다익스트라 알고리즘과 동일하게 (시작노드 → 다른 노드 들) 최단 거리를 구하는 알고리즘이다.

  하지만 다익스트라 알고리즘은 **‘음수 간선 순환’**에 대한 처리가 불가능하다.


### VS 다익스트라 알고리즘

- **다익스트라**
    - 매 순간 최단 거리가 짧은 간선을 선택해나가며 최적해를 구한다.
    - 이전 다익스트라 알고리즘에서 말했지만 그리디적 성격을 가지고 있는 알고리즘이다.
    - 하지만 음수 간선 순환이 존재한다면 최적해를 구할 수 없다.
- 음수 간선 순환이 존재할 경우 매번 탐색이 진행(사이클을 순환) 할 때마다 작은 값으로 갱신되기 때문에 문제를 풀 수 없다.

### 음수 간선 순환을 고려하는 방법 ?

- **같은 건 없다….**
    - 모든 노드를 기준하여 **모든 간선을 고려**해야 한다는 것이다.
    - 음수 간선이 존재할 경우 최적해를 구해나가는 수행이 불가능하기 때문에 모든 경우의 수를 고려해야 한다는 것이다.

### 동작 과정

1. 시작 노드를 설정 한다.
2. 최단 거리 테이블을 초기화
3. 모든 간선을 확인한다.
4. 간선을 거쳐 다른 노드로 가는 비용이 감소할 경우 갱신
- 3,4의 과정을 **(V-1)번 반복**한다.

### EX

![Untitled](https://user-images.githubusercontent.com/84346055/284212505-98a69927-3a1b-4b18-a1d3-221c92a879e3.png)

![Untitled](https://user-images.githubusercontent.com/84346055/284212566-b01287e9-6da8-4115-8514-1c7f0c33ae6f.png)

![Untitled](https://user-images.githubusercontent.com/84346055/284212578-5ac37137-f9c1-413f-871e-df2807af49b5.png)

![Untitled](https://user-images.githubusercontent.com/84346055/284212586-7499e9bb-19a0-47ca-89a4-11378faef26b.png)

![Untitled](https://user-images.githubusercontent.com/84346055/284212592-d7a254ad-7736-4939-a5d0-a77505ee928a.png)

- 이 과정을 V-1번 반복
- **음수 순환 사이클**

  V-1 번의 반복을 수행하고 나서 **한번 더 수행**한다. 이 때 값이 갱신된다면 음수 순환 사이클이 존재한다는 것이다.


### 문제

[1865번: 웜홀](https://www.acmicpc.net/problem/1865)