# 힙 (우선순위 큐)

### 우선순위 큐

- 우선순위를 가지는 데이터를 저장하는 큐

![Untitled](%E1%84%92%E1%85%B5%E1%86%B8%20(%E1%84%8B%E1%85%AE%E1%84%89%E1%85%A5%E1%86%AB%E1%84%89%E1%85%AE%E1%86%AB%E1%84%8B%E1%85%B1%20%E1%84%8F%E1%85%B2)%208182893f677148bd89790be817ca0ee2/Untitled.png)

- 사용자가 지정한 우선순위에 따라 가장 우선시되는 데이터가 앞단에 위치

**구현방법**

- 배열
    - 삽입 : O(N) , 삭제 : O(1)
- 연결 리스트
    - 삽입 : O(N) , 삭제 : O(1)
- **힙(Heap)**
    - 삽입 : O(logN) , 삭제 : O(logN)

- 삽입과 삭제 연산에 대한 시간복잡도의 편차가 큰 배열, 연결리스트보다 힙을 이용하여 우선순위 큐 사용

## 힙

- 특정 조건을 만족하는 **완전이진트리**
    - 완전이진트리(Complete BT)
        - 높이가 h일 때 , 레벨 h-1까지는 Full BT이고 , 레벨 h에서 왼쪽부터 노드가 순서대로 채워짐
    - 모든 노드의 데이터는 자식 노드들보다 우선순위가 높다.

### max heap

- 부모 노드의 우선순위가 자식 노드의 우선순위보다 **크거나 같다**

### min heap

- 부모 노드의 우선순위가 자식 노드의 우선순위보다 작거나 같다

![Untitled](%E1%84%92%E1%85%B5%E1%86%B8%20(%E1%84%8B%E1%85%AE%E1%84%89%E1%85%A5%E1%86%AB%E1%84%89%E1%85%AE%E1%86%AB%E1%84%8B%E1%85%B1%20%E1%84%8F%E1%85%B2)%208182893f677148bd89790be817ca0ee2/Untitled%201.png)

### 힙 연산

**삽입**

- 힙에서의 삽입은 2단계를 거친다.
    - 우선 새로운 데이터가 들어오면 마지막 노드에 추가
        - 해당 과정에서 힙의 성질(부모 노드와 자식 노드간의 우선순위)가 깨질 수 있다.
    - **heapify**
        - 삽입된 노드부터 루트까지의 경로의 노드들간의 우선순위를 비교 (교환 발생)
        - O(logN)

![Untitled](%E1%84%92%E1%85%B5%E1%86%B8%20(%E1%84%8B%E1%85%AE%E1%84%89%E1%85%A5%E1%86%AB%E1%84%89%E1%85%AE%E1%86%AB%E1%84%8B%E1%85%B1%20%E1%84%8F%E1%85%B2)%208182893f677148bd89790be817ca0ee2/Untitled%202.png)

**삭제**

- 기본적으로 우선순위가 가장 높은 값이 삭제되기 때문에 **루트 노드가 삭제**될 것이다.
- 과정
    - 마지막 노드를 루트 노드로 이동
    - 루트에서 단말 노드까지 우선순위를 비교하여 교환 → **heapify**
        - 루트를 기준으로 자식의 개수는 최대 2개
            - 두 자식 중에 우선순위가 높은 것과 교환

### 힙 정렬

- 정렬 중에 구현을 한다면 가장 날먹 정렬이다. O(NlogN)
- 기본적으로 힙에서 삭제 연산은 우선순위가 가장 큰 것을 반환한다.
    - 데이터의 크기가 우선순위의 기준이라면?
        - 데이터의 개수만큼 삭제를 진행할 경우 → 오름차순 or 내림차순 정렬이 완성된다.

### 배열을 이용한 힙 구현

```java
public class Main {

    public static void main(String[] args) throws IOException {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));

        MyHeap mh = new MyHeap(100);

        mh.push(7);
        mh.push(3);
        mh.push(2);
        mh.push(8);
        mh.push(9);

        for (int i = 1; i <= mh.size; i++) {
            System.out.print(mh.heap[i] + " ");
        }
        System.out.println();

        mh.pop();

        for (int i = 1; i <= mh.size; i++) {
            System.out.print(mh.heap[i] + " ");
        }
        System.out.println();

        br.close();
    }
}

class MyHeap {
    int[] heap;
    int size;

    MyHeap(int size) {
        this.heap = new int[size];
        this.size = 0;
    }

    void push(int data) {
        this.size = this.size + 1;
        int idx = this.size;
        this.heap[idx] = data;

        // heapify
        while (idx != 1 && this.heap[idx] > this.heap[idx / 2]) {
            int tmp = this.heap[idx];
            this.heap[idx] = this.heap[idx / 2];
            this.heap[idx / 2] = tmp;

            idx = idx / 2;
        }
    }

    int pop() {
        int re_data = this.heap[1];

        this.heap[1] = this.heap[size];
        this.heap[this.size] = 0;
        this.size = this.size - 1;
        int idx = 1;

        while (idx * 2 <= this.size) {
            int large = 0;

            if (this.heap[left(idx)] >= this.heap[right(idx)])
                large = left(idx);

            else large = right(idx);

            if (this.heap[idx] > this.heap[large])
                break;

            int tmp = this.heap[idx];
            this.heap[idx] = this.heap[large];
            this.heap[large] = tmp;

            if (large % 2 == 0)
                idx = idx * 2;
            else
                idx = (idx * 2) + 1;
            
        }

        return re_data;
    }

    int left(int i) {
        return i * 2;
    }

    int right(int i) {
        return (i * 2) + 1;
    }
}
```

- 오른쪽 자식과 왼쪽 자식이 힙의 크기를 벗어난 경우는 처리하지 않았다.

**힙 정렬 (구현)**

```
while(mh.size != 0)
{
    System.out.println(mh.pop());
}
```

### Java에서의 우선순위 큐

- 자바에는 별도의 Heap 클래스라는 것이 존재하지 않는다.
- `java.util` 패키지에 `PriorityQueue`라는 클래스가 존재하는데 해당 클래스가 우선순위 큐이다.

### PriorityQueue

- 제네릭 타입으로 데이터를 설정할 수 있다.
- Comparator를 통해 별도의 우선순위를 설정할 수 있다.
    - 기본적으로 Heap 자료구조를 기반으로 되어있다.

```java
class PriorityQueue {
    transient Object[] queue;

    int size;

    @SuppressWarnings("serial") // Conditionally serializable
    private final Comparator<? super E> comparator;
}
```

**사용 방법**

```
PriorityQueue<Data> pq = new PriorityQueue<>(
	(x,y) -> x.p - y.p
);
```

[[자료구조] 코드로 알아보는 java의 PriorityQueue with Heap](https://sabarada.tistory.com/144)
