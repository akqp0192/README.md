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
## 7. 추가 검증 및 운영 가이드

### 7-1. Docker 이미지와 컨테이너 전체 목록 확인

이미지는 컨테이너를 생성하기 위한 실행 템플릿이고, 컨테이너는 이미지를 바탕으로 실제 실행되는 독립된 인스턴스입니다. 예를 들어 `codyssey-web`은 NGINX와 웹 파일이 포함된 이미지이며, `codyssey-web-server`는 이 이미지로 실행한 컨테이너입니다. 이미지를 빌드해도 컨테이너가 자동 실행되지는 않으며, 컨테이너 내부에서 변경한 내용은 별도 저장소에 기록하지 않으면 컨테이너 삭제 시 사라질 수 있습니다.

이미지와 전체 컨테이너 목록은 다음 명령으로 확인합니다.

```bash
sudo docker images
sudo docker ps -a
```

실습 증거를 남길 때는 명령어와 출력 전체가 한 화면에 보이도록 터미널 로그를 저장하고, 이미지 이름·태그·이미지 ID 및 컨테이너 ID·상태·포트 항목이 잘리지 않도록 캡처합니다.

### 7-2. 웹 서버 접속 검증

컨테이너가 실행 중인지 먼저 확인한 다음 호스트에서 HTTP 응답을 요청합니다.

```bash
sudo docker ps
curl -i http://localhost:8080
```

정상 동작 시 HTTP 응답 헤더에 `200 OK`가 표시되고, 응답 본문에는 사용자 정의 페이지의 `Hello, Codyssey!` 문구가 포함됩니다. 브라우저로 확인할 때는 `http://localhost:8080`에 접속한 화면도 함께 캡처합니다. 접속이 실패하면 컨테이너 상태와 로그를 순서대로 확인합니다.

```bash
sudo docker ps -a
sudo docker logs codyssey-web-server
```

### 7-3. 포트 매핑과 네트워크 네임스페이스

컨테이너는 기본적으로 호스트와 분리된 네트워크 네임스페이스를 사용합니다. 네트워크 네임스페이스는 컨테이너별 네트워크 인터페이스, IP 주소, 라우팅 테이블, 포트 공간을 격리합니다. 따라서 컨테이너 내부에서 NGINX가 80번 포트를 사용하더라도 호스트에서 바로 같은 주소로 접근하는 것은 아닙니다. `-p 8080:80` 옵션은 호스트의 8080번 포트로 들어온 트래픽을 컨테이너의 80번 포트로 전달하도록 연결합니다.

```bash
sudo docker run -d --name codyssey-web-server -p 8080:80 codyssey-web
```

### 7-4. Git 원격 저장소 및 Push 확인

원격 저장소 주소와 연결 이름은 다음 명령으로 확인합니다.

```bash
git remote -v
```

이 저장소의 원격 주소는 다음과 같습니다.

```text
origin  https://github.com/akqp0192/README.md.git (fetch)
origin  https://github.com/akqp0192/README.md.git (push)
```

최근 커밋과 원격 반영 여부는 다음 명령으로 확인합니다.

```bash
git log --oneline --decorate -10
git status -sb
git push origin main
```

