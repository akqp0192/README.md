# Docker 실습 기록

## 1. 실습 목적

Docker Engine을 설치하고 이미지 및 컨테이너의 생성, 실행, 관리 방법을 학습한다. 또한 Dockerfile을 이용한 커스텀 웹 서버 구축과 Volume 및 Bind Mount를 통한 데이터 관리 방법을 실습한다.

## 2. 실습 환경

| 항목 | 환경 |
|---|---|
| OS | Windows + WSL2 |
| Linux | Ubuntu 26.04.1 LTS |
| Terminal | Ubuntu Bash |
| Docker Engine | 29.9.2 |
| Docker Kernel | Linux 6.18.54.1 WSL2 |

## 3. Docker 설치 및 동작 확인

### Docker 버전 확인

```bash
docker --version
```

실행 결과:
```text
Docker version 29.9.2, build a82e528
```

### Hello World 실행

```bash
sudo docker run hello-world
```

실행 결과:
```text
Hello from Docker!
This message shows that your installation appears to be working correctly.
```

### Docker 데몬 동작 확인

```bash
sudo docker info
```

Docker Client와 Server 정보를 확인했으며 Server Version 29.9.2로 정상 동작하는 것을 확인했다.

## 4. Docker 이미지 및 컨테이너 관리

### 이미지 목록 확인

```bash
sudo docker images
```

### 실행 중인 컨테이너 확인

```bash
sudo docker ps
```

### 전체 컨테이너 확인

```bash
sudo docker ps -a
```

### 컨테이너 로그 확인

```bash
sudo docker logs ubuntu-practice
```

컨테이너 내부에서 실행한 명령어와 종료 기록을 확인했다.

### 컨테이너 리소스 사용량 확인

```bash
sudo docker stats
```

CPU, 메모리, 네트워크 I/O 및 PID 정보를 확인했다.

## 5. Ubuntu 컨테이너 실습

### Ubuntu 컨테이너 실행

```bash
sudo docker run -it --name ubuntu-practice ubuntu bash
```

컨테이너 내부에서 다음 명령어를 실행했다.

```bash
pwd
ls
echo "Hello Codyssey Docker!"
```

### 실행 중인 컨테이너 재진입

```bash
sudo docker start ubuntu-practice
sudo docker exec -it ubuntu-practice bash
```

`exit` 명령어를 사용하여 컨테이너 내부 터미널에서 나오는 방법도 확인했다.

## 6. 커스텀 NGINX 이미지 제작

### 선택한 베이스 이미지

- 베이스 이미지: `nginx:latest`
- 제작 방식: 기존 웹 서버 이미지에 사용자 정의 정적 HTML 콘텐츠 적용

### Dockerfile

```dockerfile
FROM nginx:latest

COPY app/index.html /usr/share/nginx/html/index.html

EXPOSE 80
```

### 커스텀 포인트 및 목적

1. `FROM nginx:latest`
   - 기존 NGINX 웹 서버 이미지를 기반으로 사용한다.

2. `COPY app/index.html /usr/share/nginx/html/index.html`
   - 직접 제작한 HTML 파일을 NGINX 기본 웹 페이지 대신 적용한다.

3. `EXPOSE 80`
   - 컨테이너 내부 웹 서버가 사용하는 포트를 명시한다.

### 이미지 빌드

```bash
sudo docker build -t codyssey-web .
```

### 이미지 확인

```bash
sudo docker images
```

### 컨테이너 실행

```bash
sudo docker run -d --name codyssey-web-server -p 8080:80 codyssey-web
```

### 실행 상태 확인

```bash
sudo docker ps
```

호스트의 8080 포트와 컨테이너의 80 포트를 연결했다.

브라우저에서 다음 주소로 접속하여 사용자 정의 웹 페이지가 출력되는 것을 확인했다.

`http://localhost:8080`

## 7. Docker Volume 실습

### Volume 생성

```bash
sudo docker volume create codyssey-volume
sudo docker volume ls
```

### Volume 연결 및 데이터 저장

```bash
sudo docker run -it --name volume-test -v codyssey-volume:/data ubuntu bash
```

컨테이너 내부에서 실행:

```bash
echo "Codyssey Volume Persistence Test" > /data/test.txt
cat /data/test.txt
```

### 컨테이너 삭제

```bash
exit
sudo docker rm volume-test
```

### 데이터 영속성 검증

새로운 컨테이너에 기존 Volume을 연결했다.

```bash
sudo docker run --rm -it -v codyssey-volume:/data ubuntu bash
```

컨테이너 내부에서 확인:

```bash
cat /data/test.txt
```

실행 결과:

```text
Codyssey Volume Persistence Test
```

기존 컨테이너를 삭제한 후에도 Volume에 저장된 데이터가 유지되는 것을 확인했다.

## 8. Bind Mount 실습

### 호스트 파일 생성

```bash
mkdir -p bind-mount-test
cd bind-mount-test
echo "Before: Host file original content" > test.txt
cat test.txt
```

### Bind Mount 연결

```bash
sudo docker run -it --name bind-mount-test -v "$(pwd):/data" ubuntu bash
```

컨테이너 내부에서 호스트 파일 확인:

```bash
cat /data/test.txt
```

### 호스트 파일 수정

컨테이너에서 나온 후 호스트에서 실행:

```bash
echo "After: Host file has been modified!" > test.txt
cat test.txt
```

### 컨테이너 내부 변경 사항 확인

```bash
sudo docker start bind-mount-test
sudo docker exec -it bind-mount-test bash
```

컨테이너 내부에서 실행:

```bash
cat /data/test.txt
```

실행 결과:

```text
After: Host file has been modified!
```

호스트에서 변경한 파일 내용이 컨테이너 내부에도 반영되는 것을 확인했다.

## 9. 실습 결과 및 학습 내용

- Docker Engine 설치 및 버전 확인
- Docker 이미지와 컨테이너 관리 명령어 학습
- Ubuntu 컨테이너 실행 및 내부 명령어 사용
- Dockerfile을 활용한 커스텀 NGINX 이미지 제작
- 포트 매핑을 통한 웹 서버 접속 확인
- Volume을 활용한 데이터 영속성 확인
- Bind Mount를 통한 호스트와 컨테이너 간 파일 공유 확인

