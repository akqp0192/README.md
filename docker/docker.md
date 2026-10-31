# Docker 설치 및 기본 명령어 실습

## 1. 실습 환경

| 항목 | 내용 |
|---|---|
| 운영체제 | Ubuntu 26.04.1 LTS |
| 실행 환경 | WSL2 |
| 터미널 | Ubuntu Bash |
| Docker 버전 | 29.9.2 |
| 실습 도구 | Docker Engine |

## 2. Docker 설치 및 버전 확인

Ubuntu 환경에 Docker Engine을 설치하고 정상적으로 작동하는지 확인하였다.

### Docker 버전 확인

```bash
sudo docker --version
```

실행 결과:

```text
Docker version 29.9.2, build a82e528
```

### Docker 설치 확인

```bash
sudo docker run hello-world
```

실행 결과:

```text
Hello from Docker!
This message shows that your installation appears to be working correctly.
```

Docker가 정상적으로 설치되고 컨테이너를 실행할 수 있음을 확인하였다.

### Docker 시스템 정보 확인

```bash
sudo docker info
```

Docker의 버전, 컨테이너 개수, 이미지 개수, 운영체제 등의 정보를 확인하였다.

## 3. Docker 기본 명령어 실습

### 이미지 목록 확인

```bash
sudo docker images
```

현재 로컬에 저장된 Docker 이미지를 확인하였다.

### 실행 중인 컨테이너 확인

```bash
sudo docker ps
```

### 전체 컨테이너 확인

```bash
sudo docker ps -a
```

실행 중인 컨테이너와 종료된 컨테이너를 모두 확인하였다.

## 4. Ubuntu 컨테이너 실행

Ubuntu 이미지를 이용하여 컨테이너를 생성하고 내부에 접속하였다.

```bash
sudo docker run -it --name ubuntu-practice ubuntu bash
```

컨테이너 내부에서 다음 명령어를 실행하였다.

```bash
pwd
ls
echo "Hello Codyssey Docker!"
```

컨테이너에서 나올 때는 다음 명령어를 사용하였다.

```bash
exit
```

### 종료된 컨테이너 다시 실행하기

```bash
sudo docker start ubuntu-practice
```

### 실행 중인 컨테이너 내부에 다시 접속하기

```bash
sudo docker exec -it ubuntu-practice bash
```

`docker exec` 명령어를 사용하여 실행 중인 컨테이너에 다시 접속할 수 있음을 확인하였다.

## 5. 컨테이너 로그 및 리소스 확인

### 컨테이너 로그 확인

```bash
sudo docker logs ubuntu-practice
```

### 컨테이너 리소스 사용량 확인

```bash
sudo docker stats
```

CPU 사용량, 메모리 사용량, 네트워크 사용량 등을 확인하였다.

## 6. 사용자 정의 Docker 이미지 제작

NGINX를 기반으로 사용자 정의 웹 서버 이미지를 제작하였다.

기본 이미지인 `nginx:latest`를 사용하고, 직접 작성한 HTML 파일을 NGINX의 기본 웹 페이지 경로에 복사하였다.

### 이미지 빌드

```bash
sudo docker build -t codyssey-web .
```

- Base Image: nginx:latest
- Image Name: codyssey-web
- Customization: 직접 작성한 index.html 적용
- 목적: 사용자 정의 웹 페이지를 제공하는 컨테이너 제작

### 이미지 생성 확인

```bash
sudo docker images
```

`codyssey-web` 이미지가 생성된 것을 확인하였다.

## 7. 실습 결과

- Docker Engine 설치 및 버전 확인 완료
- `hello-world` 컨테이너 실행 성공
- Ubuntu 컨테이너 생성 및 내부 명령어 실행
- 컨테이너 시작, 종료 및 재접속 실습
- Docker 이미지 및 컨테이너 목록 확인
- 컨테이너 로그와 리소스 사용량 확인
- NGINX 기반 사용자 정의 이미지 빌드 성공
