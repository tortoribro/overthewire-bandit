# Bandit Level 23 

## 1. 목표
- cron 스크립트를 읽고 크론 스크립트가 감시하고있는 파일을 찾은후 파일을 복사하여 cron이 실행하게 하여 비밀번호를 알아낸다.

## 2. 문제 분석
- cron 파일을 찾아 내용을 확인한다.
- cron 스크립트 내용 분석
```bash
#!/bin/bash

cd /var/spool/bandit24/foo
echo "Executing my scripts"
for i in * .*; do
    if [ "$i" != "." -a "$i" != ".." ]; then
        echo "Handling $i"
        owner=$(stat --format "%U" ./$i)
        if [ "${owner}" = "bandit23" ]; then
            timeout -s 9 60 ./$i
        fi
        rm -f ./$i
    fi
done
```
- 스크립트가 /var/spool/bandit24/foo 디렉토리로 이동한다.
- 해당 폴더 안의 모든 파일 중 소유자가 **bandit23**인 파일을 찾아 실행(./$i)한다.
- 실행이 끝나면 파일을 삭제(rm -f)한다.
- 스크립트 자체가 bandit24의 권한으로 동작하기때문에 직접 작성한 script도 bandit24 권한으로 실행된다.

- 자신만의 디렉토리와 비밀번호를 탈취하는 스크립트를 만든다.
- 디렉토리는 임시로 만들고 디렉토리와 파일권한은 모두 777로 부여 한다.

**비밀번호 탈취 스크립트**
```bash
echo '#!/bin/bash' > 파일명.sh
echo 'cat /etc/bandit_pass/bandit24 > /tmp/tmp/비밀번호저장할파일.txt' >> 파일명.sh
```
- 작성한 스크립트를 Cron이 감시하고있는 디렉터리로 복사한다.

```bash
cp /tmp/tmp/파일명.sh /var/spool/bandit24/foo/
```
- 작업은 1분마다 생성되고 1분정도 기다리면 비밀번호 탈취 스크립트가 실행되어 비밀번호저장파일에 비밀번호가 복사된다.

- cron 스크립트가 bandit24로 실행되기때문에 직접작성한 디렉토리와 스크립트를 777권한만 주면 cron 스크립트에 의해 bandit24권한으로 실행된다.

## 3. 사용 명령어
- cp
- echo

## 4. 명령어 분석

- 핵심 개념: Cron Job Exploitation (권한 승격)

    - Cron 스크립트가 /var/spool/bandit24/foo/ 디렉터리 내의 모든 파일(스크립트)을 실행한 뒤 삭제함.
    따라서 내가 만든 스크립트를 저 위치에 넣어두면, bandit24 권한을 가진 Cron이 대신 내 스크립트를 실행해 줌.
