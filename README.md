# OverTheWire Bandit Write-up

OverTheWire Bandit 실습을 통해 학습한 Linux 명령어와
보안 기초 개념을 기록한 저장소입니다.

## 학습 목표 
- Linux 파일 및 디렉터리 구조 이해
- 특수한 파일명과 숨김 파일 처리
- find를 이용한 조건 기반 파일 탐색
- grep, sort, uniq를 이용한 텍스트 분석
- strings를 이용한 바이너리 문자열 추출
- Base64 인코딩과 디코딩 이해
- 표준 출력, 오류 출력 및 파이프 이해
- ROT13형식 파일 복원방법 이해
- 다양한 파일 형식 이해 및 형식 변경 및 압축해제
- SSH 공개키 인증 개념을 이해한다.
- localhost접속을 이해한다.
- SSL/TLS접속으로 암호화된 네트워크를 이해한다.
- 포트스캔을 이해한다.
- 파일을 비교한다.
- 로그인셸 접속없이 바로 파일에 접근해본다.
- SUID가 설정된 파일을 이해한다.

## Progress

| Level | 핵심 개념 | 정리 |
|---|---|---|
| 0 → 1 | SSH, cat | [보기](levels/level-00-01.md) |
| 1 → 2 | 특수 파일명 `-` | [보기](levels/level-01-02.md) |
| 2 → 3 | 공백과 옵션 종료 | [보기](levels/level-02-03.md) |
| 3 → 4 | 숨김 파일 | [보기](levels/level-03-04.md) |
| 4 → 5 | file 명령어 | [보기](levels/level-04-05.md) |
| 5 → 6 | find 조건 검색 | [보기](levels/level-05-06.md) |
| 6 → 7 | 소유자·그룹 검색 | [보기](levels/level-06-07.md) |
| 7 → 8 | grep 문자열 검색 | [보기](levels/level-07-08.md) |
| 8 → 9 | sort, uniq | [보기](levels/level-08-09.md) |
| 9 → 10 | strings | [보기](levels/level-09-10.md) |
| 10 → 11 | Base64 디코딩 | [보기](levels/level-10-11.md) |
| 11 → 12 | ROT13 복원| [보기](levels/level-11-12.md) |
| 12 → 13| 파일형식분석| [보기](levels/level-12-13.md) |
| 13 → 14| SSH 공개키인증| [보기](levels/level-13-14.md) |
|14 → 15|localhost 접속| [보기](levels/level-14-15.md)
|15 → 16|SSL/TLS연결 | [보기](levels/level-15-16.md)
|16 → 17|포트스캔 |[보기](levels/level-16-17.md)
|17 → 18|파일 비교 |[보기](levels/level-17-18.md)
|18 → 19|로그인셸없이 바로 접속|[보기](levels/level-18-19.md)
|19 → 20|SUID |[보기](levels/level-19-20.md)

## Security Policy

실제 비밀번호와 인증정보는 저장소에 기록하지 않습니다.
