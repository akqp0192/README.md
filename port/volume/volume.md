# Docker Volume 및 Bind Mount 실습

## 1. 실습 목적

Docker 컨테이너에서 데이터를 저장하고 공유하는 방법인 Volume과 Bind Mount를 실습하였다.

컨테이너가 삭제되더라도 데이터가 유지되는지 확인하고, 호스트와 컨테이너 사이에서 파일이 공유되는 원리를 이해하는 것을 목표로 하였다.

## 2. 실습 환경

| 항목 | 내용 |
|---|---|
| 운영체제 | Ubuntu 26.04.1 LTS |
| 실행 환경 | WSL2 |
| Docker 버전 | 29.9.2 |
| 사용 이미지 | ubuntu |
| Volume 이름 | codyssey-volume |
| 마운트 경로 | /data |

## 3. Docker Volume 실습

### 3-1. Volume 생성

```bash
sudo docker volume create codyssey-volume
```

생성된 Volume 확인:

```bash
sudo docker volume ls
```

`codyssey-volume`이 목록에 표시되는 것을 확인하였다.

### 3-2. 컨테이너에 Volume 연결

```bash
sudo docker run -it --name volume-test -v codyssey-volume:/data ubuntu bash
```

컨테이너 내부에서 파일을 생성하고 내용을 입력하였다.

```bash
echo "Codyssey Volume Persistence Test" > /data/test.txt
cat /data/test.txt
```

실행 결과:

```text
Codyssey Volume Persistence Test
```

### 3-3. 컨테이너 삭제

컨테이너에서 나간 후 컨테이너를 삭제하였다.

```bash
exit
sudo docker rm volume-test
sudo docker ps -a
```

기존 `volume-test` 컨테이너가 삭제된 것을 확인하였다.

### 3-4. 데이터 유지 확인

새로운 컨테이너를 실행하고 기존 Volume을 다시 연결하였다.

```bash
sudo docker run --rm -it -v codyssey-volume:/data ubuntu bash
```

기존 파일 확인:

```bash
cat /data/test.txt
```

실행 결과:

```text
Codyssey Volume Persistence Test
```

기존 컨테이너를 삭제했음에도 파일 내용이 유지되는 것을 확인하였다.

## 4. Bind Mount 실습

### 4-1. 호스트 디렉터리 및 파일 생성

프로젝트 폴더 내부에 Bind Mount 실습용 디렉터리를 생성하였다.

```bash
mkdir -p bind-mount-test
cd bind-mount-test
echo "Before: Host file original content" > test.txt
cat test.txt
```

### 4-2. 컨테이너에 호스트 디렉터리 연결

호스트의 현재 디렉터리를 컨테이너의 `/data` 경로에 연결하였다.

```bash
sudo docker run -it --name bind-mount-test -v "$(pwd):/data" ubuntu bash
```

컨테이너 내부에서 파일 내용을 확인하였다.

```bash
cat /data/test.txt
```

실행 결과:

```text
Before: Host file original content
```

### 4-3. 호스트 파일 수정 및 공유 확인

컨테이너에서 나온 후 호스트에서 파일 내용을 수정하였다.

```bash
echo "After: Host file has been modified!" > test.txt
cat test.txt
```

컨테이너에서도 변경된 내용이 반영되었는지 확인하였다.

```bash
sudo docker start bind-mount-test
sudo docker exec -it bind-mount-test bash
cat /data/test.txt
```

실행 결과:

```text
After: Host file has been modified!
```

호스트에서 수정한 파일 내용이 컨테이너 내부에도 반영되는 것을 확인하였다.

## 5. Volume과 Bind Mount 비교

| 구분 | Docker Volume | Bind Mount |
|---|---|---|
| 저장 위치 | Docker가 관리하는 영역 | 호스트의 지정 경로 |
| 연결 방식 | Volume 이름으로 연결 | 호스트 경로로 연결 |
| 주요 목적 | 컨테이너 데이터 유지 | 호스트와 컨테이너 간 파일 공유 |
| 특징 | 컨테이너 삭제 후에도 데이터 유지 | 호스트 파일 변경 사항이 컨테이너에 반영 |

## 6. 실습 결과

- Docker Volume 생성 및 확인 완료
- 컨테이너에 Volume 연결 성공
- 컨테이너 삭제 후에도 Volume 데이터 유지 확인
- Bind Mount를 이용한 호스트 디렉터리 연결 성공
- 호스트에서 수정한 파일이 컨테이너 내부에 반영되는 것 확인
