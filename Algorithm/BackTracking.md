# 백트랙킹

### 백트랙킹 (Backtracking)

- 해를 찾는 과정에 있어 더 이상 해를 찾을 수 없는 경우 탐색을 종료하고 이전 단계로 되돌아가 해를 찾아나가는 기법
- **가지치기**라고 불린다.
    - 백트랙킹의 성능은 얼마나 **효율적으로 가지치기**를 하는가에 달려있다.

![Untitled](https://user-images.githubusercontent.com/84346055/270316617-a720c60f-a65d-4087-acff-0b1ffe0e80d7.png)

### DFS vs 백트랙킹

- DFS
    - DFS는 가능한 모든 경로를 탐색 → 경우의 수를 최적으로 줄이지 못한다.
    - N!의 경우의 수를 가지는 문제는 처리가 불가능하다.
- 백트랙킹
    - 해를 찾아가는 도중에 지금의 경로가 해가 될 거 같지 않으면, 더 이상 깊이 들어가지 않고 이전 단계로 돌아간다.(가지치기)
    - 불필요한 부분을 쳐내고 최대한(가능한) 올바른 방향으로 나아가는 방법. → DFS보다 효율적.
    - N!의 경우 Worst Case는 여전히 지수함수의 시간복잡도가 나오므로 처리가 불가능 할 수 있다.
    - 문제를 보고 가지치기를 얼마나 잘하느냐에 따라 효율성이 결정된다.

### 구현

- 백트랙킹은 **재귀**를 바탕으로 구현한다.
- 재귀 함수 내에 조건절을 삽입하여 **탐색을 중지할 지점**을 명시해야 한다.

### 시간 복잡도

- 백트랙킹의 시간복잡도는 **가지치기의 효율성**에 따라 다르고 **문제 유형**에 따라 다르다.
- 무조건 정답은 아니지만 **지수승의 시간 복잡도의 밑 인자를 줄이기 위해 많이 사용**된다.

### 수도 코드

```
procedure bt(c) is
    if reject(P, c) then return
    if accept(P, c) then output(P, c)
    s ← first(P, c)
    while s ≠ NULL do
        bt(s)
        s ← next(P, s)
```

- 수도코드 해석
    - reject(P,c): 만약 다음의 노드가 후보가 아닌다면 return으로 끝낸다.
    - accept(P,c): 만약 현재 노드까지가 답과 일치한다면 답을 출력한다.
    - first(P,c): 후보 C의 첫번째 확장을 시작한다.
    - 답이 없을때까지 다음 함수를 계속 반복한다

### 예시

[9207번: 페그 솔리테어](https://www.acmicpc.net/problem/9207)

전체 코드

```java
import java.io.*;
import java.util.*;

public class Main {
    static int n = 0;
    static char[][] board;
    static boolean[][] visit;

    static int[] dx = {0,0,-1,1};
    static int[] dy = {1,-1,0,0};

    static int result = 45;
    static int count = 0;
    public static void main(String[] args) throws IOException {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        StringTokenizer st = new StringTokenizer(br.readLine(), " ");
        n = Integer.parseInt(st.nextToken());

        StringBuilder sb = new StringBuilder();

        for(int k=1;k<=n;k++)
        {
            board = new char[6][10];
            visit = new boolean[6][10];

            for(int i=1;i<=5;i++)
            {
                String line = br.readLine();
                for(int j=1;j<=9;j++)
                {
                    board[i][j] = line.charAt(j-1);
                }
            }
            result = 45;
            count = 0;
            travel(0);
            sb.append(result+" "+count+"\n");

            if(k!=n)
                br.readLine();
        }

        System.out.println(sb);

        br.close();
    }

    static void travel(int cur)
    {
        for(int i=1;i<=5;i++)
        {
            for(int j=1;j<=9;j++)
            {
                if(board[i][j]=='o')
                {
                    for(int k=0;k<4;k++)
                    {
                        int nx = i + dx[k];
                        int ny = j + dy[k];

                        if(nx<1||nx>5||ny<1||ny>9)
                            continue;

                        if(board[nx][ny]=='.')
                            continue;

                        if(board[nx][ny]=='o')
                        {
                            int n2x = nx + dx[k];
                            int n2y = ny + dy[k];

                            if(n2x>=1&&n2x<=5&&n2y>=1&&n2y<=9)
                            {
                                if(board[n2x][n2y]=='.')
                                {
                                    board[nx][ny]='.';
                                    board[n2x][n2y]='o';
                                    board[i][j] = '.';
                                    travel(cur + 1);
                                    board[nx][ny]='o';
                                    board[i][j] = 'o';
                                    board[n2x][n2y] = '.';
                                }
                            }
                        }
                    }
                }
            }
        }
        int tmp = sum();
        if(result > tmp)
        {
            result = tmp;
            count = cur;
        }
    }

    static int sum()
    {
        int count = 0;

        for(int i=1;i<=5;i++)
        {
            for(int j=1;j<=9;j++)
            {
                if(board[i][j]=='o')
                    count = count + 1;
            }
        }

        return count;
    }
}
```
