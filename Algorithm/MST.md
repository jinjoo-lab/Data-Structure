# MST

## 그래프

- G = (V,E)
- 정점과 간선들의 집합을 그래프라 한다.
    - 정점에 대한 조건 : *nonempty set of V*
    - 간선에 대한 조건 : *possible empty set of E*

### 그래프의 종류

- 방향 그래프 : *(v0 , v1) ≠ (v1 , v0)*
- 무방향 그래프 : *(v0, v1) = (v1, v0)*

### Complete Graph( 완전 그래프 )

- 그래프의 모든 정점이 서로 연결되어 있는 그래프
- 간선의 개수
    - 무방향 그래프 : n(n-1) / 2
    - 방향 그래프 : n(n-1)

![Alt text](https://user-images.githubusercontent.com/84346055/265740260-76e8795e-0604-4e31-ad4c-fc09f42c1078.png)

**부분 그래프**

- 그래프는 **집합의 개념**이기 때문에 부분 그래프가 존재할 수 있다.

**단순 경로**

- 경로 중에 반복되는 정점이 없는 경우 (첫번째 출발지와 마지막 도착지를 제외)

**사이클 ( Cycle )**

- 단순 경로 중 출발지와 도착지가 같은 것
- 위 그림의 경우 (0 - 1 - 2) 가 사이클이라 할 수 있다.
- 사이클의 반대말은 Acyclic
- **사이클에 대한 판단**

  **방향 그래프**에서 사이클에 대한 판단은 기본적으로 **DFS**를 통해 알 수 있다.

  [https://www.acmicpc.net/problem/16724](https://www.acmicpc.net/problem/16724)


**연결 그래프 VS 비연결 그래프**

- 무방향 그래프에 있어 **모든 정점 사이에 경로가 존재하는 경우** 연결 그래프라 할 수 있다.

**연결 요소( Connected Component )**

- 연결 요소에 속한 모든 정점을 연결하는 경로가 있어야 한다. ( 연결 그래프 )
- 서로 다른 연결 요소 사이에는 이동 경로가 존재하지 않아야 한다.
- **연결 요소 개수 판단**

  DFS , BFS 즉 그래프 탐색의 횟수


- **트리의 정의**

  트리란 연결 그래프이며 비사이클(Acyclic)인 것 !


### 그래프 사용 방법( 코드 )

- 인접 행렬(배열)
- 인접 리스트(연결 리스트)

### 그래프 탐색 알고리즘

- BFS (너비 우선 탐색)
- DFS (깊이 우선 탐색)

## 최소 신장 트리 ( MST )

**신장 트리**

- 연결 그래프에서 그래프 탐색을 통해 생기는 트리 엣지로 이루어진 사이클을 갖지 않는 최소 부분 그래프
- **최소 부분이란 ?**

  **모든 정점**을 포함 , 간선의 개수 : 정점의 개수 - 1


**최소 신장 트리**

- 각 간선에 **가중치**가 적용되어 있다고 생각해보자
- 최소 신장 트리란 **트리 엣지들의 가중치의 합이 최소가 되는 신장 트리**인 것이다.

![Alt text](https://user-images.githubusercontent.com/84346055/265740281-d48fb183-eb94-4c21-a735-0aacb528422a.png)

**MST 판단 방법**

- 크루스컬 알고리즘
- 프림 알고리즘

## 프림 알고리즘

- T 와 NT 구분하여 정점을 한 개씩 추가해가면서 T를 채워나간다.
    - T와 NT 사이의 간선 중 가중치가 최소인 간선을 선택해나간다.

![Alt text](https://user-images.githubusercontent.com/84346055/265740310-7917bc99-c264-490b-85e9-6e97d831bf42.png)

- 배열을 사용하는 방법 : O(V^2)
- min heap을 사용하는 방법 (우선순위 큐) : O(ElogV)

**코드**

- 우선순위에서 사용하는 클래스
    - Edge : (w , cost)
        - 간선에서 연결되는 정점 , 가중치
        - 가중치를 기준으로 **오름차순 정렬**
- 프림 알고리즘

```
PriorityQueue<Edge> pq = new PriorityQueue<>();
pq.offer(new Edge(start, 0)); // 시작 지점
		
int total = 0; // 총 가중치 합
while(!pq.isEmpty()) {
	Edge edge = pq.poll(); 
	int v = edge.w;
	int cost = edge.cost;
		
	if(visit[v]) continue; // 방문 건너 뛰기 즉 ( T 는 건너뛴다. )
        
	visit[v] = true;
	total += cost;
		
	for(Edge e : graph[v]) {
		if(!visit[e.w]) {
			pq.add(e);
		}
	}
}
```

- **시작 지점의 기준**

  어느 정점을 선택해도 상관없다. 그 이유는 ?


## 크루스컬 알고리즘

### Disjoint Set (서로소 집합)

- 중복되지 않는 부분 집합들 (집합들 간의 공통 원소들이 없다)

### Union-Find

- 서로소 집합을 표현할 때 사용하는 알고리즘

**3가지 연산**

- make-set(x)
    - **초기화** , x를 유일한 원소로 하는 새로운 집합
    - Array[i] = i
- union(x,y)
    - 합하기
    - x ,y 가 속한 **집합을 합치는 작업** , 일반적으로 x = parent , y = child
    - O(N)
- find(x)
    - 찾기 , x가 속한 집합의 **최상위 노드를 반환**
    - O(N-1) , 트리의 높이와 시간 복잡도가 동일하다 , 경로 압축할 경우에는 **상수 시간**

**find(x)**

```
int find(int x){
	if(root[x] == x)
		return x; // 자기 자신이 최상위 부모 노드일 경우

	else{
		return find(root[x]); // 해당 집합의 최상위 노드 찾기 (재귀)
		return root[x] = find(root[x]) // 경로 압축
	}
}
```

**union(x,y)**

```
void union(int x,int y){
	x = find(x);
	y = find(y);

	if(x > y)
		root[x] = y;
	else
		root[y] = x;
}
```

### 크루스컬 알고리즘

- 간선들을 가중치를 기준으로 오름차순 정렬
- 사이클을 형성하지 않으면서 정렬된 순서의 간선들을 선택

![Alt text](https://user-images.githubusercontent.com/84346055/265740359-da905eb0-8e68-4f55-92cc-66ed1e448d80.png)

- **결과**

  ![Alt text](https://user-images.githubusercontent.com/84346055/265740379-f954628f-046f-4747-95be-3809e7f31bae.png)


**사이클 판단**

- 무방향 그래프에서의 사이클 판단은 **Union-Find** 사용
- **어떻게 ?**

    ![Alt text](https://user-images.githubusercontent.com/84346055/265740398-d2d1f8b1-a496-48b2-acb4-4086fae5763d.png)

  선택한 간선에 대해 두 정점의 최상위 노드가 동일할 경우 해당 간선에 대해 사이클이 발생하는 것을 알 수 있다.


**Kruskal Algorithm**

- 시간복잡도 : O(ElogE)

```
if(find(graph[i][0]) != find(graph[i][1]) // 사이클이 발생하지 않는다면
{
		union(graph[i][0] , graph[i][1]); // 병합
}
```

### 크루스컬 VS 프림

**시간복잡도**

- 프림 알고리즘
    - 우선순위 큐 사용한 경우 힙의 재구성에서 시간 복잡도가 결정된다 : O(ElogV)
- 크루스컬 알고리즘
    - 경로압축을 한 경우 시간 복잡도는 정렬에 의존적 : O(ElogE)

**난이도(내 생각)**

- 크루스컬 알고리즘의 경우 Union-Find 만들어야 함, 살짝 귀찮

**이모저모**

- 해당 문제가 MST 문제인지 어떻게 판단하나요 ?

  우선 그래프 문제인지 판단한다. **(정점과 간선)**을 나타내는 요소가 있는지 판단하고 다음 **가중치**를 나타내는 개념이 있는지 확인하라. 그리고 찾아야 하는 결과가 **최소 ~~~** 를 내포한다면 **No Doubt**

- MST는 중요한 개념인가요 ?

  네.


### 예제 문제

[1197번: 최소 스패닝 트리](https://www.acmicpc.net/problem/1197)

[1647번: 도시 분할 계획](https://www.acmicpc.net/problem/1647)

[10423번: 전기가 부족해](https://www.acmicpc.net/problem/10423)
