# 다익스트라

다익스트라(Dijkstra) : DP + Greed → 하나의 정점에서 모든 정점으로의 최단 경로 탐색 알고리즘

- 최단 거리는 여러 개의 최단 거리로 이루어져 있다.
- 음의 가중치가 없는 그래프여야 한다.

![Alt text](https://user-images.githubusercontent.com/84346055/267598186-df7e5099-5855-4777-9980-42a8e37d0ec1.png)

![Alt text](https://user-images.githubusercontent.com/84346055/267598227-0d9e8c14-829f-4dc8-9335-84b4d60ef5a3.png)

![Alt text](https://user-images.githubusercontent.com/84346055/267598232-b6d2a177-6e9d-4004-a4f9-cd52347b64d5.png)

**동작 과정**

1. 출발 노드 설정
2. 출발 노드를 기준으로 각 노드의 최소 비용을 저장
3. 방문하지 않은 노드 중에서 가장 비용이 적은 노드 선택
4. 해당 노드를 거쳐서 특정한 노드로 가는 경우를 고려하여 최소 비용 갱신
5. 3 ~ 4번 반복

![Alt text](https://user-images.githubusercontent.com/84346055/267598237-ea5640ec-ab9f-4e8e-b057-c2d6a3ad70f0.png)

- 진행과정

  ![Alt text](https://user-images.githubusercontent.com/84346055/267598242-88381c65-9905-40ed-86d2-e02ed1587e9f.png)

  ![Alt text](https://user-images.githubusercontent.com/84346055/267598245-d52dad71-2ea7-4129-b951-65739c6b2f69.png)

  ![Alt text](https://user-images.githubusercontent.com/84346055/267598250-41f1ccc2-bb46-4c3c-9720-0626a42d1849.png)

  ![Alt text](https://user-images.githubusercontent.com/84346055/267598257-c3160dba-7ae0-4ff3-aaa0-83693d6f1df9.png)

  ![Alt text](https://user-images.githubusercontent.com/84346055/267598260-d3b136f7-a968-4ad5-93ea-6c0a713f94a4.png)

- 현재 최소 비용을 갖는 노드를 선택한 후, 그렇게 선택이 된 노드는 다시는 최소 비용의 갱신이 이루어지지 않았다. (방문한 노드는 다시 방문하지 않는다) → 그 이유는?

  **다익스트라 알고리즘은 그리디 알고리즘**이다. 쉽게 말해 다익스트라 알고리즘의 기본적인 아이디어는 **'최단 거리는 최단 거리로 이루어져 있다'**, 다르게 말해 **'최단 거리를 이어 붙여서 최단 거리를 만든다'**는 것이다. 즉, 그리디 알고리즘의 최적 부분 구조 조건이 성립하기 때문에 위와 같은 결과가 발생하는 것이다.

    - **※ 다익스트라 알고리즘 증명**
        - >**가설 : 이미 선택된 노드는 최단 거리가 갱신되지 않는다(즉, 다익스트라 알고리즘으로 선택된 노드는 최종 최소 비용이다).**
        - >우리는 지금부터 이 가설을 증명하기 위해 할 것이다.

          **귀류법을 사용**


(1) **이미 선택된 노드는 앞으로 선택되는 노드에 의해서 최단 거리가 갱신이 된다라고 가정**해보자. **즉, 이후 선택하는노드를 거쳐 들어오는 더 짧은 최단 경로가 존재한다**고 생각해보자.
        
(2) **만일 그러한 노드가 존재한다면, 해당 노드는 적어도 한 번 다익스트라 알고리즘을 이용해 거쳐온 노드외의 노드를 지나야만 한다.** 이 사실은 조금만 생각해보면 당연한 이야기이다. 왜냐하면, **다익스트라 알고리즘으로 선택되어진 모든 노드만을 거쳐서 지나온다면, 해당 노드는 다익스트라 알고리즘으로 선택된 노드의 최소 비용을 갱신할 수 없다.** 아래 그림을 보며 이해해보자.
        
![https://blog.kakaocdn.net/dn/c9PNU6/btqZ1bu4I9i/xJ9qsCYuhCCkkvc3kI0kXK/img.png](https://blog.kakaocdn.net/dn/c9PNU6/btqZ1bu4I9i/xJ9qsCYuhCCkkvc3kI0kXK/img.png)
        
(3) 즉, 다음과 같이 다익스트라 알고리즘으로 선택된 경로 외에 다른 노드에서 들어오는 경로가 존재할 것이다.
        
![https://blog.kakaocdn.net/dn/cNOjM8/btqZ0sDOkv2/RkU7PGfllHr3N4VhSMM4FK/img.png](https://blog.kakaocdn.net/dn/cNOjM8/btqZ0sDOkv2/RkU7PGfllHr3N4VhSMM4FK/img.png)
        
(4) 하지만 이 사실은 잘 생각해보면 **모순되는 부분을 가지고 있다.** 어떤 부분일까? 애초에 다익스트라 알고리즘이 어떻게 진행되고 있었는지를 생각해보자. **다익스트라 알고리즘에서 다음 노드를 선택하는 기준이 무엇이었는가? 그렇다. 'E'라는 노드를 선택하는 기준은 현재 E가 가지고 있는 비용이 최소였기 때문에 선택한 것이다!** 그런데, 만약 저러한 노드가 존재하는 상황이 발생한다면 **우리는 정해진 규칙에 따라서 다익스트라 알고리즘을 진행하지 않은 것이다.** 만일, 해당 노드를 Z라고 가정한다면 **Z부터 E까지의 간선의 길이는 0 보다 큰 값을 가지고 있을 것(음의 가중치를 가지면 안되는 이유)**이다. 즉, **시작 노드 S부터 노드 Z까지의 길이는 시작 노드 S부터 E까지의 거리보다 짧다!** 다익스트라 알고리즘은 분명 매번 최소 비용을 갖는 노드만을 선택한다고 하였는데, 그것보다 더 짧은 비용을 갖는 노드가 존재한다고하면 당연히 모순이다.
        
![https://blog.kakaocdn.net/dn/bIA8Kl/btqZ6jZHKxb/3UHmVfPxaok2AACjCPRkU1/img.png](https://blog.kakaocdn.net/dn/bIA8Kl/btqZ6jZHKxb/3UHmVfPxaok2AACjCPRkU1/img.png)
        
(5) 즉, **초기에 설정한 가정**(이미 선택된 노드는 앞으로 선택되는 정점에 의해서 최단 거리가 갱신이 된다)**은 모순**이다. 즉, **귀류 가정이 모순이므로, 본 명제는 참**임을 알 수 있다


## **다익스트라 알고리즘의 구현 (배열)**

- 한 번 방문한 배열은 방문할 수 없으므로 **방문 배열**이 필요하고, **각 노드까지의 최소 비용을 저장하는 배열**이 필요하다.
- 이때, 미 방문 배열을 최대값으로 초기화한다.
- 시간복잡도

  **최소 비용을 갖는 노드을 선택하는 과정**은 앞선 일반적인 구현에서는 **최악의 경우 모든 노드을 확인해야 하고, 이 것은 V번 반복하기 때문에 O(V^2)의 시간 복잡도**를 갖는다.

- 코드

    ```java
    class Node {
    	int idx;
    	int cost;
    
    	// 생성자
    	Node(int idx, int cost) {
    		this.idx = idx;
    		this.cost = cost;
    	}
    }
    
    public class Dijkstra {
    	public static void main(String[] args) {
    		Scanner sc = new Scanner(System.in);
    		// 노드와 간선의 개수
    		int V = sc.nextInt();
    		int E = sc.nextInt();
    		// 출발지점
    		int start = sc.nextInt();
    
    		// 1. 인접리스트를 이용한 그래프 초기화
    		ArrayList<ArrayList<Node>> graph = new ArrayList<ArrayList<Node>>();
    		// 노드의 번호가 1부터 시작하므로, 0번 인덱스 부분을 임의로 만들어 놓기만 한다.
    		for (int i = 0; i < V + 1; i++) {
    			graph.add(new ArrayList<>());
    		}
    		// 그래프에 값을 넣는다.
    		for (int i = 0; i < E; i++) {
    			// a로 부터 b로 가는 값은 cost이다.
    			int a = sc.nextInt();
    			int b = sc.nextInt();
    			int cost = sc.nextInt();
    
    			graph.get(a).add(new Node(b, cost));
    		}
    
    		// 2. 방문 여부를 확인할 boolean 배열, start 노드부터 end 노드 까지의 최소 거리를 저장할 배열을 만든다.
    		boolean[] visited = new boolean[V + 1];
    		int[] dist = new int[V + 1];
    
    		// 3. 최소 거리 정보를 담을 배열을 초기화 한다.
    		for (int i = 0; i < V + 1; i++) {
    			// 출발 지점 외 나머지 지점까지의 최소 비용은 최대로 지정해둔다.
    			dist[i] = Integer.MAX_VALUE;
    		}
    		// 출발 지점의 비용은 0으로 시작한다.
    		dist[start] = 0;
    
    		// 4. 다익스트라 알고리즘을 진행한다.
    		// 모든 노드을 방문하면 종료하기 때문에, 노드의 개수 만큼만 반복을 한다.
    		for (int i = 0; i < V; i++) {
    			// 4 - 1. 현재 거리 비용 중 최소인 지점을 선택한다.
    			// 해당 노드가 가지고 있는 현재 비용.
    			int nodeValue = Integer.MAX_VALUE;
    			// 해당 노드의 인덱스(번호).
    			int nodeIdx = 0;
    			// 인덱스 0은 생각하지 않기 때문에 0부터 반복을 진행한다.
    			for (int j = 1; j < V + 1; j++) {
    				// 해당 노드를 방문하지 않았고, 현재 모든 거리비용 중 최솟값을 찾는다.
    				if (!visited[j] && dist[j] < nodeValue) {
    					nodeValue = dist[j];
    					nodeIdx = j;
    				}
    			}
    			// 최종 선택된 노드를 방문처리 한다.
    			visited[nodeIdx] = true;
    
    			// 4 - 2. 해당 지점을 기준으로 인접 노드의 최소 거리 값을 갱신한다.
    			for (int j = 0; j < graph.get(nodeIdx).size(); j++) {
    				// 인접 노드를 선택한다.
    				Node adjNode = graph.get(nodeIdx).get(j);
    				// 인접 노드가 현재 가지는 최소 비용과
    				// 현재 선택된 노드의 값 + 현재 노드에서 인접 노드로 가는 값을 비교하여 더 작은 값으로 갱신한다.
    				if (dist[adjNode.idx] > dist[nodeIdx] + adjNode.cost) {
    					dist[adjNode.idx] = dist[nodeIdx] + adjNode.cost;
    				}
    			}
    		}
    
    		// 5. 최종 비용을 출력한다.
    		for (int i = 1; i < V + 1; i++) {
    			if (dist[i] == Integer.MAX_VALUE) {
    				System.out.println("INF");
    			} else {
    				System.out.println(dist[i]);
    			}
    		}
    		sc.close();
    	}
    }
    ```


## **다익스트라 알고리즘의 구현(우선순위 큐 이용)**

- 노드 선택 후, 방문하지 않은 인접한 노드를 우선순위 큐에 집어넣는다.
- 큐에서 값을 뺀 후, 방문하지 않았으면 최소비용을 갱신해주고, 주변 노드를 우선순위 큐에 넣는다.
- 시간복잡도

  **최소 비용을 갖는 노드을 선택하는 과정**은 앞선 일반적인 구현에서는 **최악의 경우 모든 노드을 확인해야 하고, 이 것은 V번 반복하기 때문에 O((V+E)log V)의 시간 복잡도**를 갖는다.

- 코드

    ```java
    public class Dijkstra2 {
    	static int V, E, start;
    	static ArrayList<ArrayList<Node>> graph;
    
    	static class Node {// 다음 노드의 인덱스와, 그 노드로 가는데 필요한 비용을 담고 있다.
    		int idx, cost;
    
    		Node(int idx, int cost) {
    			this.idx = idx;
    			this.cost = cost;
    		}
    	}
    
    	public static void main(String[] args) throws IOException {
    		// 초기화
    		BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
    		StringTokenizer st = new StringTokenizer(br.readLine());
    		V = Integer.parseInt(st.nextToken());
    		E = Integer.parseInt(st.nextToken());
    		start = Integer.parseInt(br.readLine());
    		graph = new ArrayList<ArrayList<Node>>();
    		for (int i = 0; i < V + 1; i++) {
    			graph.add(new ArrayList<Node>());
    		}
    		for (int i = 0; i < E; i++) {
    			st = new StringTokenizer(br.readLine());
    			int s = Integer.parseInt(st.nextToken());
    			int e = Integer.parseInt(st.nextToken());
    			int c = Integer.parseInt(st.nextToken());
    			// 문제에서는 유향 그래프에서의 다익스트라 알고리즘(이 조건도 문제에 따라 중요하다!).
    			graph.get(s).add(new Node(e, c));
    		}
    
    		// 다익스트라 알고리즘 초기화
    		int[] dist = new int[V + 1]; // 최소 비용을 저장할 배열
    		for (int i = 0; i < V + 1; i++) {
    			dist[i] = Integer.MAX_VALUE;
    		}
    
    		// 주의점 1. 다익스트라 알고리즘의 최소비용을 기준으로 추출해야 한다. 최대 비용을 기준으로 하는 경우 최악의 경우 지수시간 만큼의 연산을
    		// 해야한다!
    		PriorityQueue<Node> q = new PriorityQueue<Node>((o1, o2) -> Integer.compare(o1.cost, o2.cost));
    		// 시작 노드에서, 시작 노드로 가는 값이 초기에 가장 짧은 비용을 갖는 노드이다.
    		// 즉, 도착 정점은 start, 비용은 0인 노드를 가장 먼저 선택할 것이다.
    		q.offer(new Node(start, 0));
    		// 해당 노드를 선택한 것이나 마찬가지 이므로, dist[start] = 0으로 갱신.
    		dist[start] = 0;
    
    		while (!pq.isEmpty()) {
                Node curNode = pq.poll();
                int cur = curNode.end;
    
                if (visited[cur]) continue;
                visited[cur] = true;
    
                for (Node node :
                        list.get(cur)) {
                    if (!visited[node.end] && dist[node.end] > dist[cur] + node.weight) {
                        dist[node.end] = dist[cur] + node.weight;
                        pq.add(new Node(node.end, dist[node.end]));
                    }
                }
            }
    
    		// 결과 출력
    		System.out.println(Arrays.toString(dist));
    	}
    }
    ```


# 플루이드 워셜

플로이드 워샬(Floyd Warshall) → 모든 정점에서 다른 모든 정점으로의 최단 경로 탐색 알고리즘

음의 가중치가 있어도 되지만, 음의 사이클이 있으면 안된다.

- 시간복잡도

  O(V^3)

- 코드

    ```java
    public class FloydWarshall {
    
    	public static void main(String[] args) {
    		int[][] a = {{1,2,5}, {2,1,7},{3,1,2},{1,4,8},{2,3,9},
    				{3,4,3}, {4,3,3}};
    		int n =4;
    		solution(n,a);
    	}
    	
    	static void solution(int n, int[][] arr) {
    		int[][] floyd = new int[n][n];
    		
    		// 결과 그래프 초기화 
    		for(int i=0; i<n; i++) {
    			for(int j=0; j<n; j++){
    				if(i==j) {
    					floyd[i][j]	 =0;
    				}else floyd[i][j] = 1_000_000_000;
    			}
    		}
    		
    		// 결과 그래프 입력 
    		for(int i=0; i<arr.length; i++) {
    			floyd[arr[i][0]-1][arr[i][1]-1] = arr[i][2];
    		}
    		
    		// k : 거쳐가는 노드 (기준) 
    		for(int k=0; k<n; k++) {
    			// i : 출발 노드  
    			for(int i=0; i<n; i++) {
    				// j : 도착 노드 
    				for(int j=0; j<n; j++) {
    					// i에서 j로 가는 최소 비용 VS 
    					//         i에서 노드 k로 가는 비용 + 노드 k에서 jY로 가는 비용
    					if(floyd[i][k] + floyd[k][j] < floyd[i][j]) {
    						floyd[i][j] = floyd[i][k] + floyd[k][j];
    					}
    				}
    			}
    		}
    		
    		for(int i=0; i<n; i++) {
    			for(int j=0; j<n; j++) {
    				System.out.print(floyd[i][j]+ " ");
    			}
    			System.out.println();
    		}
    	}
    }
    ```


# 다익스트라 vs 플루이드 워셜

- **Dijkstra 알고리즘**은 **하나의 정점**에서 출발했을 때 **다른 모든 정점**으로의 최단 경로를 구하는 알고리즘이다.
- 그에 반해 **Floyd Warshall 알고리즘**은 **모든 정점**에서 **다른 모든 정점**으로의 최단 경로를 구하는 알고리즘이다.

![img1.daumcdn.png](https://user-images.githubusercontent.com/84346055/267598314-3cfcd82d-acc4-424f-a1e4-e0edf0bad7f2.png)
