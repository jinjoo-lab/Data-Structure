# 이진 탐색

## Binary Search

### 이진 탐색

- 정렬된 데이터들에 대한 탐색의 효율이 좋은(속도가 빠른) 알고리즘
    - 배열의 중앙에 있는 값을 기준 → 탐색 대상이 왼쪽 or 오른쪽 배열에 있는지 탐색
        - 이 과정에서 검색 범위를 지속적으로 **절반**으로 줄일 수 있다.
    - 데이터의 삽입 or 삭제가 빈번한 경우 적합하지 않다. → 탐색에 특화된 알고리즘

### 정리

| 시간복잡도 | O(logN) |
| --- | --- |
| 가정 | 데이터가 정렬되어 있어야 한다. |
| 방식 | mid(중앙값)을 활용해 매 연산마다 탐색 범위를 절반으로 줄임 |

## Upper Bound , Lower Bound

- 이진 탐색을 기반하여 **경계값**을 찾는 알고리즘 (데이터 중복일때 효과적 동작)
    - 시간 복잡도 : **O(logN)**
- 이진 탐색 시 데이터내 특정 값을 찾을 때 → 값의 중복이 있는 경우
    - Lower Bound : 특정 K 값보다 **같거나 큰 값의 처음 나오는 위치**
    - Upper Bound : 특정 K 값보다 **큰 값의 처음 위치**

### Lower Bound

- 특정 **K값의 시작 위치**

![Untitled](https://user-images.githubusercontent.com/84346055/270638074-d531c14d-ec28-4e64-be9a-fbc829a71d8f.png)

**동작 방식**

1. 배열의 중간 값(mid)를 찾는다.
2. 중간 값하고의 비교
    1. 검색 값(target)보다 **작으면** left = mid + 1
    2. 검색 값(target)보다 **크거나 같으면** right = mid
3. 1,2 의 과정을 **left < right** 일 때까지 반복
4. 반복이 종료된 경우 : **right** 값이 lower bound

```
while(left < right){
		int mid = (left + right) / 2;

		if(data[mid] < target)
			left = mid + 1;

		else
			right = mid;
}

return data[right]
```

### Upper Bound

- 특정 **K값보다 큰값의 처음 위치**

![Untitled](https://user-images.githubusercontent.com/84346055/270638086-83475e0b-77eb-49c1-9725-f1f3feb0839d.png)

**동작 방식**

1. 배열의 중간값(mid)를 찾는다.
2. 중간값하고의 비교
    1. 검색 값(target)보다 **작거나 같으면** **left = mid +1**
    2. 검색 값(target)보다 **크면** **right = mid**
3. 1, 2의 과정을 left < right 인 동안 반복
4. 반복이 종료된 경우 : **right** 값이 upper bound

```
while(left < right){
		int mid = (left + right) / 2;

		if(data[mid] <= target)
			left = mid + 1;

		else
			right = mid;
}

return data[right]
```

### 예제

[3079번: 입국심사](https://www.acmicpc.net/problem/3079)
