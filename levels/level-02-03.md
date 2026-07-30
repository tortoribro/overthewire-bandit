# Bandit Level 2

## 1. 목표
-  파일명이 --spaces in this filename-- 인 파일을 읽어야한다.

## 2. 문제 분석
- 파일명이 --로 시작하면 명령어가 옵션으로 오해할 수 있다.
- 셸은 

```txt
    인자1:--spaces 
    인자2: in  
    인자3: this 
    인자4: filename-- 
```
으로 해석된다.

## 3. 사용 명령어
```
cat "--spaces in this filename--"
```
공백앞에 \를 붙여도 된다.
```
cat ./--spaces\ in\ this\ filename--
```
## 4. 명령어 분석
- 큰따옴표를 사용하면 하나의 파일명으로 처리된다.