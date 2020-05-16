# 퀵 정렬(Quick Sort)

## 개념

- 분할 정복 알고리즘의 하나이다.
  - 분할 정복(Divide and conquer)
    - 문제를 작은 2개로 분리하고 각각을 해결한 다음, 결과를 모아서 원래의 문제를 해결하는 전략
    - 분할 정복은 대부분 재귀를 이용하여 구현한다.
- 하나의 리스트를 피벗(pivot)을 기준으로 두 개의 비균등한 크기로 분할하고 분할된 부분 리스트를 정렬한 다음, 두 개의 정렬된 부분 리스트를 합하여 전체가 정렬된 리스트가 되게 하는 방법이다.
- 평균적으로 **매우 빠른 수행 속도**
- 시간 복잡도 
  - 최선 : O(nlogn)
  - 평균 : O(nlogn)
  - 최악 : O(n^2)

<br>

## 구현

```java
int[] arr = { 54, 2, 22, 43, 24, 77, 37, 32, 64, 99, 53 };
quickSort(arr, 0, arr.length - 1);
```

```java
public static int partition(int[] arr, int left, int right) {
    int pivot = arr[(left + right) / 2];

    while (left < right) {
        while (arr[left] < pivot && left < right)
            left++;
        while (arr[right] > pivot && left < right)
            right--;

        if (left < right) {
            int tmp = arr[left];
            arr[left] = arr[right];
            arr[right] = tmp;
        }
    }
    return left;
}

public static void quickSort(int[] arr, int left, int right) {
    if (left < right) {
        int mid = partition(arr, left, right);

        quickSort(arr, left, mid - 1);
        quickSort(arr, mid + 1, right);
    }
}
```

<br>

## 장점과 단점

- 장점
  - 속도가 빠르다.(시간 복잡도가 O(nlogn)을 가지는 다른 정렬 알고리즘과 비교했을 때도 빠름)
  - 추가 메모리 공간을 필요하지 않음(병합 정렬에서 임시 배열 등등 .. )
    - O(logn)만큼의 메모리 필요
- 단점
  - 정렬된 리스트에 대해서는 퀵 정렬의 불균형 분할에 의해 오히려 수행시간이 더 많이 걸린다.
