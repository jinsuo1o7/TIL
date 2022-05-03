### 최적화 문제들

최적화 문제 : 여러 개의 가능한 답 중 가장 좋은 답을 찾는 문제를 뜻함

최적화 문제를 DP로 푸는것 또한 Brute Force(Recursion) 에서 시작되며,

최적화 문제의 특정 성질이 성립할 경우 메모이제이션을 적용하여 DP를 구현하는 것

```cpp
// 삼각형의 최대 경로를 푸는 DP 알고리즘
int path(vector<vector<int>> tri, vector<vector<int>>& dp, int i, int j){
 if(i >= tri.size() || j > tri[i].size()) return 0;
 if(dp[i][j] != -1) return dp[i][j];
 return max(path(tri, dp, i+1, j), path(tri, dp, i+1, j+1)) + tri[i][j];
}
```

경로를 따라가면서 경로의 합을 다 구할 필요가 없음

**최적 부분 구조 ( optimal substructure )**

→ 지금까지 어떤 경로로 부분 문제에 도달 했건 남은 부분 문제는 최적으로 풀어도 됨

최적 부분 구조는 어떤 문제와 분할 방식에 성립하는 조건

→ 각 부분 문제의 최적해가 있다면 전체 문제의 최적해를 구하는게 가능

삼각형을 내려가는 방식이 2가지이므로 2가지 부분 문제로 나뉘고 현 위치와 상관없이 앞으로 각 부분 문제를 최적으로 해결한다면 전체 문제도 최적으로 해결하는 것과 같음

ex ) 서울에서 부산으로 가는 최단거리 구하기
경로가 (서울-대전) (대전-부산)이 있다면 서울에서 대전으로 가는 최단 거리와 대전에서 부산으로 가는 최단거리의 합과 같음 → 각 부분 문제의 최적해가 전체의 최적해에도 사용됨

### LIS ( 최대 증가 부분수열 )

```cpp
int n;
int dp[101], nums[100];

int lis(int start){
 if(dp[start] != -1) return dp[start];
 dp[start] = 1;
 for(int next = start + 1; next < n; next++){
  if(start == -1 || nums[start] < nums[next])
   dp[start] = max(dp[start], lis(next) + 1);
 }
 return dp[start];
}
```

```cpp
// bottom-up 풀이
for (int i=0; i<n; i++) {
    dp[i] = 1;
    for (int j=0; j<i; j++) {
        if (a[j] < a[i])
            d[i] = max(dp[i], d[j]+1);
    }
}
```

```cpp
// binary search (nlogn)

int binary_search(vector<int> lis, int start, int end, int element) {
    //이분 탐색으로 lis 벡터 내에서 element의 위치를 반환
    //lis 벡터의 start - end 구간에서만 확인
    while (start < end) {
        int mid = (start + end) / 2;
        if (element > lis[mid]) start = mid + 1;
        else end = mid;
    }
    return end;
}
 
int LIS_BS() {
    int ret = 0;
    vector<int> lis;
    lis.push_back(arr[0]);
 
    for (int i = 1; i < n; i++) {
        //만약 lis 벡터의 마지막 수보다 i번째 수가 크다면, 그냥 뒤에 붙인다.
        if (arr[i] > lis.back()) {
            lis.push_back(arr[i]);
            ret = lis.size() - 1;
        }
        //i번째 수에 대해, lis 벡터 내에서 그 수의 위치를 찾는다.
        int pos = binary_search(lis, 0, ret, arr[i]);
        lis[pos] = arr[i];
    }
 
    return ret + 1;
}
```
