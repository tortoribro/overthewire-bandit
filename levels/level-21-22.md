# Bandit Level 21

## 1. 목표
- cron이 자동으로 실행하는 작업을 추적해야 한다.

## 2. 문제 분석
- cron 설정 파일을 확인한다.
- bandit22관련 cron 설정을 읽는다.
- cron 설정에서 발견한 경로를 읽는다.
- 임시파일을 만들고 비밀번호를 담을 빈 txt파일을 만든다.
- 임시파일의 권한을 644로 변경한다.
- bandit22만 읽을 수 있는 파일을 임시파일에 저장시킨다.
- 임시파일 권한이 644 이기때문에 bandit21도 파일을 읽을 수가있다.

cron 스크립트
```bash
#!/bin/bash

chmod 644 /tmp/어떤파일명
cat /etc/bandit_pass/bandit22 > /tmp/어떤파일명

```

## 3. 사용 명령어
- ls -la /etc/cron.d/
- cat /etc/cron.d/cronjob_bandit22
- cat /usr/bin/cronjob_bandit22.sh
- cat /tmp/스크립트에서_확인한_파일명


## 4. 명령어 분석

- 핵심개념
#### cron 설정
```bash
* * * * *
│ │ │ │ │
│ │ │ │ └─ 요일
│ │ │ └─── 월
│ │ └───── 날짜
│ └─────── 시
└───────── 분

* * * * * bandit22 /usr/bin/cronjob_bandit22.sh &> /dev/null

* * * * * bandit22 실행할_명령
          └──────┘
          실행 사용자

매분 bandit22 사용자 권한으로
/usr/bin/cronjob_bandit22.sh 스크립트를 실행한다.
```

- &> /dev/null
    - 표준 출력 stdout
    - 표준 오류 stderr

    을 모두 /dev/null로 보낸다.