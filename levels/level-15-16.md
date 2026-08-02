# Bandit Level 15

## 1. 목표
- SSL/TLS연결을 하여 비밀번호를 알아낸다.


## 2. 문제 분석
- bandit14에서는 nc를 이용해 단순히 평문으로 데이터를 전송하였지만 bandit15는 SSL/TLS 즉, 암호화된 네트워크 통신을 요구한다.
- 암호화된 형태로 localhost:30001에 전송하면 서버가 다음레벨의 비밀번호를 반환한다.


## 3. 사용 명령어
- openssl 

## 4. 명령어 분석
- openssl

```bash
openssl s_client -connect localhost:30001 -quiet
```
구성요소|의미
|----|----|
|openssl|	암호화와 인증서, TLS 기능을 제공하는 도구
|s_client|	SSL/TLS 클라이언트로 동작
|-connect|	접속할 호스트와 포트를 지정
|localhost:30001|	현재 서버의 30001번 포트
|-quiet|	인증서와 세션 등의 부가 출력을 줄이고 데이터 통신 결과에 집중

파이프를 이용해 접속
```bash
cat /etc/bandit_pass/bandit15 | openssl s_client -connect localhost:30001 -quiet
```

#### 참고
- TLS Handshake
  - TLS 연결을 시작하면 클라이언트와 서버는 암호화 통신을 위한 협상 과정을 수행한다.
 ```
 클라이언트 연결 요청
→ 서버 인증서 전달
→ TLS 버전 및 암호화 방식 협상
→ 세션 키 생성
→ 암호화 통신 시작
→ 비밀번호 전송
→ 서버 응답
 ```