# 선택 정렬(Selection Sort)

## 개념

- 해당 순서에 넣을 위치는 이미 정해져 있고, 어떤 값을 넣을지 선택하는 알고리즘
- 첫 번째 원소를 두 번째 값부터 마지막 값까지 차례대로 비교하여 가장 작은 값을 찾아 첫 번째로 넣고, 두 번째 원소를 세 번째 값부터 마지막 값까지 차례대로 비교하여 그 중 가장 작은 값을 찾아 두 번째 위치에 넣는 과정을 반복
- 시간 복잡도 : O(n^2)

<br>

## 구현

```java
int[] arr = {54, 2, 22, 43, 24, 77, 37, 32, 64, 99, 53};
selectionSort(arr);
```

```java
public static void selectionSort(int[] arr) {
    for(int i = 0; i < arr.length; i++) {
        int min = i;
        for(int j = i+1; j < arr.length; j++) {
            if(arr[j] < arr[min]) {
                min = j;
            }
        }
        swap(arr, min, i);
    }
}

public static void swap(int[] arr, int i, int j) {
    int temp = arr[i];
    arr[i] = arr[j];
    arr[j] = temp;
}
```

<br>

## 장점과 단점

- 장점
  - 구현하기 쉬움.
  - 자료 이동 횟수가 미리 결정된다.
- 단점
  - 안정성을 만족하지 않음(값이 같은 원소가 있는 경우에 상대적인 위치가 변경될 수 있다.)

