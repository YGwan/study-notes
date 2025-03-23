# How to enable communication between Docker containers?
- 도커 내부에서 각각의 컨테이너가 접근하는 방법

<br>

### 상황
- 도커 내부에 be서버 fe서버 db 존재
- fe -> be와 연결되어 있고, be -> db와 연결되어 있음

<br>

### 전제 조건
- Docker 컨테이너 간의 통신은 기본적으로 동일한 네트워크에 속하게 하여 컨테이너 이름을 DNS 이름처럼 사용할 수 있도록 하는 방식으로 활성화된다.
- Docker에서는 기본적으로 서로 다른 네트워크에 있는 컨테이너들 간의 통신이 격리되어 있다.

<br>

## 해결 방법

### 1. 컨테이너 실행 시 네트워크 지정

1. 네트워크 생성
``` shell
docker network create my_network
```

<br>

2. 컨테이너 실행 시 네트워크 지정
``` shell
docker run -d --name fe --network my_network fe-image
docker run -d --name be --network my_network be-image
docker run -d --name db --network my_network db-image
```

<br>

3. 환경 변수 관리
``` text
- container 명을 사용해서 접근
ex) jdbc:postgresql://[db 컨테이너 명]:[포트]/[db명]
```

<br>

---
### 2. docker-compose 로 관리
``` yaml
version: '3'
services:
  fe:
    build: fe-image
    networks:
      - my_network
  be:
    build: be-image
    networks:
      - my_network
  db:
    image: db-image
    environment:
      ...
    networks:
      - my_network

networks:
  my_network:
    driver: bridge
```
- 여러 컨테이너를 함께 관리하는 경우, Docker Compose를 사용하면 네트워크 설정을 보다 쉽게 구성할 수 있다.
- 모든 서비스가 my_network라는 사용자 정의 네트워크에 연결되어, 컨테이너 이름으로 서로 통신할 수 있다.

<br>

---
### 3. 이미 다른 네트워크에 있는 경우
``` shell
docker network connect fe_network be
docker network connect db_network be
```
- 각각의 네트워크를 연결

<br><br><br>