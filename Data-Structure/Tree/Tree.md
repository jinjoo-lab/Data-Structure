# 트리

### 트리

![Untitled](https://private-user-images.githubusercontent.com/84346055/296761684-bdd058e8-4544-4787-b37b-218d9075a82d.png?jwt=eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpc3MiOiJnaXRodWIuY29tIiwiYXVkIjoicmF3LmdpdGh1YnVzZXJjb250ZW50LmNvbSIsImtleSI6ImtleTUiLCJleHAiOjE3MDUzMjM4MjYsIm5iZiI6MTcwNTMyMzUyNiwicGF0aCI6Ii84NDM0NjA1NS8yOTY3NjE2ODQtYmRkMDU4ZTgtNDU0NC00Nzg3LWIzN2ItMjE4ZDkwNzVhODJkLnBuZz9YLUFtei1BbGdvcml0aG09QVdTNC1ITUFDLVNIQTI1NiZYLUFtei1DcmVkZW50aWFsPUFLSUFWQ09EWUxTQTUzUFFLNFpBJTJGMjAyNDAxMTUlMkZ1cy1lYXN0LTElMkZzMyUyRmF3czRfcmVxdWVzdCZYLUFtei1EYXRlPTIwMjQwMTE1VDEyNTg0NlomWC1BbXotRXhwaXJlcz0zMDAmWC1BbXotU2lnbmF0dXJlPTU0NTgzNDY2YTQ1ZjEzODYzNjhjMTQ1OTllMjMzM2NmMDY0YzRlOWZjNjFhNjllYTYxMjBhNDdlYWUyMmNhMGYmWC1BbXotU2lnbmVkSGVhZGVycz1ob3N0JmFjdG9yX2lkPTAma2V5X2lkPTAmcmVwb19pZD0wIn0.k5vdBZQAOg59PpA-rAVh4_VcEVrYd0KAhrM2ZFdGKw0)

- **사이클이 없는 한개 이상의 노드로 이루어진 연결(Connected) 그래프**
- 특징
    - 트리에는 사이클이 존재하지 않는다.
    - **한 노드로부터 다른 노드까지의 경로는 오직 1개이다 !**
    - 노드 중 루트 노드를 제외하고는 모두 부모 노드가 있다.
    - **V개의 정점을 가지고 있다면 간선은 V-1개이다.**
- 그래프는 집합의 개념이기 때문에 트리 또한 집합으로 바라볼 수 있다.

> 나머지 노드들은 n ≥ 0 의 분리집합으로 분리되며 이 분리 집합들은 루트의 서브트리 !
>

### 용어

- 단말 노드 : 차수가 0인 노드 (서브트리를 가지지 않는다. 자식 노드가 없다)
- 부모 노드 : 서브트리를 가지고 있는 노드를 서브트리의 부모노드 !
- 자식 노드 : 서브트리를 부모노드의 자식 노드
- 형제 노드 : 같은 부모 노드를 가지고 있는 노드들
- 조상 노드 : 특정 노드 → 루트 노드까지의 경로에 존재하는 노드

### 트리란 자료구조?

- 트리는 검색에 최적화되어 있는 자료구조이다.

### 트리에서의 BFS

![Untitled](https://private-user-images.githubusercontent.com/84346055/296761738-1f705882-3700-44a0-a723-28749b921edb.png?jwt=eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpc3MiOiJnaXRodWIuY29tIiwiYXVkIjoicmF3LmdpdGh1YnVzZXJjb250ZW50LmNvbSIsImtleSI6ImtleTUiLCJleHAiOjE3MDUzMjM4MjYsIm5iZiI6MTcwNTMyMzUyNiwicGF0aCI6Ii84NDM0NjA1NS8yOTY3NjE3MzgtMWY3MDU4ODItMzcwMC00NGEwLWE3MjMtMjg3NDliOTIxZWRiLnBuZz9YLUFtei1BbGdvcml0aG09QVdTNC1ITUFDLVNIQTI1NiZYLUFtei1DcmVkZW50aWFsPUFLSUFWQ09EWUxTQTUzUFFLNFpBJTJGMjAyNDAxMTUlMkZ1cy1lYXN0LTElMkZzMyUyRmF3czRfcmVxdWVzdCZYLUFtei1EYXRlPTIwMjQwMTE1VDEyNTg0NlomWC1BbXotRXhwaXJlcz0zMDAmWC1BbXotU2lnbmF0dXJlPTAyNGYxMmI3YjMzZWVlYzgyNjhhNDczYTE3ZDhiNGRlYjg0NzdjYjQ3NzJhZWRhMmYzNDkzZWE1YzFjN2M5MGQmWC1BbXotU2lnbmVkSGVhZGVycz1ob3N0JmFjdG9yX2lkPTAma2V5X2lkPTAmcmVwb19pZD0wIn0.wTEDb0DkVCyWucZKWH2lQ-9s9DA973Qk6lviFEDLb8A)

- 탐색 순서 : 1 → ( 2, 3, 4) → (5, 6) → (7, 8)
- O(V + E)
- 루트 노드를 기점으로 방문 값 **: 노드의 레벨**
    - 부모 노드가 아니라면 탐색 지속하도록 코드 작성 ( 자식 노드만 가도록 )
        - 트리의 특징 : vis 배열이 아닌 p 배열로 부모의 정보만 기입
        - depth도 탐색 가능
    - 시작점을 루트로 잡고 탐색한다면 **높이 순으로 탐색**

```
int[] p = new int[n];
int[] depth = new int[n];
Queue<Integer> q = new LinkedList<>();
q.add(root);

while(!q.isEmpty()){
	int cur = q.poll();

	for(int next : graph[cur]){
			if(next == p[cur] continue; // 부모일 경우 건너뛰기
			q.push(next);
			p[next] = cur;
			depth[next] = depth[cur] + 1;
	}
}
```

### 트리에서의 DFS

![Untitled](https://private-user-images.githubusercontent.com/84346055/296761738-1f705882-3700-44a0-a723-28749b921edb.png?jwt=eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpc3MiOiJnaXRodWIuY29tIiwiYXVkIjoicmF3LmdpdGh1YnVzZXJjb250ZW50LmNvbSIsImtleSI6ImtleTUiLCJleHAiOjE3MDUzMjM4MjYsIm5iZiI6MTcwNTMyMzUyNiwicGF0aCI6Ii84NDM0NjA1NS8yOTY3NjE3MzgtMWY3MDU4ODItMzcwMC00NGEwLWE3MjMtMjg3NDliOTIxZWRiLnBuZz9YLUFtei1BbGdvcml0aG09QVdTNC1ITUFDLVNIQTI1NiZYLUFtei1DcmVkZW50aWFsPUFLSUFWQ09EWUxTQTUzUFFLNFpBJTJGMjAyNDAxMTUlMkZ1cy1lYXN0LTElMkZzMyUyRmF3czRfcmVxdWVzdCZYLUFtei1EYXRlPTIwMjQwMTE1VDEyNTg0NlomWC1BbXotRXhwaXJlcz0zMDAmWC1BbXotU2lnbmF0dXJlPTAyNGYxMmI3YjMzZWVlYzgyNjhhNDczYTE3ZDhiNGRlYjg0NzdjYjQ3NzJhZWRhMmYzNDkzZWE1YzFjN2M5MGQmWC1BbXotU2lnbmVkSGVhZGVycz1ob3N0JmFjdG9yX2lkPTAma2V5X2lkPTAmcmVwb19pZD0wIn0.wTEDb0DkVCyWucZKWH2lQ-9s9DA973Qk6lviFEDLb8A)

- 탐색 순서 : 1 → 2 → 5 → 3 → 4 → 6 → 7 → 8
- O(V + E)
- 부모 배열과 depth 배열을 채우는 것은 동일

### 이진 트리

- 자식 노드가 최대 2개까지 가능한 트리
- 특징
    - 왼쪽 자식과 오른쪽 자식이 **구분**된다!

![Untitled](https://private-user-images.githubusercontent.com/84346055/296761757-c5798b6a-a076-484a-a7e4-21267730b68d.png?jwt=eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpc3MiOiJnaXRodWIuY29tIiwiYXVkIjoicmF3LmdpdGh1YnVzZXJjb250ZW50LmNvbSIsImtleSI6ImtleTUiLCJleHAiOjE3MDUzMjM4MjYsIm5iZiI6MTcwNTMyMzUyNiwicGF0aCI6Ii84NDM0NjA1NS8yOTY3NjE3NTctYzU3OThiNmEtYTA3Ni00ODRhLWE3ZTQtMjEyNjc3MzBiNjhkLnBuZz9YLUFtei1BbGdvcml0aG09QVdTNC1ITUFDLVNIQTI1NiZYLUFtei1DcmVkZW50aWFsPUFLSUFWQ09EWUxTQTUzUFFLNFpBJTJGMjAyNDAxMTUlMkZ1cy1lYXN0LTElMkZzMyUyRmF3czRfcmVxdWVzdCZYLUFtei1EYXRlPTIwMjQwMTE1VDEyNTg0NlomWC1BbXotRXhwaXJlcz0zMDAmWC1BbXotU2lnbmF0dXJlPTVjNjg0OGNiNTY3ZmUzNmUwZTU1NWQ2NDI4YzcwMmU0OGFmNDc4Yjc1ZWNjYzRlNGNiMGNkNGIzZDRlZDFmNzgmWC1BbXotU2lnbmVkSGVhZGVycz1ob3N0JmFjdG9yX2lkPTAma2V5X2lkPTAmcmVwb19pZD0wIn0.Nq_dVqCgv4z-dSQbmwpBEsENVkBl8juh-dLhgOlDnkw)

### 포화 이진 트리 (Full Binary Tree)

- 최고 레벨에 대해 가질 수 있는 모든 노드를 가지고 있는 트리 !
- 노드의 개수 : 레벨 k

  $$
  2^k -1 (lev = k)
  $$


![Untitled](https://private-user-images.githubusercontent.com/84346055/296761760-6d1f2547-fc42-4bb5-a713-43f289a9676f.png?jwt=eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpc3MiOiJnaXRodWIuY29tIiwiYXVkIjoicmF3LmdpdGh1YnVzZXJjb250ZW50LmNvbSIsImtleSI6ImtleTUiLCJleHAiOjE3MDUzMjM4MjYsIm5iZiI6MTcwNTMyMzUyNiwicGF0aCI6Ii84NDM0NjA1NS8yOTY3NjE3NjAtNmQxZjI1NDctZmM0Mi00YmI1LWE3MTMtNDNmMjg5YTk2NzZmLnBuZz9YLUFtei1BbGdvcml0aG09QVdTNC1ITUFDLVNIQTI1NiZYLUFtei1DcmVkZW50aWFsPUFLSUFWQ09EWUxTQTUzUFFLNFpBJTJGMjAyNDAxMTUlMkZ1cy1lYXN0LTElMkZzMyUyRmF3czRfcmVxdWVzdCZYLUFtei1EYXRlPTIwMjQwMTE1VDEyNTg0NlomWC1BbXotRXhwaXJlcz0zMDAmWC1BbXotU2lnbmF0dXJlPWVmYmE2YzhjZTMwZGMwN2UyNjk5MjIwMjFlMTQ5YjhkZDQxMWY2ZWFkZDdlNDYwYzFkMWY0OGNlNGM0ZTkzMDImWC1BbXotU2lnbmVkSGVhZGVycz1ob3N0JmFjdG9yX2lkPTAma2V5X2lkPTAmcmVwb19pZD0wIn0.flV85q4JwJXcHZoRjq4EgmF2Pg2LH0Lf2N1-Ud6nuAw)

### 완전 이진 트리

**조건**

- 최고 레벨 k에 대하여 k-1레벨 까지는 Full - Binary Tree
- 레벨 k에서는 왼쪽부터 순서대로 노드가 채워진다.

![Untitled](https://private-user-images.githubusercontent.com/84346055/296761761-8bd141ac-1678-4c93-afd7-664e7da2b8f2.png?jwt=eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpc3MiOiJnaXRodWIuY29tIiwiYXVkIjoicmF3LmdpdGh1YnVzZXJjb250ZW50LmNvbSIsImtleSI6ImtleTUiLCJleHAiOjE3MDUzMjM4MjYsIm5iZiI6MTcwNTMyMzUyNiwicGF0aCI6Ii84NDM0NjA1NS8yOTY3NjE3NjEtOGJkMTQxYWMtMTY3OC00YzkzLWFmZDctNjY0ZTdkYTJiOGYyLnBuZz9YLUFtei1BbGdvcml0aG09QVdTNC1ITUFDLVNIQTI1NiZYLUFtei1DcmVkZW50aWFsPUFLSUFWQ09EWUxTQTUzUFFLNFpBJTJGMjAyNDAxMTUlMkZ1cy1lYXN0LTElMkZzMyUyRmF3czRfcmVxdWVzdCZYLUFtei1EYXRlPTIwMjQwMTE1VDEyNTg0NlomWC1BbXotRXhwaXJlcz0zMDAmWC1BbXotU2lnbmF0dXJlPWQ3NzQ2YzJlZjA1MjgzOGY0NDIzZmRjM2IzZDJiN2MzMDQ4YjNhMzk4YmZiZDBkYmExYzNmMGJjMTJjOGUzOWQmWC1BbXotU2lnbmVkSGVhZGVycz1ob3N0JmFjdG9yX2lkPTAma2V5X2lkPTAmcmVwb19pZD0wIn0.Yw6UGC31j6kXKNEo9dN0oJWP_oZ87X_TB8smDQdg_tk)

## 트리 순회

- 트리의 순회는 기본적으로 재귀적인 방식이다.
- 구분 기준은 **‘루트 노드를 언제 방문하는가’** 이다.

![Untitled](https://private-user-images.githubusercontent.com/84346055/296761764-5cc28578-f812-4f4b-8b45-adec02bcaea6.png?jwt=eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpc3MiOiJnaXRodWIuY29tIiwiYXVkIjoicmF3LmdpdGh1YnVzZXJjb250ZW50LmNvbSIsImtleSI6ImtleTUiLCJleHAiOjE3MDUzMjM4MjYsIm5iZiI6MTcwNTMyMzUyNiwicGF0aCI6Ii84NDM0NjA1NS8yOTY3NjE3NjQtNWNjMjg1NzgtZjgxMi00ZjRiLThiNDUtYWRlYzAyYmNhZWE2LnBuZz9YLUFtei1BbGdvcml0aG09QVdTNC1ITUFDLVNIQTI1NiZYLUFtei1DcmVkZW50aWFsPUFLSUFWQ09EWUxTQTUzUFFLNFpBJTJGMjAyNDAxMTUlMkZ1cy1lYXN0LTElMkZzMyUyRmF3czRfcmVxdWVzdCZYLUFtei1EYXRlPTIwMjQwMTE1VDEyNTg0NlomWC1BbXotRXhwaXJlcz0zMDAmWC1BbXotU2lnbmF0dXJlPWE4MTE5Nzg1NzU4MDRhN2VmOWQ2ODhkN2I1MTdhNWIwNjVkNDg2MGQ4YWY2ZGQ3ODAwMmNhNDcxMTMxOGRmOWQmWC1BbXotU2lnbmVkSGVhZGVycz1ob3N0JmFjdG9yX2lkPTAma2V5X2lkPTAmcmVwb19pZD0wIn0.kPDt25c3lTLTSfu5suUjTSjwigatn64Qj_huAmys4Eg)

1. 전위 순회
    - **루트** 노드 → **왼쪽 서브** 트리 → **오른쪽 서브** 트리
- **전위 순회 결과**

    ![Untitled](https://private-user-images.githubusercontent.com/84346055/296761768-3bc05903-92eb-41d4-b62c-fbe5aaa71f8c.png?jwt=eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpc3MiOiJnaXRodWIuY29tIiwiYXVkIjoicmF3LmdpdGh1YnVzZXJjb250ZW50LmNvbSIsImtleSI6ImtleTUiLCJleHAiOjE3MDUzMjM4MjYsIm5iZiI6MTcwNTMyMzUyNiwicGF0aCI6Ii84NDM0NjA1NS8yOTY3NjE3NjgtM2JjMDU5MDMtOTJlYi00MWQ0LWI2MmMtZmJlNWFhYTcxZjhjLnBuZz9YLUFtei1BbGdvcml0aG09QVdTNC1ITUFDLVNIQTI1NiZYLUFtei1DcmVkZW50aWFsPUFLSUFWQ09EWUxTQTUzUFFLNFpBJTJGMjAyNDAxMTUlMkZ1cy1lYXN0LTElMkZzMyUyRmF3czRfcmVxdWVzdCZYLUFtei1EYXRlPTIwMjQwMTE1VDEyNTg0NlomWC1BbXotRXhwaXJlcz0zMDAmWC1BbXotU2lnbmF0dXJlPTJkNTgxMWZiMGVkNzUwN2FhYzY1Y2I2NWQ3YjM1YzAyOWFiOTkzZTJkNzIwN2QzMWQyOThmZTk3Y2Q0Y2RlNWMmWC1BbXotU2lnbmVkSGVhZGVycz1ob3N0JmFjdG9yX2lkPTAma2V5X2lkPTAmcmVwb19pZD0wIn0.OlbYDfGztooh9oyMRKR-rCjhMqG2qIMRw71V7Ab7I8g)

**구현**

```
public void preOrder(Node node)
{
		if(node != null)
		{
				// root 처리
				if(node.left != null)
						preOrder(node.left);
				if(node.right != null)
						preOrder(node.right);
		}
}
```

1. 중위 순회
    - **왼쪽** 서브 트리 → **루트** 노드 → **오른쪽** 서브 트리
- **중위 순회 결과**

  ![Untitled](https://private-user-images.githubusercontent.com/84346055/296761773-98894032-d5b5-49cd-a07e-dd63738c7093.png?jwt=eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpc3MiOiJnaXRodWIuY29tIiwiYXVkIjoicmF3LmdpdGh1YnVzZXJjb250ZW50LmNvbSIsImtleSI6ImtleTUiLCJleHAiOjE3MDUzMjM4MjYsIm5iZiI6MTcwNTMyMzUyNiwicGF0aCI6Ii84NDM0NjA1NS8yOTY3NjE3NzMtOTg4OTQwMzItZDViNS00OWNkLWEwN2UtZGQ2MzczOGM3MDkzLnBuZz9YLUFtei1BbGdvcml0aG09QVdTNC1ITUFDLVNIQTI1NiZYLUFtei1DcmVkZW50aWFsPUFLSUFWQ09EWUxTQTUzUFFLNFpBJTJGMjAyNDAxMTUlMkZ1cy1lYXN0LTElMkZzMyUyRmF3czRfcmVxdWVzdCZYLUFtei1EYXRlPTIwMjQwMTE1VDEyNTg0NlomWC1BbXotRXhwaXJlcz0zMDAmWC1BbXotU2lnbmF0dXJlPWFlNWE4YTY0Y2Q0MTU2MzdhZmMzMmZlOTNjNDEzYzJlYTQxY2FhMzA4YTVkNDRhNzhjZmVkOGNiZDExZTkwMTgmWC1BbXotU2lnbmVkSGVhZGVycz1ob3N0JmFjdG9yX2lkPTAma2V5X2lkPTAmcmVwb19pZD0wIn0.9FCHzjm9s5rQARfq_jRcXb4t2XVDOas8VDVSPre2qlA)


```
public void inOrder(Node node)
{
		if(node != null)
		{
				if(node.left != null)
						inOrder(node.left);
				// root 처리
				if(node.right != null)
						inOrder(node.right);
		}
}
```

1. 후위 순회
    - **왼쪽** 서브 트리 → **오른쪽** 서브 트리 → **루트** 노드
- **후위 순회 결과**

  ![Untitled](https://private-user-images.githubusercontent.com/84346055/296761777-2d33de28-cee9-40da-9f75-555a2eb36b4a.png?jwt=eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpc3MiOiJnaXRodWIuY29tIiwiYXVkIjoicmF3LmdpdGh1YnVzZXJjb250ZW50LmNvbSIsImtleSI6ImtleTUiLCJleHAiOjE3MDUzMjM4MjYsIm5iZiI6MTcwNTMyMzUyNiwicGF0aCI6Ii84NDM0NjA1NS8yOTY3NjE3NzctMmQzM2RlMjgtY2VlOS00MGRhLTlmNzUtNTU1YTJlYjM2YjRhLnBuZz9YLUFtei1BbGdvcml0aG09QVdTNC1ITUFDLVNIQTI1NiZYLUFtei1DcmVkZW50aWFsPUFLSUFWQ09EWUxTQTUzUFFLNFpBJTJGMjAyNDAxMTUlMkZ1cy1lYXN0LTElMkZzMyUyRmF3czRfcmVxdWVzdCZYLUFtei1EYXRlPTIwMjQwMTE1VDEyNTg0NlomWC1BbXotRXhwaXJlcz0zMDAmWC1BbXotU2lnbmF0dXJlPWM4MGFjMTY3OTZhN2VmM2UxZmFmNDZhYTZkYTM0OGE1ZmIyMWJjMjQwN2ZiNmUyZDY2MWY2MDI1MmZhZjBiZDMmWC1BbXotU2lnbmVkSGVhZGVycz1ob3N0JmFjdG9yX2lkPTAma2V5X2lkPTAmcmVwb19pZD0wIn0.TsMVjpz3Z8WKVRIzQkTTJkCe-R8WMgVHPpTmq5DD_YY)


```
public void postOrder(Node node)
{
		if(node != null)
		{
				if(node.left != null)
						postOrder(node.left);
				if(node.right != null)
						postOrder(node.right);
				// root 처리
		}
}
```

### 예제

- **이진 트리 순회**

[1991번: 트리 순회](https://www.acmicpc.net/problem/1991)

- **트리에서 부모 찾기**

[11725번: 트리의 부모 찾기](https://www.acmicpc.net/problem/11725)
