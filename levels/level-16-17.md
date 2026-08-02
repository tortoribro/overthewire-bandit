# Bandit Level 16

## 1. 목표
- 현재 레벨인 bandit16의 비밀번호를 localhost의 특정 포트에 제출하여 다음 레벨에
접속할 수 있는 개인키를 얻는다.

## 2. 문제 분석
- 포트 범위 31000부터 32000까지에서 열려있는 포트를 찾아야한다.
- 그중 SSL/TLS를 사용하는 포트를 구분해야한다.
- 여려서비스중 단 하나만 다음 레벨의 인증 정보를 반환한다.
- 나머지 서비스는 입력한 내용을 그대로 돌려주는 echo서비스이다.
- 포트확인후 SSL/TLS접속으로 반환된 개인키를 복사,저장해서 bandit서버 말고 자신의 로컬에서 ssh로 접속해야한다. 즉 자신의 서버에 개인키를 복사하는것이 좋다.
- openssl에 접속시에는 현재 bandit계정의 비밀번호를 입력한다.

## 3. 사용 명령어
- nmap
- openssl


## 4. 명령어 분석
- nmap
```bash
nmap -p 31000-32000 localhost
nmap --open -p 31000-32000 localhost # 열려있는 포트만 확인
nmap -sV -p 31000-32000 localhost # 서비스 버전탐지
```
구성요소|의미
|----|----|
|nmap|	네트워크 포트와 서비스를 탐지하는 도구
|-p	|스캔할 포트 범위를 지정
|31000-32000	|검사할 포트 번호 범위
|localhost|	현재 Bandit 서버 자신
|--open| 열려있는 포트 확인
|-sV| 어떤 서비스인지 확인

- openssl
```bash
openssl s_client -connect localhost:포트번호 -quiet
```

#### 참고
 - 개인키 형식 검증
   - 복사하다보면 의도치않게 개인키의 내용이 누락될 수 있다. 그러므로 개인키인지 검증을 해본다.
```bash
ssh-keygen -y -f 개인키가담긴파일명
```
출력하면 아주 긴 공개키가 출력된다.

- 개인키를이용할때는 자신의 로컬서버에서 bandit서버로 접속해준다. bandit서버에서 localhost로 접속하려면 permission deny가 발생한다.

```bash
ssh -i 비밀키파일명 bandit17@localhost -p 2220
```