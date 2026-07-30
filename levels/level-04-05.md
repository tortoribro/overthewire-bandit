# Bandit Level 4

## 1. 목표
- inhere 디렉터리에 있는 여러 파일 중 사람이 읽을 수 있는 파일을 찾는다.

## 2. 문제 분석
파일 이름은 다음처럼 -로 시작한다.
```bash
-file00
-file01
-file02
...
```
파일 형식 확인
```bash 
file ./*
```
출력
```bash
./-file00: UTF-8 Unicode text
./-file01: PNG image data
./-file02: ELF executable
./-file07: ASCII text
...
```

ASCII text로 표시되는 파일이 사람이 읽을 수 있는 텍스트 파일이다.


## 3. 사용 명령어
file은 파일 이름이 아니라 실제 내용과 구조를 분석해 파일 형식을 추정한다.
```bash
file 파일명
```


## 4. 명령어 분석

```bash
file ./*
```
- . : 현재 디렉터리
- / : 경로 구분자
- * : 현재 디렉터리의 일반 파일 전체

숨긴 파일까지 file로 검사 , *는 숨김 파일을 포함하지 않는다.
```bash
find . -type f -exec file {} +
```
- find .: 현재 디렉터리부터 검색
- -type f: 일반 파일만 선택
- -exec: 찾은 파일에 명령 실행
- file: 파일 형식 판별
- {}: 찾은 파일 경로가 들어갈 자리
- +: 여러 파일을 한 번에 file에 전달