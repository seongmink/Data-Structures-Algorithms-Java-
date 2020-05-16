# 병합 정렬(Merge Sort)

## 개념

- 분할 정복 알고리즘의 하나이다.
  - 분할 정복(Divide and conquer)
    - 문제를 작은 2개로 분리하고 각각을 해결한 다음, 결과를 모아서 원래의 문제를 해결하는 전략
    - 분할 정복은 대부분 재귀를 이용하여 구현한다.
- 시간 복잡도 : O(nlogn)

<br>

## 구현

```java
int[] arr = {54, 2, 22, 43, 24, 77, 37, 32, 64, 99 ,53};
mergeSort(arr, 0, arr.length-1)
```

1.

```java
public static void mergeSort(int[] arr, int left, int right) {
		if(left >= right) {
			return;
		}
		
		int mid = (left + right)/2;
		
		mergeSort(arr, left, mid);
		mergeSort(arr, mid+1, right);
		// 왼쪽 정렬, 오른쪽 정렬 된 상태임. 합쳐서 정렬된 상태를 만들어야함
		int[] leftArr = Arrays.copyOfRange(arr, left, mid+1);
		int[] rightArr = Arrays.copyOfRange(arr, mid+1, right+1);
		
		int left_i=0, right_i=0, idx=left;
		
		while(left_i < leftArr.length && right_i < rightArr.length) {
			if(leftArr[left_i] < rightArr[right_i]) { // 두 부분배열 숫자 하나씩 비교, 왼쪽에 숫자가 더 작으면 왼쪽 배열 사용
				arr[idx] = leftArr[left_i]; 
				left_i++;
			} else { // 오른쪽이 더 작으면 오른쪽 배열 쓰기
				arr[idx] = rightArr[right_i];
				right_i++;
			}
			idx++;
		}
		
 	   // 왼쪽 배열에 숫자가 남아있으면 순서대로 넣음(어차피 정렬되어있음)
		while(left_i < leftArr.length) { 
			arr[idx] = leftArr[left_i];
			left_i++;
			idx++;
		}
		
    	// 오른쪽 배열에 숫자가 남아있으면 순서대로 넣음(어차피 정렬되어있음)
		while(right_i < rightArr.length) { 
			arr[idx] = rightArr[right_i];
			right_i++;
			idx++;
		}
}
```

2. 

```
static int[] temp = new int[arr.length]; // 저장할 공간을 만들어 놓아야 함
```

```
int[] arr = {54, 2, 22, 43, 24, 77, 37, 32, 64, 99, 53};
merge_sort(arr, 0, arr.length - 1);
```

```java
public static void merge_sort(int[] arr, int left, int right) {
    int mid;

    if (left < right) {
        mid = (left + right) / 2; // 중간 위치를 계산하여 리스트를 균등 분할 -분할(Divide)
        merge_sort(arr, left, mid); // 앞쪽 부분 리스트 정렬 -정복(Conquer)
        merge_sort(arr, mid + 1, right); // 뒤쪽 부분 리스트 정렬 -정복(Conquer)
        merge(arr, left, mid, right); // 정렬된 2개의 부분 배열을 합병하는 과정 -결합(Combine)
    }
}

public static void merge(int[] arr, int left, int mid, int right) {
    int[] temp = new int[arr.length];
    int i, j, k, l;
    i = left;
    j = mid + 1;
    k = left;

    // 분할 정렬된 arr의 합병
    while (i <= mid && j <= right) {
        if (arr[i] <= arr[j])
            temp[k++] = arr[i++];
        else
            temp[k++] = arr[j++];
    }

    // 남아 있는 값들을 일괄 복사
    if (i > mid) {
        for (l = j; l <= right; l++)
            temp[k++] = arr[l];
    }
    // 남아 있는 값들을 일괄 복사
    else {
        for (l = i; l <= mid; l++)
            temp[k++] = arr[l];
    }

    // 배열 temp 값을 arr로 재 복사
    for (l = left; l <= right; l++) {
        arr[l] = temp[l];
    }
}
```

<br>

## 장점과 단점

- 장점
  - 안정적인 정렬 방법(입력 데이터가 무엇이든 간에 정렬되는 시간은 동일)
  - 연결 리스트(LinkedList)로 구현하면 링크 인덱스만 변경되므로 데이터의 이동은 무시할 수 있을 정도로 작아진다.
  - 따라서 크기가 큰 데이터를 정렬할 경우에 연결 리스트를 사용한다면, 합병 정렬은 퀵 정렬 을 포함한 다른 어떤 정렬 방법보다 효율적이다.
- 단점
  - 만약 데이터들을 배열로 구성하면, 임시 배열이 필요하다.
