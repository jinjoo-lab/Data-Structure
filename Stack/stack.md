# 스택

### 스택

- 선형 자료 구조
- FILO (First In Last Out) 자료구조
    - 가장 마지막에 넣은 값부터 차례대로 꺼낼 수 있다.
- 가장 대표적으로 프링글스 통을 생각하면 쉽다.

![Alt text](https://user-images.githubusercontent.com/84346055/248739113-45a54425-1d76-48e7-906d-4f3439789bdd.png)

**스택의 3가지 연산**

- push()
    - stack 의 top 위치에 데이터를 삽입한다.
    - O(1)
- pop()
    - statck의 top 위치의 데이터를 (삭제)꺼낸다.
    - O(1)
- top()
    - stack의 top 위치의 데이터를 확인한다.
    - O(1)
- 스택의 연산은 기본적으로 Top 위치에서 진행되기 때문에 시간 복잡도가 O(1)인 것을 알 수 있다.

**배열을 이용한 스택 구현**

```java
class MyStack
{
    int pos; // top의 위치를 갱신하기 위한 index 개념
    int[] stack;

    MyStack()
    {
        this.pos = 1;
        stack = new int[100000]; // 스택 선언
    }

    void push(int val)
    {
        stack[pos] = val;
        pos = pos + 1; // 스택에 데이터 추가 후 위치 조정
    }

    int pop()
    {
        return stack[--pos]; // 스택의 top 데이터를 반환 (삭제)
    }

    int top()
    {
        return stack[pos]; 
    }
}
```

- 배열을 이용한 스택의 구현은 난이도가 낮다. 하지만 스택의 Empty 여부 등등 편의성을 위해서는 다양한 추가 작업이 필요하다.
- 스택의 사용에 대해서는 기본적으로 위 3가지 연산이 핵심이 되어야 한다.

**Java 스택**

- `Stack<> stack`
    - java.util 패키지에 존재 , 스택에서 사용할 데이터는 제네릭 타입 (자유도가 높다)

```java
package java.util;

public class Stack<E> extends Vector<E> {

    public Stack() {
    } // 스택 생성

    public E push(E item) {
        addElement(item); // 위치(top) 증가후 데이터 삽입
				return item;
    }

    public synchronized E pop() {
        E       obj;
        int     len = size(); // 마지막 데이터 (LIFO)

        obj = peek(); // top과 같은 기능이라 생각하면 편하다.
        removeElementAt(len - 1); // 데이터 제거 후 위치 조정

        return obj;
    }

    public synchronized E peek() {
        int     len = size();

        if (len == 0)
            throw new EmptyStackException();
        return elementAt(len - 1); // 스택의 마지막 데이터 반환
    }

    public boolean empty() {
        return size() == 0; // 스택이 비어있는지 확인 -> while문과 함께 사용
    }
    public synchronized int search(Object o) {
        int i = lastIndexOf(o);

        if (i >= 0) {
            return size() - i;
        }
        return -1; // O(N)의 데이터를 찾는 메소드
    }
}
```
