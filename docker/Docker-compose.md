### docker-compose command

``` shell

# 실행
docker-compose up

# 정지된 컨테이너 재개
docker-compose start

# 컨테이너 재시작
docker-compose restart

# 컨테이너 정지
docker-compose stop

# 종료
docker-compose down

# 컨테이너 로그 확인
docker-compose logs

# 컨테이너 목록 확인
docker-compose ps

# 실행중인 컨테이너 접근
docker-compose exec

# 컨테이너 build
docker0-compose build
```

<br>

---

## docker-compose.yml file's grammar

<br>

### 실행할 컨테이너 정의

``` yaml
# docker run --name <name> 

services:
  <CONTAINER_NAME>: 
    ...
```

<br>

### 컨테이너에 사용할 이미지 이름과 태그 설정

``` yaml
servives:
  <CONTAINER_NAME>:
    image: <image_name:tag>
    ...
```

<br>

### 컨테이너와 연결할 포트 설정

``` yaml
servives:
  <CONTAINER_NAME>:
    ...
    ports:
      - "<HOST_PORT:CONTAINER_PORT>"
    ...
```

<br>

### 컨테이너에 사용할 환경변수

``` yaml
servives:
  <CONTAINER_NAME>:
    ...
    environment:
      - <ENVIRONMENT_NAME=ENVIRONMENT_VALUE>
      ...
    ...
```

<br>

### 연결할(마운트할) 파일들

``` yaml
services:
  <CONTAINER_NAME>:
    ...
    volumes:
      -<HOST_DIRECTORY:CONTAINER_DIRECTORY>
    ...
```

<br>

### 재시작 정책 설정

``` yaml
servives:
  <CONTAINER_NAME>:
    ...
    restart: <POLICY>
    ...

# POLICY
no, always, on-failure, unless-stopped
```

<br>

### 이미지 빌드

``` yaml
servives:
  <CONTAINER_NAME>:
    ...
    build:
      context: <dir Docker file>
      dockerfile : <build docker file name>
    ...
```