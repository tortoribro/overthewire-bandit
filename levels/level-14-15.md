# Bandit Level 14

## 1. 목표
- localhost 30000번포트에 접속하여 비밀번호를 획득해야한다.

## 2. 문제 분석
- localhost 30000번 포트에 접속한다.
- 접속시 현재 비밀번호 필요

## 3. 사용 명령어
- nc
- cat


## 4. 명령어 분석
- nc(Netcat)
    - Netcat의 약자
    - Netcat은 명령줄에서 네트워크를 연결을 생성하고 데이터를 읽거나 쓰는데 사용하는 도구
```bash
 nc localhost 30000 #localhost 30000에 접속
```

파이프를 사용하여 비밀번호까지 한꺼번에 입력
```bash
cat /etc/bandit_pass/bandit14 | nc localhost 30000
```

