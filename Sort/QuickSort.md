# Quick Sort

### **Quick Sort**

- 분할 정복(Divide And Conquer) 알고리즘
- 평균적으로 매우 빠른 시간 복잡도를 가진다.

### 정렬 과정

1. 데이터들 중에서 한 요소를 선택한다. → **pivot**
2. pivot을 기준
    - 더 작은 값들 → **pivot의 왼쪽**으로 이동
    - 더 큰 값 → **pivot의 오른쪽** 이동
3. 모든 값들이 정렬될 때까지 1, 2 과정을 반복 → **재귀**

### 코드

```java
import java.io.*;

public class Main {

    public static void main(String[] args) throws IOException {
        int[] arr= {7,4,2,8,3,5,1,6,10,9};
        QuickSort(arr,0,arr.length-1);
        
        for(int i=0;i<arr.length;i++) {
            System.out.print(arr[i]+",");
        }
        
    }

    static void QuickSort(int arr[] , int l , int r){
        int part = partition(arr,l,r);
        if(l < part -1)
            QuickSort(arr,l,part -1);

        if(r > part)
            QuickSort(arr,part,r);
    }

    static int partition(int[] arr,int l,int r){
        int pivot = arr[(l+r)/2];

        while(l <= r){
            while(arr[l] < pivot)
                l++;

            while(arr[r] > pivot)
                r--;

            if(l <= r){
                swap(arr,l,r);
                l++;
                r--;
            }
        }

        return l;
    }

    private static void swap(int[] arr,int l,int r) {
        int tmp=arr[l];
        arr[l]=arr[r];
        arr[r]=tmp;
    }

}
```

## 시간복잡도

- 피벗 값이 최소나 최댓값으로 지정되어 파티션이 나누어지지 않는 경우 → O(N^2)
    - 즉 이미 정렬이 되어있는 상태라면 최악의 시간복잡도를 가진다.
- 평균적인 상황 → O(NlogN)

### 평균의 경우

- 비교 횟수 : logN

![Alt text](https://user-images.githubusercontent.com/84346055/261543866-a9cd39d5-821a-4aab-8324-1e9393f778f1.png)

### 최악의 경우

- 비교 횟수 : N

![Alt text](https://user-images.githubusercontent.com/84346055/261543887-820efa57-2d13-4a66-8c6a-c55ffab5f1d6.png)

### 장점

- 불필요한 데이터의 이동을 줄이고 먼 거리의 데이터를 교환할 뿐만 아니라, 한 번 결정된 피벗들이 추후 연산에서 제외되는 특성 때문에, 시간 복잡도가 O(nlog₂n)를 가지는 다른 정렬 알고리즘과 비교했을 때도 가장 빠르다.
- 정렬하고자 하는 배열 안에서 교환하는 방식이므로, 다른 메모리 공간을 필요로 하지 않는다.

### 단점

- **불안전 정렬(Unstable Sort)**이다.
    - 중복된 값이 입력 순서와 동일하지 않게 정렬되는 알고리즘 !
- 최악의 경우 시간 복잡도가 O(N^2)이다.

### Java

- 자바의 Arrays.sort()는 내부적으로 QuickSort를 구현하고 있다

```
public static void sort(int[] a) {
        DualPivotQuicksort.sort(a, 0, 0, a.length);
    }
```

- Arrays.sort
    - Insertion Sort + Quick Sort

### [참고]
https://gwang920.github.io/algorithm%20non%20ps/qucikSort/
