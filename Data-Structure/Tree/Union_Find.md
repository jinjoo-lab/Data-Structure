# 분리 집합

### 분리 집합(Disjoint Set)

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

### **find(x)**

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

- **경로 압축**

  **O(logN)**

    - 최적화 과정을 거치면 트리의 높이는 합쳐진 두 트리의 높이가 같을 때만 증가하게 된다.
    - 최적화를 통해 트리의 높이가 포함한 노드의 수의 로그에 비례하는 것을 보장하게 되므로 union과 find의 연산의 시간복잡도가 O(logN)이 된다.

### **union(x,y)**

```
void union(int x,int y){
	x = find(x);
	y = find(y);

	if(x < y)
			root[y] = x;
	else
			root[x] = y;
}
```

### 예제

[4195번: 친구 네트워크](https://www.acmicpc.net/problem/4195)

[10775번: 공항](https://www.acmicpc.net/problem/10775)
