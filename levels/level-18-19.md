# Bandit Level 18

## 1. 목표
- bandit18은 ssh에 접속하면 바로 접속이 끊기고 종료가 되어버린다. 
이 상황에서 비밀번호를 알아내야한다.

## 2. 문제 분석
- 로그인 셸을 열지 말고 SSH 접속과 동시에 명령어를 실행해야한다.

## 3. 사용 명령어
- ssh

## 4. 명령어 분석
- ssh 접속과 동시에 명령어를 실행한다.
    - ssh bandit18@bandit.labs.overthewire.org -p 2220 "cat readme"
