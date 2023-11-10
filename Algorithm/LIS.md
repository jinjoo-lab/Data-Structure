# LIS

## LIS

> 최장 증가 부분 수열 : 원소가 n개인 리스트에서 **가장 긴 길이의 부분 수열**
>
- 수열의 개념
    - 연속하지 않아도 된다. 하지만 인덱스는 증가해야 한다.
- Ex) { 1 , 2 , 4, 2, 5 }
    - LIS : { 1, 2, 4, 5}

## 방법

- LIS를 구하는 방법에는 **DP , 이진 탐색** 2가지 방법이 있다.

### DP

- 시간 복잡도 : **O(N^2)**
- 점화식
    - dp[j]
        - if (arr[j] > arr[i] ) : max(dp[j] , dp[i] + 1)
        - else : max(dp[j], dp[i])
    - LIS를 구하는 방법
        - Past 배열을 선언하여 바로 전의 숫자의 idx를 저장한다.
        - maxLen 의 idx로부터 역추적 !
- code

```
        int[] dp = new int[n+1];
        dp[1] = 1; 
        past[1] = 1;

        int maxL = 1;
        for(int i=2;i<=n;i++){
            int max = 1;
            int idx = i;

            for(int j=i-1;j>=1;j--){

                if(board[i] > board[j])
                {
                    if(dp[j]+1 > max){
                        idx = j;
                    }
                    max = Math.max(max , dp[j] + 1);
                }

            }
            past[i] = idx;
            dp[i] = max;
            maxL = Math.max(maxL,dp[i]);
        }
```

### 이진 탐색

- 시간 복잡도 : **O(NlogN)**
- 방법
    - 이진 탐색의 조건 : 정렬되어 있는 배열의 상태
- **주어진 원본 배열이 정렬이 아닌데 … ?**

  생각을 좀 해본다면 결과로 나오는 LIS 배열은 ? : **정렬 상태 !**

- result 배열의 상태는, "증가 수열"의 규칙에 어긋나지 않게, LIS 배열의 상태를
  보면서, "최적의 위치"를 찾으면서 값을 재설정하거나, 값을 삽입해 줄 것이다.
- code

```
static int bs(int left,int right,int target)
{
        int mid = 0;
        while(left <= right)
        {
            mid = (left + right) / 2;

            if(result[mid] < target)
            {
                left = mid + 1;
            }

            else{
                right = mid -1 ;
            }
        }

        return left;
 }

int i = 1;
int j = 0;

result[0] = board[0];

while(i < n)
{
   if(board[i] > result[j]){
      result[j+1] = board[i];
      j = j + 1;
   }

   else{
       int tmp = bs(0,j,board[i]);
       result[tmp] = board[i];
   }
    i = i + 1;
}
// LIS의 길이 : j + 1
```

> **LIS를 이진 탐색으로 구할 때 만드는 result 배열**
>
- 해당 배열은 LIS 배열이 아닐 수 있다 !!!!!
- 최적의 위치를 구하는 것 뿐 만들어진 결과가 LIS임을 보장하지 못한다 !!

[14003번: 가장 긴 증가하는 부분 수열 5](https://www.acmicpc.net/problem/14003)

- 이진 탐색을 통해 LIS를 구하는 방법
    - 앞서와 마찬가지로 index 역추적을 활용해야 한다.

```
while(i < n){
    if(result[j] < num[i]){
        result[j+1] = num[i];
        past[i] = j + 1;
        j = j + 1;
    }
    else{
        int idx = bs(0,j,num[i]);
        result[idx] = num[i];
        past[i] = idx;
	 }
    i = i + 1;
}
```

- 방법
    - 원본 배열의 마지막 원소부터 첫번째 원소까지 꺼꾸로 탐색하면서 해당 위치의 원소를 찾는다.
