# GCD + LCM

## 최대공약수(GCD)

- Greatest Common Divisor

> 두 자연수의 공통된 약수 중 가장 큰 수
>

### Brute Force : O(N)

- 가장 단순한 방법 , **범위 부터 1까지** 나눠 보면서 진행
    - 역순 진행을 통해 더 빠르게 찾을 수 있다. 하지만 크게 상관은 없다
- 시간 복잡도 : O(N)
- **범위**

  두 수중 작은 수까지 진행해본다. 두 수중 한 수가 최대 공약수일 수 있다 !


```
static void find(int min,int max){
	for(int i = min; i>0;i --){
		if(max % i == 0 && min % i == 0){
			// find !
			break;
		}
	}
}
```

### 유클리드 호제법

- 시간 복잡도 : O(log N)
- 2개의 자연수를 x, y 라 하자 (x를 y로 나눈 나머지 : r)

> **x와 y의 최대 공약수 = y와 r의 최대 공약수**
>
- 위 특징을 재귀적으로 접근하여 나머지가 0이 되는 순간 y의 값이 최대 공약수이다.

![Untitled](GCD%20+%20LCM%20b10b8743aa604001b3efb77f0aaa9fbb/Untitled.png)

### 반복문

```
while(x % y !=0){
     r = x % y;
     x = y;
     y = r;
}
```

### 재귀

```
static int find(int x,int y){
    if(y == 0) return x;

     return find(y, x % y);
}
```

## 최소공배수(LCM)

- 두 자연수의 공통된 배수 중 가장 작은 수

> 최소 공배수 = (두 자연수의 곱) / 최대 공약수
>
