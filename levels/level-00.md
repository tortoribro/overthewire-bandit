# Bandit Level 0

## 1. 목표
- Bandit 서버에 SSH로 접속

## 2. 문제 분석

- ssh 아이디와 비밀번호로 bandit ssh 서버에 원격접속을 한다.

## 3. 사용 명령어

- 접속
```bash
ssh bandit0@bandit.labs.overthewire.org -p 2220
```

| 부분                            | 의미                   |
| ----------------------------- | -------------------- |
| `ssh`                         | 원격 서버에 안전하게 접속       |
| `bandit0`                     | 사용자 계정               |
| `@`                           | 계정과 서버 주소 구분         |
| `bandit.labs.overthewire.org` | 서버 주소                |
| `-p 2220`                     | SSH 포트 번호를 2220으로 지정 |



- 종료
```bash
exit
```