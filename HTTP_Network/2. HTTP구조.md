## HTTP Request, Response

```tsx
클라이언트 Request
GET /index.html HTTP /1.1
Host: www.hackr.jp
```

- GET : HTTP 메소드
- /index.html : 요구하는 리소스
- HTTP/1.1 : 클라이언트 HTTP 버전 정보

```tsx
서버 Response
HTTP /1.1 200 OK
Date: Tue, 10 Jul 2022 06:50:15 GMT // 리스폰스 발생 일시
Content-Length : 362
Content-Type : text/html

<html>
```

- HTTP /1.1 : 서버 HTTP 버전
- 200 OK : 처리 결과
- <html> 한줄 공백 이후에 body필드로 리소스 본체

---

### HTTP는 stateless 프로토콜

HTTP는 데이터를 Request와 Response를 교환하는 동안에 Status를 관리하지 않음

---

### HTTP 메소드

- GET : 리소스 요청
- POST : 엔티티 전송
- HEAD : 메시지 헤더 취득 → body를 돌려주지 않고 URI 유효성과 리소스 갱신 시간을 확인 하는 목적
- PUT :  파일 전송 - 누구든 전송 가능해서 보안상 문제로 사용하지 않음
- DELETE : 파일 삭제 - 누구든 삭제 가능해서 사용하지 않음
- OPTIONS : URI로 지정한 리소스가 제공하는 메소드들을 알려줌
- TRACE : 경로 조사
- CONNECT : 프록시에 터널 접속을 요청하여 TCP 통신 터널링

---

### 지속 연결

초기에 HTTP 통신은 한번 Request가 일어날때 마다 TCP에 연결과 종료를 거쳐야 했음

지속연결을 도입하여 한곳에서 종료하지 않는 이상 TCP연결을 계속 유지하게 함

### 파이프라인

지속 연결을 통하여 여러 Request를 보낼 수 있도록 파이프라인이 가능해짐

Request 송신 후에 Response를 기다린 뒤에야 다시 Request를 해야했지만 파이프 라인은 Response를 기다리지 않고 여러  Request를 보내는게 가능

### 쿠키와 상태 관리

인증이 필요한 웹 페이지에서 상태 관리를 하지 않는다면 새로운 페이지마다 다시 로그인을 해야함

1. 쿠키는 서버에서 Response를 보낼때 Set-Cookie 헤더필드를 붙여서 클라이언트에게 줌
2. 클라이언트는 Request를 보낼때 자동으로 Cookie를 넣어서 송신
3. 서버는 쿠키를 확인하여 클라이언트의 상태를 확인

```tsx
Request 쿠키를 가지고 있지 않은 상태
GET /header/ HTTP /1.1
Host: www.hackr.jp
```

```tsx
Response 쿠키 발행
HTTP /1.1 200 OK
Date: Tue, 12 Jul 2022 08:12:20 GMT
Server: Apache
**<Set-Cookie: sid=1247128638712: path=/:expires=Wed, => 10-Oct- 12 08:12:20 GMT>**
Content-Type: text/plain: charset=UTF-8
```

```tsx
Request 쿠키 자동 송신
GET /header/ HTTP /1.1
Host: www.hackr.jp
**Cookie: sid=1247128638712**
```
