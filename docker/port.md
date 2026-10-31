# Docker 포트 매핑 실습

## 1. 실습 목적

Docker 컨테이너 내부에서 실행되는 NGINX 웹 서버에 외부에서 접근할 수 있도록 포트 매핑을 설정하였다.

호스트의 8080번 포트와 컨테이너의 80번 포트를 연결하여 웹 페이지에 접속하는 것을 목표로 하였다.

## 2. 실습 환경

| 항목 | 내용 |
|---|---|
| 운영체제 | Ubuntu 26.04.1 LTS |
| 실행 환경 | WSL2 |
| Docker 이미지 | codyssey-web |
| 컨테이너 이름 | codyssey-web-server |
| 호스트 포트 | 8080 |
| 컨테이너 포트 | 80 |

## 3. 컨테이너 실행 및 포트 매핑

앞서 제작한 `codyssey-web` 이미지를 사용하여 컨테이너를 실행하였다.

```bash
sudo docker run -d --name codyssey-web-server -p 8080:80 codyssey-web
```

### 명령어 설명

- `-d`: 컨테이너를 백그라운드에서 실행
- `--name`: 컨테이너 이름 지정
- `-p 8080:80`: 호스트의 8080번 포트를 컨테이너의 80번 포트에 연결
- `codyssey-web`: 실행할 Docker 이미지 이름

## 4. 컨테이너 실행 상태 확인

```bash
sudo docker ps
```

실행 중인 컨테이너 목록에서 `codyssey-web-server`의 상태와 포트 매핑을 확인하였다.

포트 매핑 결과:

```text
0.0.0.0:8080->80/tcp
```

## 5. 웹 브라우저 접속 확인

웹 브라우저 주소창에 다음 주소를 입력하였다.

```text
http://localhost:8080
```

직접 제작한 HTML 페이지가 정상적으로 출력되는 것을 확인하였다.

페이지에는 다음 문구가 표시된다.

- Hello, Codyssey!
- My first Docker Web Server is running.
- Powered by NGINX

## 6. 실습 결과

- NGINX 기반 Docker 컨테이너 실행 성공
- 호스트 포트 8080번과 컨테이너 포트 80번 연결 성공
- `docker ps`를 통한 포트 매핑 확인
- 웹 브라우저에서 `localhost:8080` 접속 성공
- 사용자 정의 HTML 페이지 출력 확인

