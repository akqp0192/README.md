# Codyssey 개발 환경 구축 프로젝트

## 1. 프로젝트 개요

본 프로젝트는 Windows 환경에서 WSL2 기반 Ubuntu를 구성하고 Linux 터미널, 파일 권한, Git/GitHub, Docker의 기본 사용법을 실습하는 것을 목적으로 한다.

Docker 이미지와 컨테이너를 직접 생성하고 관리했으며, NGINX 기반 커스텀 웹 서버와 데이터 영속성 및 파일 공유 기능을 검증했다.

## 2. 개발 환경

| 항목 | 사용 환경 |
|---|---|
| Host OS | Windows |
| Linux OS | Ubuntu 26.04.1 LTS |
| Linux 환경 | WSL2 |
| Terminal | Ubuntu Bash / PowerShell |
| Git | 2.56.0.windows.4 |
| Docker Engine | 29.9.2 |
| Docker Base Image | nginx:latest, ubuntu |
| Editor | Visual Studio Code |
| GitHub | akqp0192 |

## 3. 실습 진행 현황

### 01. Git 및 GitHub 환경 구축

- Git 설치 및 버전 확인
- Git 사용자 정보 설정
- GitHub 저장소 생성 및 연결
- VS Code와 GitHub 연동
- Commit 및 Push 실습

### 02. Linux Terminal 명령어 실습

- `pwd`: 현재 위치 확인
- `ls -la`: 숨김 파일을 포함한 목록 확인
- `cd`: 디렉터리 이동
- `mkdir`: 디렉터리 생성
- `touch`: 파일 생성
- `echo`: 파일 내용 입력
- `cat`: 파일 내용 확인
- `cp`: 파일 복사
- `mv`: 파일 이름 변경 및 이동
- `rm`: 파일 삭제

상세 기록: [terminal-log.md](terminal/terminal-log.md)

### 03. Linux Permission 실습

파일 및 디렉터리 권한을 확인하고 `chmod` 명령어로 권한을 변경했다.

| 대상 | 변경 전 | 변경 후 |
|---|---|---|
| test.txt | 644 | 600 |
| test-dir | 755 | 700 |

사용 명령어:

```bash
chmod 600 test.txt
chmod 700 test-dir
ls -ld test-dir
ls -l test.txt
```

상세 기록: [permission-log.md](permission/permission-log.md)

### 04. Docker 설치 및 컨테이너 실습

- Docker Engine 설치
- Docker 버전 확인
- `docker info`로 데몬 동작 확인
- Hello World 이미지 실행
- Ubuntu 컨테이너 실행 및 내부 명령어 실습
- 이미지 및 컨테이너 목록 확인
- 컨테이너 로그 및 리소스 사용량 확인

주요 명령어:

```bash
docker --version
sudo docker info
sudo docker images
sudo docker ps
sudo docker ps -a
sudo docker logs ubuntu-practice
sudo docker stats
```

상세 기록: [docker-log.md](docker/docker-log.md)

### 05. Dockerfile 기반 커스텀 웹 서버 제작

NGINX를 베이스 이미지로 사용하여 사용자 정의 HTML 웹 페이지를 포함한 커스텀 이미지를 제작했다.

Dockerfile:

```dockerfile
FROM nginx:latest
COPY app/index.html /usr/share/nginx/html/index.html
EXPOSE 80
```

이미지 빌드:

```bash
sudo docker build -t codyssey-web .
```

컨테이너 실행:

```bash
sudo docker run -d --name codyssey-web-server -p 8080:80 codyssey-web
```

브라우저 접속 주소:

http://localhost:8080

### 06. Docker Volume 실습

- Docker Volume 생성
- Volume을 컨테이너 `/data` 경로에 연결
- 데이터 저장 및 확인
- 기존 컨테이너 삭제
- 새로운 컨테이너에서 기존 데이터 유지 여부 검증

```bash
sudo docker volume create codyssey-volume
sudo docker volume ls
```

### 07. Docker Bind Mount 실습

- 호스트 디렉터리와 컨테이너 디렉터리 연결
- 호스트에서 파일 내용 수정
- 컨테이너 내부에서 변경 내용 반영 확인

```bash
sudo docker run -it --name bind-mount-test -v "$(pwd):/data" ubuntu bash
```

호스트에서 수정한 파일 내용이 컨테이너 내부에도 반영되는 것을 확인했다.

## 4. 프로젝트 폴더 구조

```text
README.md/
├── README.md
├── terminal/
│   └── terminal-log.md
├── permission/
│   └── permission-log.md
├── docker/
│   ├── Dockerfile
│   ├── app/
│   │   └── index.html
│   └── docker-log.md
└── evidence/
    ├── 01-git/
    ├── 02-terminal/
    ├── 03-permission/
    ├── 04-docker/
    ├── 05-port/
    └── 06-volume/
```

## 5. 증거 자료

각 실습의 실행 결과와 검증 화면은 `evidence/` 폴더에 단계별로 저장했다.

| 폴더 | 증거 자료 |
|---|---|
| 01-git | Git 및 GitHub 설정 |
| 02-terminal | Linux 터미널 명령어 |
| 03-permission | 파일 및 디렉터리 권한 변경 |
| 04-docker | Docker 설치 및 컨테이너 실행 |
| 05-port | NGINX 웹 서버 접속 |
| 06-volume | Volume 및 Bind Mount 검증 |

## 6. 최종 결과

본 프로젝트를 통해 Linux 기본 명령어와 권한 관리, Git 및 GitHub를 통한 버전 관리, Docker 이미지 및 컨테이너 관리 방법을 실습했다.

또한 NGINX 기반 커스텀 웹 서버를 구축하고 포트 매핑을 통해 웹 페이지 접속을 확인했다. Docker Volume과 Bind Mount를 활용하여 컨테이너 데이터의 영속성과 호스트-컨테이너 간 파일 공유 방식도 검증했다.