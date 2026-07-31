# Bandit Level 13

## 1. 목표
- ssh private키를 이용해 원격접속을 한다.


## 2. 문제 분석
- 비대칭키(공개키,개인키)인증을 사용한다.
- bandit13에서는 다음 레벨의 비밀번호가 직접 제공되지 않기 때문에 홈 디렉터링 있는 ssh.private를 이용하여 bandit14 계정으로 접속해야한다.
- bandit 서버 내부에서 localhost로 접속시 permission deny
- 개인키를 자신의 계정으로 가져온뒤 개인키를 사용하여 다음레벨에 접속한다.
- 개인키권한도 제한해야한다. SSH 개인키가 다른 사용자에게 공개된 상태라면 OpenSSH가 보안상의 이유로 해당 키의 사용을 거부할 수 있다.
    - 예를들어 다음과 같은 경고가 발생할 수 있다.
        ```
        WARNING: UNPROTECTED PRIVATE KEY FILE!
        Permissions for 'sshkey.private' are too open.

        권한을 제한한다.

        chmod 600 sshkey.private
        ```
- 다음레벨에 접속해 /etc/bandit_pass/bandit14 에있는 현재 서버의 비밀번호를 확인한다.


## 3. 사용 명령어
- scp 
- ssh
- chmod
- mkdir

## 4. 명령어 분석
- scp -P 2220 bandit13@bandit.labs.overthewire.org:sshkey.private .

    |구성요소|의미|
    |-------|------|
    |scp	|SSH를 기반으로 파일을 안전하게 전송
    |-P 2220	|원격 서버의 SSH 포트를 2220번으로 지정
    |bandit13@...|	원격 서버의 사용자 계정과 주소
    |:sshkey.private|	원격 서버에서 가져올 파일
    |.	|현재 로컬 디렉터리에 저장

- ssh -i  ./sshkey.private bandit14@bandit.labs.overthewire.org -p 2220

    |구성요소|의미|
    |-------|------|
    |ssh	|원격 서버에 SSH로 접속
    |-i	|인증에 사용할 개인키 지정(-i는 SSH 인증에 사용할 identity file을 지정하는 옵션이다.)
    |./sshkey.private	|현재 디렉터리에 있는 개인키
    |bandit14|	접속할 사용자 계정
    |@	|사용자 이름과 서버 주소 구분
    |bandit.labs.overthewire.org	|접속할 Bandit 서버
    |-p 2220	|SSH 포트를 2220번으로 지정

- chmod 600 sshkey.private
   - -rw------- : 파일소유자만 읽고쓰기가 가능

- mkdir
  - 디렉토리 생성