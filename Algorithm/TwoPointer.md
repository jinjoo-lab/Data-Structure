# 투 포인터

### 투 포인터

| 시간복잡도 | O(N) |
| --- | --- |
| 가정 | X |
| 방식 | 양 끝단에서 한칸씩 이동하면서 검색 범위를 좁힘 |
- 배열(리스트)를 **순차 접근** 시 사용 → **두 개의 위치**를 기록하면서 처리하는 알고리즘

> 1차원 배열이 있고, 이 배열에서 각자 다른 원소를 가리키고 있는 2개의 포인터를 조작해가면서 원하는 것을 얻는 형태이다. 이때문에 투포인터 알고리즘이라 부른다.
>

### 방식

- (양쪽에서 좁히기) start = 0 , end = n
- (하나가 나머지를 따라가기) start = 0 , end = 0

## 양쪽에서 좁히기

- start = 0 , end = n 이라고 설정하자 (n은 배열이나 리스트의 마지막을 의미한다)
- 조건에 따라 **start + 1** or **end - 1** 로 지속 탐색
- start ≤ end 라는 조건의 반복문을 만족하는 동안 위의 과정 반복

### 예제

[1253번: 좋다](https://www.acmicpc.net/problem/1253)

- 투 포인터를 사용해야 한다.
    - 위 문제에서는 우선 **배열을 정렬**해야 한다.
    - target에 대하여 조건을 만족하는 동안 left + 1 , right -1로 위치 조정하여 결과

```java
import java.io.*;
import java.util.*;

public class Main {

    static int n = 0;
    static int result = 0;

    public static void main(String[] args) throws IOException {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        n = Integer.parseInt(br.readLine());
        int[] board = new int[n];

        StringTokenizer st = new StringTokenizer(br.readLine());
        for (int i = 0; i < n; i++) {
            board[i] = Integer.parseInt(st.nextToken());
        }

        Arrays.sort(board);

        for(int i=0;i<n;i++){
            search(0,n-1,board[i],board);
        }

        System.out.println(result);
        br.close();
    }

    static void search(int left, int right, int target, int[] board) {
        while (left < right) {

            if (board[left] == target)
                left = left + 1;

            if (board[right] == target)
                right = right - 1;

            if(left >= right)
                return;

            int sum = board[left] + board[right];

            if (sum == target) {
                result = result + 1;
                return;
            }

            if(sum < target){
                left = left + 1;
            }

            if(sum > target){
                right = right - 1;
            }

        }

    }
}
```

## 하나가 나머지를 따라가기

- start = 0 , end = 0인 형태
- **start 가 break 조건을 가지고 있는 경우**가 많다. (주로 start ≥ end)인 경우 종료
- **start + 1 , end + 1**을 통해 탐색

### 예제

![Untitled](https://user-images.githubusercontent.com/84346055/271763170-9a3183f9-4ca9-432b-9230-71914ae10a99.png)

[1484번: 다이어트](https://www.acmicpc.net/problem/1484)

```java
import java.io.*;
import java.util.*;

public class Main {

    static int n = 0;
    public static void main(String[] args) throws IOException {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        n = Integer.parseInt(br.readLine());
        ArrayList<Integer> list = new ArrayList<>();
        int left = 1;
        int right = 2;

        while(true){
            if(left == right)
                break;

            int l = left * left;
            int r = right * right;
            int minus = r - l;
            if(minus >= n){
                if(minus == n) {
                    list.add(right);
                }

                left = left + 1;
            }

            else{
                right = right + 1;
            }
        }

        StringBuilder sb = new StringBuilder();
        for(int tmp : list){
            sb.append(tmp+"\n");
        }

        if(list.isEmpty())
            sb.append(-1+"\n");

        System.out.print(sb);

        br.close();
    }
}
```
