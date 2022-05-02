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

<br/>

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

<br/>

### 메모이제이션의 시간복잡도는 ?

`존재하는 부분 문제의 수` * `한 부분 문제를 풀때 필요한 반복문의 수행 횟수`

bino2(n,r) 함수에서 모든 부분문제의 개수는 O(n^2)개이고 부분 문제에 반복문이 없으므로 O(1)

따라서 O(n^2) 만큼 걸림

단, 위의 식은 간단히 계산하기 위함일뿐, 항상 정확성을 보장하지 않음

<br/>

### Dynamic Programming

번역하면 동적 프로그래밍이지만 사실 동적 계획법이라고 보는게 적절한 번역이다.

DP 또한 분할정복처럼 접근한다. 큰 문제를 작게 나누고 계산하는 접근법

차이점은 문제를 나누는 방식 !

DP의 특징은 어떤 문제의 답을 여러번 계산하는 것이 아닌 **한번만 계산하고 그 값을 계속 재활용하는 것**

이미 저장한 값을 저장하기 위해 `cache` 에 저장

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

<br/>

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

<br/>

### 메모이제이션의 시간복잡도는 ?

`존재하는 부분 문제의 수` * `한 부분 문제를 풀때 필요한 반복문의 수행 횟수`

bino2(n,r) 함수에서 모든 부분문제의 개수는 O(n^2)개이고 부분 문제에 반복문이 없으므로 O(1)

따라서 O(n^2) 만큼 걸림

단, 위의 식은 간단히 계산하기 위함일뿐, 항상 정확성을 보장하지 않음

<br/>

### 와일드카드 문제

```cpp
Brute Force

bool match(const string& w, const string& s){
 int pos = 0;
 // 문자열 대응하기 서로 같거나 와일드카드문자가 ? 일경우 pos++
 while(pos < s.size() && pos < w.size() && (w[pos] == '?' || w[pos]==s[pos]){
  pos++;
 }
 // 대응할것이 끝나고 while문이 벗어난 이유 처리하기
 // 1.pos가 와일드카드문, 비교할 문자열 끝에까지 도달한 경우 정답
 if(pos==w.size()) return pos == s.size();

 // 2. *을 만난경우 *에 몇글자를 대응해야할지 재귀호출
 if(w[pos] == '*'){
  for(int skip = 0; pos+skip <= s.size(); ++skip){
   if(match(w.substr(pos+1), s.substr(pos+skip)) return true;
  }
 }
 return false;
}
```

*에 대응하는 모든 문자를 검사해야하므로 시간 복잡도가 오래 걸림

예) 만일 와일드카드가 ********a 문자열이 aaaaaaab인경우*하나마다 수많은 a들을 대응시킴

<br/>

### 메모이제이션 적용하기

w, s의 종류는 제한되어 있다는 점을 이용하기 → 재귀 호출시에 w s 앞 글자들을 때어서 비교하기 때문에  w, s는 항상 W와 S의 부분 문자열임

문자열의 길이 제한이 100이므로 w,s 는 최대 101개다.

→ w는 W의 부분 문자열이기 때문에 w의 길이가 정해지면 w도 정해짐 ( 101 * 101 배열에 모든 부분 문제를 저장 가능 )

```cpp
// -1은 초기 계산되지 않은 값
// 1은 서로 대응됨
// 0은 서로 대응하지 않음 
vector<vector<int>> dp(101, vector<int>(101, -1));
string W, S;

// 와일드카드 W[w..]가 S[s..]에 대응하는지 보기
bool matchMemoized(int w, int s){
 // 메모이제이션
 if(dp[w][s] != -1) return dp[w][s];

 // W[w] S[s]를 맞춰나가기
 while(s < S.size() && w < W.size() && (W[w] == '?' || W[w] == s[s])){
  w++, s++;
 }
 
 // while문 끝난 이유 처리하기
 if(w == W.size()) return dp[w][s] = (s==S.size());
 
 if(W[w] == '*'){
  for(int skip = 0; skip + s <= S.size(); skip++)
   if(matchMemoized(w+1, s+skip)) return dp[w][s] = 1;
 }

 return dp[w][s] = 0;
}
```

시간복잡도 : 문자열의 길이 n 이므로 부분 문제의 개수 n^2, matchMemoized() 호출마다 n번의 재귀호출을 해야함  총 O(n^3)

<br/>

### 좀 더 효율적인 방식 O(n^2)

```cpp
// O(n^3)에서의 W[w] S[s]를 맞춰나가는 방식
 while(s < S.size() && w < W.size() && (W[w] == '?' || W[w] == s[s])){
  w++, s++;
 }
```

```cpp
// W[w] S[s]를 비교해서 pos를 늘리는 방식대신 
// 와일드카드와 문자열을 한글자씩 떼서 재귀로 확인하는게 가능
if(w< W.size() && s < S.size() && (W[w] == '?' || W[w] == S[s]))
 return dp[w][s] = matchMemoized(w+1, s+1);
```

```cpp
// *를 만나는 경우 몇 글자에 대응할지 말지 재귀로 돌림
if(W[w] =='*'){
 // matchMemoized(w+1, s) 대응하는 경우 matchMemoized(w, s+1) 대응하지 않는 경우
 if(matchMemoized(w+1, s) || (s<S.size() && matchMemoized(w, s+1)))
  return dp[w][s] = 1;
}
```
