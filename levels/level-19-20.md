# Bandit Level 19

## 1. 목표
- 홈 디렉터리에 있는 bandit20-do 라는 특수 실행파일을 이용해서 bandit20 권한으로 명령어를 실행하고, 다음단계의 비밀번호를 알아낸다.

## 2. 문제 분석
- 파일을 확인하면
```
-rwsr-x--- 1 bandit20 bandit19 ... bandit20-do 
```
- s는 SUID(Set User ID) 권한이 설정되어 있다는 뜻
- bandit20 권한으로 명령어를 실행해야한다.
```
./bandit20-do cat etc/bandit_pass/bandit20
```

## 3. 사용 명령어
- bandit20 권한으로 실행
```
./bandit20-do cat etc/bandit_pass/bandit20
```

## 4. 명령어 분석
- SUID가 설정된 실행파일은 파일 소유자의 권한으로 실행된다.

### 참고
- SUID가 설정된 파일
```
보통 프로그램은 실행한 사용자의 권한으로 동작한다.
하지만 SUID가 설정되면 실행될 때 파일 소유자의 권한으로 동작한다.
단 SUID가 있다고 해서 bandit19가 완전히 bandit20 사용자가 되는 것은 아니다.
다만, bandit20-do 프로그램이 실행되는 동안만 실효 UID(EUID) = bandit20
```
- 실제 UID와 실효 UID
| 구분            | 의미                |
| ------------- | ----------------- |
| Real UID      | 실제로 프로그램을 실행한 사용자 |
| Effective UID | 권한 검사에 사용되는 사용자   |

