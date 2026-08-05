# Bandit Level 22

## 1. 목표
- cron으로 실행되는 스크립트를 분석하여 다음 레벨인 bandit23의 비밀번호가 저장된 파일을 찾아야한다.

## 2. 문제 분석
- bandit23 관련 cron 파일을 찾는다.
- cron 스크립트 분석
```bash
#!/bin/bash

myname=$(whoami)

mytarget=$(echo I am user $myname | md5sum | cut -d ' ' -f 1)

echo "Copying passwordfile /etc/bandit_pass/$myname to /tmp/$mytarget"

cat /etc/bandit_pass/$myname > /tmp/$mytarget
```
- cron 스크립트는 bandit23 권항으로 실행, myname=bandit23
- mytarget에 해시값이 저장된다.
- 해시값이 복사할 파일명이된다.
- 파일을 출력해서 비밀번호를 알아낸다.

## 3. 사용 명령어
- md5sum
- cut 


## 4. 명령어 분석
- md5sum
```bash
echo I am user bandit23 | md5sum
```
 문자열의MD5 해시값을 생성한다.

- cut -d ' ' -f 1
    - 공백을 기준으로 첫 번째 필드만 가져온다.
        - -d ' ' : 공백을 구분자로 사용
        - -f 1 : 첫 번째 필드 출력