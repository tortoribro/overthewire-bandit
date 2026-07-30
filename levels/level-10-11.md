# Bandit Level 10 

## 1. 목표
- data.txt의 내용이 Base64로 인코딩되어 있다. 이를 원래 데이터로 디코딩한다.


## 2. 문제 분석
- Base64로 인코딩되어있는 파일을 디코딩해야한다.
    - Base64 데이터들은 다음 문자들로 구성된다.
```
A-Z
a-z
0-9
+
/
=
```

## 3. 사용 명령어

```bash
base64 -d data.txt
```
 or
```bash
base64 --decode data.txt
```

## 4. 명령어 분석
인코딩 
```
목적: 호환성, 전달, 저장
키: 필요 없음
복구: 누구나 가능
예: Base64, URL encoding
```
!=암호화
