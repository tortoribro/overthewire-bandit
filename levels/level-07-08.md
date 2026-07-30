# Bandit Level 7

## 1. 목표
-  data.txt에서 millionth라는 단어가 포함된 줄을 찾는다.


## 2. 문제 분석
- grep을 이용해 파일에서 millionth 단어를 검색한다.


## 3. 사용 명령어

```bash
grep millionth data.txt
```

## 4. 명령어 분석
**grep**
```bash
grep 찾을문자열 파일명
```
- grep  옵션
    - -i : 대소문자 무시
    - -n : 줄 번호 표시
    - -w : 정확히 일치하는 단어 검색
    - -v : 일치하지 않는 줄 출력
    - -R : 여러 파일에서 재귀 검색

**cat과 파이프를 사용**
```bash
cat data.txt | grep millionth
```

