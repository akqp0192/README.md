# Linux 터미널 조작 실습 기록

## 1. 실습 개요

- 실습 환경: Windows + WSL2 + Ubuntu
- 사용자: user
- 작업 디렉터리: `/home/user/codyssey-practice/terminal-test`
- 실습 목적: Linux 터미널을 이용한 파일 및 디렉터리 관리 명령어 학습

## 2. 수행 항목 및 검증 결과

### 2-1. 현재 위치 확인

**명령어**
```bash
pwd
```

**실행 결과**
```text
/home/user
```

### 2-2. 파일 목록 확인 (숨김 파일 포함)

**명령어**
```bash
ls -la
```

**확인 결과**
- `.bashrc`, `.profile` 등 숨김 파일 확인
- 파일 및 디렉터리의 권한, 소유자, 크기 확인

### 2-3. 디렉터리 이동 및 생성

**명령어**
```bash
cd ~/codyssey-practice
pwd
mkdir terminal-test
ls -l
cd terminal-test
```

**확인 결과**
- `codyssey-practice` 디렉터리로 이동
- `terminal-test` 디렉터리 생성 확인
- 해당 디렉터리 내부로 이동

### 2-4. 빈 파일 생성 및 내용 확인

**명령어**
```bash
touch hello.txt
ls -l
echo "Hello Codyssey!" > hello.txt
cat hello.txt
```

**실행 결과**
```text
Hello Codyssey!
```

- `touch`로 빈 파일 생성
- `echo`와 리다이렉션 기호 `>`로 파일에 내용 작성
- `cat`으로 파일 내용 확인

### 2-5. 파일 복사

**명령어**
```bash
cp hello.txt hello-copy.txt
ls -l
```

**확인 결과**
- `hello.txt`를 `hello-copy.txt`로 복사
- 원본 파일과 복사 파일이 모두 존재하는 것을 확인

### 2-6. 파일 이름 변경 및 이동

**명령어**
```bash
mv hello-copy.txt hello-renamed.txt
cat hello-renamed.txt
mkdir backup
mv hello-renamed.txt backup/
ls -l backup/
```

**실행 결과**
```text
Hello Codyssey!
```

- 파일 이름 변경 확인
- `backup` 디렉터리 생성
- 변경한 파일을 `backup` 디렉터리로 이동
- 이동한 파일의 존재 확인

### 2-7. 파일 삭제

**명령어**
```bash
rm hello.txt
ls -l
ls -l backup/
```

**확인 결과**
- `hello.txt` 삭제 확인
- `backup/hello-renamed.txt` 파일은 유지됨을 확인

## 3. 핵심 명령어 정리

| 명령어 | 기능 |
|---|---|
| `pwd` | 현재 작업 디렉터리 확인 |
| `ls -la` | 숨김 파일을 포함한 상세 목록 확인 |
| `cd` | 디렉터리 이동 |
| `mkdir` | 디렉터리 생성 |
| `touch` | 빈 파일 생성 |
| `echo` | 문자열 출력 및 파일 기록 |
| `cat` | 파일 내용 확인 |
| `cp` | 파일 복사 |
| `mv` | 파일 이동 및 이름 변경 |
| `rm` | 파일 삭제 |

## 4. 증거 자료

실제 실습 화면은 다음 경로에서 확인할 수 있다.

- [현재 위치 및 파일 목록](../evidence/02-terminal/1.%20pwd,%20ls%20-la.png)
- [파일 복사](../evidence/02-terminal/2.%20cp.png)
- [디렉터리 생성](../evidence/02-terminal/3.%20mkdir.png)
- [이동 및 파일 생성·내용 확인](../evidence/02-terminal/4.%20cd,%20touch,%20echo,%20cat.png)
- [파일 이름 변경 및 이동](../evidence/02-terminal/5.%20mv.png)
- [파일 삭제](../evidence/02-terminal/6.%20rm.png)

## 5. 실습 결과

Linux 터미널의 기본 파일 및 디렉터리 관리 명령어를 직접 실행하였다. 파일 생성, 복사, 이름 변경, 이동 및 삭제 과정을 수행하고 명령어별 결과를 확인하였다.