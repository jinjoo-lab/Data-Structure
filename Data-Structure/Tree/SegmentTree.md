# 세그먼트 트리

### 세그먼트 트리

- 여러 개의 데이터가 존재할 때 **구간합(최솟값,최댓값,곱)**을 구하는 자료구조
- **이진 트리의 형태**
    - 특정 구간의 합을 : O(logN) 안에 구할 수 있다 ! (구간이라는 의미에서 연속성을 가진다)
- **기존 방식과 비교 (구간합)**

  선형적인 방법으로 반복문을 통해 구간합을 구하는 경우 **O(N)**을 가진다.


### 생성

- Tree의 크기
    - 데이터의 개수 : N이라 하자
    - N보다 큰 가장 가까운 **N의 제곱수의 2배만큼의 크기** 필요
    - 하지만 보통 N * 4 만큼의 크기를 설정한다.

**Data**

![Alt text](https://user-images.githubusercontent.com/84346055/267258542-f262ed56-c662-4101-83f9-6feafa7aad31.png)

**Segment Tree**

![Alt text](https://user-images.githubusercontent.com/84346055/267258561-518fafbe-353c-49dd-b613-203dababda57.png)

- 루트 노드
    - 전체 데이터의 합 → 총 합 !
    - 왼쪽 자식 노드 → 맨 왼쪽부터 절반 까지의 합
    - 오른쪽 자식 노드 → 절반+1 부터 맨 오른쪽 데이터 까지의 합
- **코드적 구현 ?**
    - **재귀를 사용**하여 구현한다 ! 범위를 절반씩 줄여가며 구간합을 저장한다.
    - 세그먼트 트리에서는 루트 Index를 1로 하도록 습관화하자 !
- **세그먼트 트리 root 노드 인덱스 → 1**

  세그먼트 트리는 이진 트리의 형태이다. 이진 트리의 경우 왼쪽 자식은 idx * 2 , 오른쪽 자식은 idx * 2 + 1인데 이러한 규칙을 적용하기 위해서는 루트 인덱스를 1부터 시작해야 한다.


### 생성 코드

```java
import java.util.*;
import java.io.*;

public class Main {

    static int[] data;
    static int[] tree;

    public static void main(String[] args) throws IOException {
       
        data = new int[]{0,1,2,3,4,5,6,7,8,9,10};

        tree = new int[data.length * 4];

        makeST(0,data.length- 1,1); // 루트 노드부터 만든다 생각

    }

    static int makeST(int left,int right,int index)
    {
        if(left == right) {
            tree[index] = data[left];
            return tree[index];
        }

        int mid = (left + right) / 2;

        tree[index] = makeST(left,mid,index*2) + makeST(mid+1,right,index*2 + 1);

        return tree[index];
    }
}
```

### **구간 합 구하기**

- 세그먼트 트리를 생성한 후 특정 구간의 합을 구하고 싶을 때
    - 범위로 판단
        - 범위가 데이터의 구간을 벗어난 경우 → 0
        - 범위가 데이터 구간 안에 포함된 경우 → tree[index]
    - 총 구간의 합은
        - left 구간합 + right 구간합

```java
import java.util.*;
import java.io.*;

public class Main {

    static int[] data;
    static int[] tree;

    public static void main(String[] args) throws IOException {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));

        data = new int[]{0,1,2,3,4,5,6,7,8,9,10};

        tree = new int[data.length * 4];

        makeST(0,data.length- 1,1);

        // 0부터 2까지 (0,1,2) = 3
        System.out.println(getV(0,data.length-1,1,0,2));

        br.close();
    }

    // start, end -> 시작 인덱스 , 마지막 인덱스
    // left , right -> 구간 합을 구하고자 하는 범위
    // index -> root 인덱스 부터 시작
    static int getV(int start , int end,int index , int left,int right)
    {
        if(left > end || right < start)
            return 0;  // 구간을 벗어난 경우

        if(left <= start && right >= end)
            return tree[index]; // 구간 내의 경우

        int mid = (start + end) / 2;

        return getV(start , mid , index * 2,left , right) + getV(mid + 1,end,index*2 + 1,left,right);
    }
}
```

[2042번: 구간 합 구하기](https://www.acmicpc.net/problem/2042)

### 특정 원소 값이 수정되는 경우

- 구간 합도 변경되기 때문에 세그먼트 트리 또한 변경되어야 한다.
    - tI → 값이 변경되는 index
    - tV → **변경되는 값 - 원래 값**

```
static void update(int left,int right, int index,int tI , long tV )
{
        if(tI < left || tI > right)
            return;

        tree[index] += tV;

        if(left == right)
            return;

        int mid = (left + right) / 2;

        update(left,mid,index*2,tI,tV);
        update(mid+1,right,index*2 +1,tI,tV);
}
```

### 최솟값 구하기

[10868번: 최솟값](https://www.acmicpc.net/problem/10868)

- **문제를 푸는 방식 ?**



```
// start , end -> data 범위
// left , right -> 최솟값을 찾고자 하는 범위
// index -> root부터 시작
static int find(int start,int end,int left,int right,int index)
{
        if(start > right || end < left)
            return Integer.MAX_VALUE;

        if(start >= left && end <= right)
            return tree[index];

        int mid = (start + end) / 2;

        int tl = find(start,mid,left,right,index*2);
        int tr = find(mid+1,end,left,right,index*2+1);

        return Math.min(tl,tr);

}
```
