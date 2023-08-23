# 위상정렬

# 위상정렬

**시간복잡도 : O(V + E)**

**위상정렬(Topology Sort)**은 ‘순서가 정해져있는 작업’을 차례로 수행해야 할 때, 그 순서를 결정해 주기 위해 사용하는 알고리즘이다.

![Alt text](https://user-images.githubusercontent.com/84346055/262577918-0ddc7d82-9a55-4e08-8ba9-68754c127fcb.png)

- 위상정렬이 불가능한 경우

  사이클이 발생하는 그래프에서는 위상정렬을 사용할 수 없다.

  ![Alt text](https://user-images.githubusercontent.com/84346055/262577970-ee04ee4f-ab35-4174-b80e-bf8da462da52.png)

  따라서 → **DAG(Directed Acyclic Graph)**에서만 적용이 가능하다.


### 위상정렬 순서 (Queue)

1. 진입차수가 0인 방문하지 않은 정점을 큐에 삽입한다.
2. 큐에서 원소를 꺼내 연결된 모든 간선을 제거한다.
3. 간선 제거 이후에 진입차수가 0이 된 정점을 큐에 삽입한다.
4. 큐가 빌때까지 2~3번 과정을 반복한다.
5. 만약 모든 원소를 방문하기 전에 큐가 빈다면 사이클이 존재하는 것 이고, 모든 원소를 방문했다면 큐에서 꺼낸 순서가 위상 정렬의 결과이다.

```java
import java.util.*;
import java.io.*;

public class Main {
    static int n = 0;
    static int m = 0;
    static int[] count;
    static ArrayList<Integer>[] graph;
    public static void main(String[] args) throws IOException {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        StringTokenizer st = new StringTokenizer(br.readLine(), " ");

        n = Integer.parseInt(st.nextToken());
        m = Integer.parseInt(st.nextToken());
        count = new int[n+1];
        graph = new ArrayList[n+1];
        
				for(int i=1;i<=n;i++){
            graph[i] = new ArrayList<>();
        }

        for(int i=1;i<=m;i++){
            st = new StringTokenizer(br.readLine(), " ");
            int x = Integer.parseInt(st.nextToken());
            int y = Integer.parseInt(st.nextToken());

            graph[x].add(y);
            count[y] += 1;
        }

        Queue<Integer> q = new LinkedList<>();
        
				for(int i=1;i<=n;i++){
            if(count[i] == 0){
                q.add(i);
            }
        }

        while(!q.isEmpty()){
            int cur = q.poll();

            for(int next : graph[cur]){
                count[next] -= 1;

                if(count[next] == 0){
                    q.add(next);
                }
            }
        }

        br.close();
    }

}
```

- **예시**

  다음과 같은 그래프가 있을 때, 위상 정렬을 사용하여 순서를 구해보자.

  ![Alt text](https://user-images.githubusercontent.com/84346055/262577980-3c9cc0f3-b073-4882-9b51-410534ade257.png)

  ![Alt text](https://user-images.githubusercontent.com/84346055/262577981-98c62431-c9c3-4813-81ca-16edee95df7c.png)

  진입차수가 0인 정점 1을 큐에 삽입한다.

  ![Alt text](https://user-images.githubusercontent.com/84346055/262577984-50308dac-672e-4ad7-92c5-4122bb1cf728.png)

  ![Alt text](https://user-images.githubusercontent.com/84346055/262577984-50308dac-672e-4ad7-92c5-4122bb1cf728.png)

  위와 같이 1을 큐에서 빼내면서 연결되어있던 간선을 다 제거해준다.

  ![Alt text](https://user-images.githubusercontent.com/84346055/262577988-f4d0a8b1-681c-4dfe-8ea1-dab62bec9bb4.png)

  진입차수가 0인 새로운 정점들을 다시 큐에 삽입해준다.

  ![Alt text](https://user-images.githubusercontent.com/84346055/262577990-f9c1b520-c6c1-4963-960d-3e3227e85901.png)

  ![Alt text](https://user-images.githubusercontent.com/84346055/262577994-121de532-bf3f-48a9-8868-ceb68071a4f3.png)

  ![Alt text](https://user-images.githubusercontent.com/84346055/262577997-ce9b0433-d10f-42ab-80f2-bdfa9b2c74b3.png)

  ![Alt text](https://user-images.githubusercontent.com/84346055/262578003-8aefab65-df0d-495b-b395-ddc584a8f60f.png)

  ![Alt text](https://user-images.githubusercontent.com/84346055/262578005-db03339a-8d65-4ef1-b678-7d2e0445298e.png)


- 정석 예제

[2252번: 줄 세우기](https://www.acmicpc.net/problem/2252)

[14567번: 선수과목 (Prerequisite)](https://www.acmicpc.net/problem/14567)

- 시간 구하는 예제

[2056번: 작업](https://www.acmicpc.net/problem/2056)
