### Dynamic Programming

번역하면 동적 프로그래밍이지만 사실 동적 계획법이라고 보는게 적절한 번역이다.

DP 또한 큰 문제를 작게 나누고 계산하는 접근법인 분할정복처럼 접근한다.

**차이점은 문제를 나누는 방식 !!**

DP의 특징은 어떤 문제의 답을 여러번 계산하는 것이 아닌 **한번만 계산하고 그 값을 계속 재활용하는 것**

이미 저장한 값을 저장하기 위해 `cache` 에 저장해서 재활용한다.

```cpp
재귀함수를 통해 이항계수 구현
메모이제이션을 하지 않으므로 중복 계산이 있음
int bino(int n, int r){
 if(r==0 || r==n) return 1;
 return bino(n-1, r-1) + bino(n-1, r)
}

메모이제이션을 활용하기
메모이제이션을 사용하면 중복된 계산을 하지 않음
vector<vector<int>> dp(30, vector<int>(30, -1));
int bino2(int n, int r){
 if(r==0 || r==n) return 1;
 if(dp[r][n] != -1) return dp[r][n];
 return dp[r][n] = bino(n-1, r-1) + bino(n-1, r);
}
```

메모이제이션을 사용하려면 참조적 투명성(referential transparency)를 만족해야 함

referential transparency : 함수의 입력값이 같을때 같은 결과를 반환해주는 함수

### 메모이제이션 구현 패턴

1. 항상 base case를 먼저 처리하자. cache 체크보다 먼저 해줘야 범위 오류가 안나옴
2. 초기 dp[] 를 모두 -1로 초기화 해주자 ( 만일 함수의 반환값이 -1도 있을경우 다르게 설정해주기 )

```cpp
vector<vector<int>> dp(25000, vector<int>(25000,-1)); // 초기에는 모두 -1로 초기화 해주기
int someObscuerFunction(int a, int b){
 if(...) return ...;  // 먼저 basecase부터 처리하기
 if(dp[a][b] != -1) return dp[a][b]; // 그리고 cache체크하기
 return dp[a][b] = ...; // 답을 계산하기
}
```

### 메모이제이션의 시간복잡도는 ?

`존재하는 부분 문제의 수` * `한 부분 문제를 풀때 필요한 반복문의 수행 횟수`

bino2(n,r) 함수에서 모든 부분문제의 개수는 O(n^2)개이고 부분 문제에 반복문이 없으므로 O(1)

따라서 O(n^2) 만큼 걸림

단, 위의 식은 간단히 계산하기 위함일뿐, 항상 정확성을 보장하지 않음
