# Linux Terminal 실습 기록

## 1. 실습 목적

Linux Bash 환경에서 기본적인 파일 및 디렉터리 관리 명령어를 익히고 직접 실행한다.

## 2. 실습 환경

- OS: Ubuntu 26.04.1 LTS
- Terminal: Ubuntu Bash (WSL2)

## 3. 현재 위치 확인

```bash
pwd
```

실행 결과:
```text
/home/user
```

## 4. 숨김 파일을 포함한 목록 확인

```bash
ls -la
```

숨김 파일과 디렉터리를 포함한 전체 목록을 확인했다.

## 5. 디렉터리 이동 및 생성

```bash
cd ~/codyssey-practice
mkdir terminal-test
cd terminal-test
```

`cd` 명령어로 디렉터리를 이동하고 `mkdir` 명령어로 새로운 디렉터리를 생성했다.

## 6. 파일 생성 및 내용 입력

```bash
touch hello.txt
echo "Hello Codyssey!" > hello.txt
cat hello.txt
```

실행 결과:
```text
Hello Codyssey!
```

`touch`로 파일을 생성하고 `echo`로 내용을 입력한 뒤 `cat`으로 확인했다.

## 7. 파일 복사

```bash
cp hello.txt hello-copy.txt
cat hello-copy.txt
```

실행 결과:
```text
Hello Codyssey!
```

원본 파일을 복사하고 복사된 파일의 내용을 확인했다.

## 8. 파일 이름 변경 및 이동

```bash
mv hello-copy.txt hello-renamed.txt
mkdir backup
mv hello-renamed.txt backup/
```

파일 이름을 변경하고 `backup` 디렉터리로 이동했다.

## 9. 파일 삭제

```bash
rm hello.txt
```

`rm` 명령어를 사용하여 파일을 삭제했다.

## 10. 실습 결과

- `pwd`: 현재 작업 디렉터리 확인
- `ls -la`: 숨김 파일을 포함한 목록 확인
- `cd`: 디렉터리 이동
- `mkdir`: 디렉터리 생성
- `touch`: 파일 생성
- `echo`: 파일에 내용 입력
- `cat`: 파일 내용 확인
- `cp`: 파일 복사
- `mv`: 파일 이름 변경 및 이동
- `rm`: 파일 삭제

