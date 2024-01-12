### Docker OPTIONS

``` shell
-d : 백그라운드 모드로 실행
-p : 호스트와 컨테이너의 포트 연결
-v : 호스트와 컨테이너의 디렉토리 연결
-e : 컨테이너 내의 사용할 환경변수 설정
--name : 컨테이너 이름 설정
-- rm : 프로세스 종료시 컨테이너 자동 제거
-- it : 컨테이너를 종료하지 않은체로, 터미널의 입력을 계속해서 컨테이너로 전달
-- network : 네트워크 연결
```

### 컨테이너 실행

``` shell
# 컨테이너 실행
docker run <OPTIONS> IMAGE:TAG <COMMAND>


# 실행 중인 도커 컨테이너에 접속
docker exec <CONTAINER ID OR NAME> <COMMAND>
```

### 컨테이너 & 이미지 목록 확인

``` shell
# 실행중인 컨테이너 목록만 확인
docker ps

# 실행 + 중지된 컨테이너 목록 확인
docker ps -a

# 다운로드한 이미지 목록 확인
docke images <OPTIONS>

# 이미지 다운로드
docker pull <OPTIONS> <IMAGE_NAME:TAG>
```

### 컨테이너 중지

``` shell
docker stop <OPTIONS> <CONTAINER_ID OR CONTAINER_NAME ...>
```

### 컨테이너 & 이미지제거

``` shell
# 컨테이너 제거
docker rm <OPTIONS> <CONTAINER_ID OR CONTAINER_NAME ...>

# 이미지 제거
docker rmi <OPTIONS> <IMAGE_ID OR IMAGE_NAME ...>
```

### 컨테이너 로그 확인

``` shell
docker logs <OPTIONS> <CONTAINER_ID OR CONTAINER_NAME>

-f : 실시간으로 로그를 출력
-tail : 출력할 로그의 라인 수 지정
```

### 가상 네트워크 생성 및 연결

``` shell
# 가상 네트워크 생성
docker network create <OPTIONS> <NETWORK_NAME>

# 컨테이너에 네트워크 추가

docker network connect <NETWORK_NAME> <CONTAINER_NAME>
```

### 