GitHub의 [커밋 이력](https://github.com/akqp0192/README.md/commits/main)에서도 원격 저장소에 반영된 커밋을 확인할 수 있습니다. 제출 증거에는 `git remote -v` 전체 출력과 Push 성공 후 커밋 이력 화면을 첨부합니다.

### 7-5. 디렉터리별 역할과 구성 기준

실습 주제별로 디렉터리를 분리하여 관련 명령어, 설명 문서, 실행 증거를 빠르게 찾을 수 있도록 구성했습니다.

- `terminal/`: Linux 기본 명령어 실습 순서와 실행 기록을 보관합니다.
- `permission/`: 파일·디렉터리 권한 변경 명령과 결과를 보관합니다.
- `docker/`: Docker 설치, 이미지 빌드, 컨테이너 실행 관련 문서와 Dockerfile을 보관합니다.
- `port/`: 포트 매핑과 웹 서버 접속 실습을 보관합니다.
- `port/volume/`: Volume 및 Bind Mount의 데이터 영속성 실습을 보관합니다.
- `evidence/`: 각 실습 단계의 원본 터미널 출력과 화면 캡처를 주제별로 보관합니다.

### 7-6. 재현 절차: 이미지 빌드부터 웹 접속까지

아래 순서로 실행하면 커스텀 웹 서버 실습을 재현할 수 있습니다.

1. 프로젝트 저장소를 내려받고 Docker 데몬이 실행 중인지 확인합니다.
2. Dockerfile과 `app/index.html`이 있는 프로젝트 루트로 이동합니다.
3. 이미지 빌드 후 이미지 목록에서 생성 여부를 확인합니다.
4. 컨테이너를 실행하고 포트 매핑을 확인합니다.
5. 브라우저 또는 curl로 웹 페이지 응답을 확인합니다.

```bash
# 1. Docker 데몬 및 프로젝트 파일 확인
sudo docker info
ls -la

# 2. 이미지 빌드
sudo docker build -t codyssey-web .

# 3. 이미지 생성 확인
sudo docker images

# 4. 컨테이너 실행
sudo docker run -d --name codyssey-web-server -p 8080:80 codyssey-web

# 5. 실행 상태와 포트 확인
sudo docker ps

# 6. 웹 응답 확인
curl -i http://localhost:8080
```

예상 확인 항목은 이미지 목록의 `codyssey-web`, 컨테이너 목록의 `codyssey-web-server`, 포트 매핑 `0.0.0.0:8080->80/tcp`, HTTP 응답 `200 OK` 및 페이지 본문입니다. 동일한 이름의 컨테이너가 이미 존재하면 먼저 `sudo docker rm -f codyssey-web-server`로 기존 컨테이너를 정리한 뒤 다시 실행합니다.

### 7-7. 포트 충돌 진단 및 해결

호스트 8080번 포트를 다른 프로세스가 사용 중이면 Docker 실행 시 `port is already allocated` 또는 `address already in use` 오류가 발생할 수 있습니다. 먼저 포트를 점유한 프로세스를 확인합니다.

```bash
# Linux / WSL
sudo ss -ltnp | grep ':8080'
# 대체 명령
sudo lsof -i :8080
```

출력에서 PID와 프로세스를 확인한 뒤, 해당 프로그램이 불필요한지 확인하고 정상 종료합니다. 프로세스를 종료해도 되는 경우에만 다음 명령을 사용합니다.

```bash
sudo kill <PID>
# 정상 종료되지 않고 종료가 꼭 필요한 경우에만 사용
sudo kill -9 <PID>
```

Docker 컨테이너가 포트를 점유하고 있다면 프로세스를 강제 종료하기보다 먼저 컨테이너 이름과 포트 매핑을 확인하고 정상 중지합니다.

```bash
sudo docker ps
sudo docker stop codyssey-web-server
```

프로세스 종료 후 `ss` 명령으로 포트가 해제되었는지 확인하고 컨테이너를 다시 실행합니다. 실제 제출 시에는 포트 점유 확인 전후의 `ss` 출력과 종료 명령 결과를 캡처합니다.

### 7-8. Docker Volume 백업 및 복구

Docker Volume은 컨테이너와 별도로 데이터를 보관하지만, 실수로 Volume을 삭제하거나 호스트 장애가 발생할 경우를 대비해 정기 백업이 필요합니다. 다음 예시는 `codyssey-volume`의 내용을 tar 파일로 백업하고 다시 복구하는 방법입니다.

```bash
# 백업 디렉터리 생성
mkdir -p backups

# Volume 내용을 tar.gz로 백업
sudo docker run --rm \
  -v codyssey-volume:/source:ro \
  -v "$(pwd)/backups:/backup" \
  ubuntu tar czf /backup/codyssey-volume-backup.tar.gz -C /source .

# 백업 파일 확인
ls -lh backups/
```

복구할 때는 대상 Volume을 생성한 후 백업 파일을 대상 Volume에 풀어 줍니다.

```bash
sudo docker volume create codyssey-volume-restore

sudo docker run --rm \
  -v codyssey-volume-restore:/target \
  -v "$(pwd)/backups:/backup:ro" \
  ubuntu tar xzf /backup/codyssey-volume-backup.tar.gz -C /target

# 복구된 파일 확인
sudo docker run --rm \
  -v codyssey-volume-restore:/data:ro \
  ubuntu ls -la /data
```

백업 파일은 컨테이너 내부가 아닌 호스트의 `backups/` 디렉터리에 보관합니다. 실제 운영에서는 백업 파일의 무결성과 복구 후 데이터 내용을 함께 확인해야 합니다.

### 7-9. 트러블슈팅 기록 방법

문제가 발생하면 원인 추측만 기록하지 않고 **가설 → 검증 → 조치 → 재검증** 순서로 정리합니다. 아래는 웹 서버 포트가 이미 사용 중인 경우에 적용할 수 있는 기록 예시이며, 실제 발생 여부와 명령 출력은 실습 환경에서 확인한 내용으로 채워야 합니다.

| 단계 | 기록할 내용 | 확인 명령 예시 |
|---|---|---|
| 가설 | 호스트 8080 포트를 다른 프로세스 또는 컨테이너가 점유했을 가능성 | 오류 메시지 확인 |
| 검증 | 포트 리스닝 프로세스와 Docker 포트 매핑 확인 | `sudo ss -ltnp | grep ':8080'`, `sudo docker ps` |
| 조치 | 불필요한 기존 컨테이너를 정상 중지하거나 사용 가능한 호스트 포트로 변경 | `sudo docker stop codyssey-web-server` 또는 `-p 8081:80` |
| 재검증 | 컨테이너 상태와 HTTP 응답 확인 | `sudo docker ps`, `curl -i http://localhost:8080` 또는 변경한 포트 |

실제 제출용 트러블슈팅 증거에는 오류 원문, 검증 명령의 전체 출력, 조치 명령, 조치 후 정상 동작 결과를 같은 사례로 묶어 첨부합니다. 실제로 발생하지 않은 오류나 실행하지 않은 명령의 결과를 실습 결과처럼 기재하지 않습니다.

