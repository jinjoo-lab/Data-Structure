# 큐

### Queue

- (FIFO) 선입 선출의 선형 자료구조
- **음식점 앞의 대기줄**을 생각하면 쉽다.

**대표적인 연산**

- Enqueue ↔ push : 큐의 tail에 데이터를 추가
- Dequeue ↔ pop : 큐의 head에 있는 데이터를 삭제 + 반환
- peek : 큐의 head 에 있는 데이터를 확인

**배열을 이용한 큐**

- 배열을 통해 직접 큐를 구현할 때 고려해야 할 점이 있다.
    - 선언적 배열은 기본적으로 크기가 **한정적**
    - push 연산 수행 → Tail의 인덱스가 1 증가
    - pop 연산 수행 → Head 의 인덱스가 1 증가
- 위 두 연산이 반복적으로 수행되는 경우 남는(쓰레기 공간) 발생

![Untitled](%E1%84%8F%E1%85%B2%20b6a0746696a94b3da9a2131a7b1fab31/Untitled.png)

**해결 방법**

- 원형 큐(Circular Queue) 사용
    - 기본적인 큐에서 Tail의 위치가 **마지막 인덱스에 도달한 경우 0으로 교체**

![Untitled](%E1%84%8F%E1%85%B2%20b6a0746696a94b3da9a2131a7b1fab31/Untitled%201.png)

**리스트를 이용한 큐**

- 기본적으로 위와 같은 걱정을 할 필요가 없다 !

### Java에서의 큐

**선언**

- `Queue<Integer> q = new LinkedList<>();`
    - 자바에서 Queue는 인터페이스 형태 , 구현체로 LinkedList를 사용

**메소드**

```java
public interface Queue<E> extends Collection<E> {
   
    boolean add(E e);

    boolean offer(E e);

    E remove();

    E poll();

    E element();

    E peek(); 
}
```

- add , offer
    - Tail 위치에 데이터를 추가하는 메소드
    - 데이터 추가 성공시 `true` 반환

  차이점

    - add는 데이터 추가 실패시 `illegalStateException`
    - offer는 데이터 추가 실패기 `false`

- remove , poll
    - Head 위치에서 데이터를 제거하는 메소드

  차이점

    - remove는 큐가 비어있을 때 `NoSuchElementException`
    - offer는 큐가 비어있을 때 `null` 반환

- element , peek
    - 큐의 Head에 있는 데이터 반환
    - 차이점은 remove , poll과 동일

### Queue 활용

- 가장 대표적인 활용에는 BFS가 있다.

```java
class BFS{
    void bfs(){
    Queue<Data> q = new LinkedList<>();
    q.add(new Data(i,j));
    visit[i][j] = true;

    while(!q.isEmpty())
    {
	    Data cur = q.poll();

	    for(int i=0;i<4;i++)
	    {
		    int nx = cur.x + dx[i];
		    int ny = cur.y + dy[i];

		    if(!visit[nx][ny])
		    {
			    visit[nx][ny] = true;
			    q.add(new Data(nx,ny));
		    } 
	    }
    }
    }
}
```
