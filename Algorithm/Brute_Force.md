**완전탐색 레시피**

1. 완전 탐색은 존재하는 모든 답을 하나씩 검사해야 하므로 걸리는 시간은 답의 수에 비례

    ( 최대 크기의 입력을 가정했을 때 답의 개수를 계산하고 이들을 모두 제한 시간안에 생성이 가능한지를 가늠하기 )

2. 가능한 모든 답의 후보를 만드는 과정을 여러 개의 선택으로 나누기, 각 선택은 답의 후보를 만드는 과정의 한 조각이 됨
3. 그중 하나의 조각을 선택해 답의 일부를 만들고, 나머지 답을 재귀 호출을 통해 완성하기
4. 조각이 하나밖에 남지 않는 경우, 혹은 하나도 남지 않을 경우에는 기저 사례(base case)로 선택해 처리

**재귀 호출과 부분 문제**

하나의 문제와 부분 문제의 정의가 가장 중요함


**재귀 함수 ( recursion )**

1부터 n까지의 합을 구하는 함수

n개의 숫자의 합을 구하는 것은 n개의 "조각"으로 쪼개서 더 할 각 숫자가 하나의 조각이 되도록 하자

- 재귀 호출을 하기 위해서 조각 중 하나를 자기가 해결하고 나머지 조각은 자기를 호출해야 함
- n개의 조각 중 n을 처음에 빼낸게 아니라 1을 뺏을 경우 이런 방식으로 문제를 해결 못함

1을 처음에 빼면 2부터 n까지의 합이 남는데 원래 문제와 다른 형태이고 제귀 호출을 못하게 됨

1. n만 이 조각들에서 따로 빼냄 그러면 1 부터 n-1까지 조각이 남음
2. 자기자신을 호출해서 n-1까지의 합을 구하고 n을 더함

    ```cpp
    int recursiveSum(int n) {
      if (n == 1)
        return 1;
      return n + solution(n - 1);
    }
    ```

- if문이 없으면 1일경우 조각이 하나이고 더 이상 처리할 작업이 없기 때문에 기저 사례(base case)로 함

base case : 더 이상 쪼개지지 않는 최소 작업에 도달할때 답을 바로 반환하도록 하는 조건문

### 중첩된 반복문 대체하기

0부터 7까지 원소중 4개의 원소를 골라 출력하는 모든경우를 4중 for문으로 구현

```cpp
for (int i = 0; i <= 7; i++)
    for (int j = i + 1; j <= 7; j++)
      for (int k = j + 1; k <= 7; k++)
        for (int l = k + 1; l <= 7; l++)
          cout << i << ' ' << j << ' ' << k << ' ' << l << '\n';
```

- 5개를 골라야하는 경우 5중 for문 ... 코드가 너무 길고 복잡함

문제를 조각으로 나누고 각 조각에서 하나의 원소를 고르고 남은 원소들을 고르는 작업을 자신을 호출해서 재귀함수로 바꿔 보자

이때 남은 원소들을 고른는 '작업'을 다음과 같은 입력의 집합으로 정의하자

1. 원소들의 총 개수
2. 더 골라야할 원소들의 개수
3. 지금까지 고른 원소들의 번호

```cpp
void solution(int n, vector<int> &picked, int toPick) {
  // base case 더 이상 고를 원소가 없으므로 모두 출력
  if (toPick == 0) {
    printPicked(picked);
    return;
  }

  //고를 수 있는 가장 작은 번호를 계산
  int smallest = picked.empty() ? 0 : picked.back() + 1

  //이 단계에서 원소 하나를 고른다
  for (int next = smallest; next < n; ++next) {
    picked.push_back(next);
    solution(n, picked, toPick - 1);
    picked.pop_back();
  }
}
```
