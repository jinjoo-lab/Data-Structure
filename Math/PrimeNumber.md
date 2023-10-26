# 소수 판별

### 소수 (Prime Number)

- 1보다 큰 자연수 중에서 **1과 자기 자신을 제외한 자연수로는 떨어지지 않는 자연수**

### 단일 소수 판별

1. **기본적인 방식**
    - X가 주어졌을 때 2부터 X-1까지의 모든 자연수로 나누었을 때 약수가 있는지 판단.
    - 시간 복잡도 : O(N)

```
static boolean isPrime(int num){
	for(int i=2;i<=num-1;i++){
		if(num % i == 0)
			return false;
	}

	return true;
}
```

1. **제곱근까지만 탐색**
- 시간 복잡도 : O(sqrt(N))
- 16의 약수를 우리는 다음과 같이 표현할 수 있다.

```
16의 약수 : 1,2,4,8,16
(1,16)
(2,8)
(4,4)
(8,2)
(16,1)
```

- 가운데 약수인 4를 표현하는 방식 이후에는 **이전에 나왔던 약수의 순서만 바뀐것**을 알 수 있다 !
    - 다시 말해 가운데 약수(제곱근) 까지만 탐색을 해도 답을 구할 수 있다는 것이다.

```
static boolean isPrime(int num){
	for(int i=2;i<=Math.sqrt(num) + 1;i++){
		if(num % i == 0)
			return false;
	}

	return true;
}
```

### 다중 소수 판별 : 에라토스테네스의 체

- 시간복잡도 : O(NloglogN) (선형 시간 탐색 가능)
- 위의 방식은 각 수에 대해 소수 판단을 하는 것이다.
- 그렇다면 **여러 개의 소수를 한번에 판단**할 수는 없을까?

> 에라토스테네스의 체는 일**정 범위(N)을 기준으로 N보다 작거나 같은 모든 소수를 찾을 때 사용**
>

**과정**

1. 2부터 N까지의 모든 자연수에 대한 리스트 or 배열 생성
2. 가장 작은 수(i)부터 과정을 수행
    1. i를 제외한 **i의 배수를 모두 제거**(소수가 아니다)
3. 2의 과정을 반복할 수 없을 때까지 수행
    1. **제곱근탐색 방식**을 사용

```
static void isPrime(int num){
	boolean[] notPrime = new boolean[num+1];
	
	for(int i=2;i<=Math.sqrt(num)+1;i++){
			if(!notPrime[i]){
				int j= 2;

				 while(i * j <= num){
						notPrime[i*j] = true;
						j = j + 1;
					}
			}
	}
}
```

- **왜 i는 제거 X**
    - 2,3은 배수의 시작이면서 동시에 소수이기 때문이다.
- **동작 과정**

  ![Untitled](https://user-images.githubusercontent.com/84346055/278248903-90b4eb2d-7056-4317-b29f-dfb48b91219d.png)

  ![Untitled](https://user-images.githubusercontent.com/84346055/278248934-a0eec968-f837-4d2c-8eda-63b39f7f8d3c.png)

  ![Untitled](https://user-images.githubusercontent.com/84346055/278248943-5eaa235f-7b0f-4e43-b49f-7ccca1a0feb3.png)

  ![Untitled](https://user-images.githubusercontent.com/84346055/278248948-fbc5927c-6f66-4f84-8cff-6e364ee50cc5.png)


### Ex)

[17425번: 약수의 합](https://www.acmicpc.net/problem/17425)

**문제**

- 두 자연수 A와 B가 있을 때, A = BC를 만족하는 자연수 C를 A의 약수라고 한다. 예를 들어, 2의 약수는 1, 2가 있고, 24의 약수는 1, 2, 3, 4, 6, 8, 12, 24가 있다.
- 자연수 A의 약수의 합은 A의 모든 약수를 더한 값이고, f(A)로 표현한다. x보다 작거나 같은 모든 자연수 y의 f(y)값을 더한 값은 g(x)로 표현한다.
- 자연수 N이 주어졌을 때, g(N)을 구해보자.

**접근**

> 약수를 계산할 때 에라토스테네스의 체를 활용해야 한다.
>

**코드**

```java
import java.io.*;
import java.util.*;

public class Main {
    static int t = 0;

    public static void main(String[] args) throws IOException {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        StringTokenizer st = new StringTokenizer(br.readLine(), " ");
        t = Integer.parseInt(st.nextToken());

        long[] sum = new long[1000001];

        for (int i = 1; i <= 1000000; i++) {

            int j = 1;

            while (i * j <= 1000000) {
                sum[i * j] += i;
                j = j + 1;
            }

            sum[i] += sum[i-1];
        }

        StringBuilder sb = new StringBuilder();
        for (int i = 1; i <= t; i++) {
            int tmp = Integer.parseInt(br.readLine());

            sb.append(sum[tmp] + "\n");
        }
        System.out.print(sb);

        br.close();
    }

}
```
