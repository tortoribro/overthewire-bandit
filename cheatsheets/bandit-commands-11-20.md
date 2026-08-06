# OverTheWire Bandit 11–20 핵심 명령어

| 단계                 | 핵심 명령어                                                                                           | 핵심 내용                         |
| ---------------------     | ------------------------------------------------------------------------------------------------ | ----------------------------- |
| **Bandit 11 → 12** | `cat data.txt \| tr 'A-Za-z' 'N-ZA-Mn-za-m'`                                                     | `tr`을 이용한 ROT13 문자열 복호화       |
| **Bandit 12 → 13** | `tmpdir=$(mktemp -d)`                                                                            | 작업용 임시 디렉터리 생성                |
|                    | `cp data.txt "$tmpdir"`                                                                          | 원본 파일을 임시 디렉터리로 복사            |
|                    | `cd "$tmpdir"`                                                                                   | 임시 디렉터리로 이동                   |
|                    | `xxd -r data.txt > data`                                                                         | 16진수 덤프를 원본 바이너리 파일로 복원       |
|                    | `file data`                                                                                      | 현재 파일의 압축 형식 확인               |
|                    | `mv data data.gz`                                                                                | gzip 파일로 확장자 변경               |
|                    | `gzip -d data.gz`                                                                                | gzip 압축 해제                    |
|                    | `mv data data.bz2`                                                                               | bzip2 파일로 확장자 변경              |
|                    | `bzip2 -d data.bz2`                                                                              | bzip2 압축 해제                   |
|                    | `mv data data.tar`                                                                               | tar 파일로 확장자 변경                |
|                    | `tar -xf data.tar`                                                                               | tar 아카이브 해제                   |
| **Bandit 13 → 14** | `ls -l sshkey.private`                                                                           | SSH 개인키 파일 확인                 |
|                    | `chmod 600 sshkey.private`                                                                       | 개인키 파일 권한 제한                  |
|                    | `ssh -i sshkey.private bandit14@localhost -p 2220`                                               | 개인키를 이용해 Bandit 14로 접속        |
| **Bandit 14 → 15** | `cat /etc/bandit_pass/bandit14`                                                                  | 현재 Bandit 14 비밀번호 확인          |
|                    | `cat /etc/bandit_pass/bandit14 \| nc localhost 30000`                                            | 비밀번호를 TCP 30000번 포트로 전송       |
| **Bandit 15 → 16** | `cat /etc/bandit_pass/bandit15 \| openssl s_client -connect localhost:30001 -quiet`              | SSL/TLS 연결을 통해 비밀번호 전송        |
| **Bandit 16 → 17** | `nmap -sV --open -p 31000-32000 localhost`                                                       | 열린 포트와 SSL/TLS 서비스 탐색         |
|                    | `openssl s_client -connect localhost:<포트번호> -quiet`                                              | 발견한 SSL/TLS 포트에 연결            |
|                    | `cat /etc/bandit_pass/bandit16 \| openssl s_client -connect localhost:<포트번호> -quiet 2>/dev/null` | 현재 비밀번호를 전송해 SSH 개인키 획득       |
|                    | `tmpdir=$(mktemp -d) && cd "$tmpdir"`                                                            | 개인키를 저장할 임시 디렉터리 생성           |
|                    | `cat > bandit17.key`                                                                             | 출력된 개인키를 파일로 저장               |
|                    | `chmod 600 bandit17.key`                                                                         | 개인키 파일 권한 제한                  |
|                    | `ssh-keygen -y -f bandit17.key`                                                                  | 개인키 파일 형식 검증                  |
|                    | `ssh -i bandit17.key bandit17@localhost -p 2220`                                                 | 개인키를 이용해 Bandit 17로 접속        |
| **Bandit 17 → 18** | `ls -l passwords.old passwords.new`                                                              | 이전·새 비밀번호 파일 확인               |
|                    | `diff passwords.old passwords.new`                                                               | 두 파일에서 변경된 한 줄 확인             |
|                    | `grep -Fvx -f passwords.old passwords.new`                                                       | 새 파일에만 존재하는 줄 출력              |
| **Bandit 18 → 19** | `ssh bandit18@bandit.labs.overthewire.org -p 2220 "cat readme"`                                  | 로그인 셸을 열지 않고 원격 명령으로 비밀번호 확인  |
|                    | `ssh -p 2220 bandit18@bandit.labs.overthewire.org cat /home/bandit18/readme`                     | 절대경로를 이용해 원격 파일 읽기            |
| **Bandit 19 → 20** | `ls -l bandit20-do`                                                                              | SUID 실행파일과 권한 확인              |
|                    | `./bandit20-do whoami`                                                                           | 실행파일이 Bandit 20 권한으로 동작하는지 확인 |
|                    | `./bandit20-do cat /etc/bandit_pass/bandit20`                                                    | Bandit 20 권한으로 다음 비밀번호 파일 읽기  |
| **Bandit 20 → 21** | `ls -l suconnect`                                                                                | Bandit 21 소유의 SUID 실행파일 확인    |
|                    | `cat /etc/bandit_pass/bandit20 \| nc -l -p 12345`                                                | 첫 번째 터미널에서 포트를 열고 현재 비밀번호 전송  |
|                    | `nc -l 12345`                                                                                    | `-p` 옵션을 사용하지 않는 Netcat 문법    |
|                    | `./suconnect 12345`                                                                              | 두 번째 터미널에서 해당 포트에 접속해 비밀번호 검증 |
|                    | `ss -lnt \| grep 12345`                                                                          | 해당 TCP 포트의 수신 대기 상태 확인        |

## 명령어 핵심 요약

| 명령어                | 용도                  |
| ------------------ | ------------------- |
| `tr`               | 문자 치환 및 ROT13 복호화   |
| `xxd -r`           | 16진수 덤프를 바이너리로 복원   |
| `file`             | 파일 형식 확인            |
| `gzip -d`          | gzip 압축 해제          |
| `bzip2 -d`         | bzip2 압축 해제         |
| `tar -xf`          | tar 아카이브 해제         |
| `ssh -i`           | SSH 개인키 인증          |
| `chmod 600`        | 개인키를 소유자만 읽고 쓰도록 제한 |
| `nc`               | TCP 연결 및 포트 수신 대기   |
| `openssl s_client` | SSL/TLS 서비스 연결      |
| `nmap -sV`         | 포트 및 서비스 종류 탐지      |
| `diff`             | 두 파일의 내용 차이 비교      |
| `grep -Fvx`        | 다른 파일에 없는 줄 검색      |
| `ssh "명령어"`        | SSH 접속 후 원격 명령만 실행  |
| `./실행파일`           | 현재 디렉터리에 있는 프로그램 실행 |
| `ss -lnt`          | TCP 수신 대기 포트 확인     |
