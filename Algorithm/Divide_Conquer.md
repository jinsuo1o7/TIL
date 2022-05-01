**Divide & Conquer**

재귀 호출은 문제를 한조각과 나머지 전체로 나누는 반면

분할 정복은 큰 문제를 같은 크기로 계속 나눔

분할 정복은 같은 작업을 더 빠르게 처리해주는 장점을 가지고 있음

**분할 정복의 세가지 구성 요소**

- Divide 문제를 더 작게 분할하는 과정
- Merge 각 문제에 대해 구한 답을 원래 문제에 대한 답으로 병합하는 과정
- Base case 더 이상 답을 분할하지 않고 바로 풀 수 있는 최소 단위의 문제

분할 정복으로 문제를 해결하기 위해서는 문제의 특성이 성립해야 함

1. 문제를 둘 이상으로 자연스럽게 나누는게 가능한가?
2. 부분 문제의 답을 조합해 원래 문제의 답을 계산할 수 있는가?

```cpp
1+2+3+... +n 까지 계산하는 재귀
int recursiveSum(int n){
 if(n==1) return 1;
 return n + recursiveSum(n-1);
}

분할정복을 적용하기
n이 짝수로 가정하고 문제를 반으로 나눠서 빠르게 구하는게 가능
fastSum(n) = 2*fastSum(n/2) + (n/2)^2

int fastSum(int n){
 if(n==1) return 1;
 // n이 홀수일 경우 n-1(짝수) 까지의 합을 구하고 n만 따로 더하면 됨
 if(n%2==1) return fastSum(n-1) + n;
 return 2*fastSum(n/2) + (n/2)*(n/2);
}
```

recursiveSum은 함수 호출이 n번 필요하지만 fastSum()은 호출마다 n이 절반으로 줄들기 때문에 훨씬 적음

### Merge Sort & Quick Sort

Merge sort : 주어진 수열을 가운데에서 쪼개 비슷한 크기의 수열로 나누고 재귀호출을 통해 정렬

```cpp
#include <iostream>
using namespace std;

void merge(int *arr, int low, int high, int mid)
{
    int i, j, k, c[50];
    i = low;
    k = low;
    j = mid + 1;
    while (i <= mid && j <= high) {
        if (arr[i] < arr[j]) {
            c[k] = arr[i];
            k++;
            i++;
        }
        else  {
            c[k] = arr[j];
            k++;
            j++;
        }
    }
    while (i <= mid) {
        c[k] = arr[i];
        k++;
        i++;
    }
    while (j <= high) {
        c[k] = arr[j];
        k++;
        j++;
    }
    for (i = low; i < k; i++)  {
        arr[i] = c[i];
    }
}

void merge_sort(int *arr, int low, int high)
{
    int mid;
    if (low < high){
        //divide the array at mid and sort independently using merge sort
        mid=(low+high)/2;
        merge_sort(arr,low,mid);
        merge_sort(arr,mid+1,high);
        //merge or conquer sorted arrays
        merge(arr,low,high,mid);
    }
}
```

quick sort

```cpp
int partition(int arr[], int low, int high) {
  int pivot = arr[high]; // pivot
  int i = (low - 1);// 더 작은 요소의 인덱스이며 지금까지 찾은 피벗의 올바른 위치를 나타냅니다.

  for (int j = low; j <= high - 1; j++) {
    if (arr[j] <= pivot) {
      swap(&arr[++i], &arr[j]);
    }
  }
 // i < pivot < i+2 이므로 i+1위치가 피봇 위치 (정렬된 위치임)
  swap(&arr[i + 1], &arr[high]);
  return (i + 1); // 피봇 인덱스 반환
}

void quickSort(int arr[], int low, int high) {
  if (low < high) {
    /* pi is partitioning index, arr[p] is now
       at right place */
    int pi = partition(arr, low, high);

    // Separately sort elements before
    // partition and after partition
    quickSort(arr, low, pi - 1);
    quickSort(arr, pi + 1, high);
  }
}
```
