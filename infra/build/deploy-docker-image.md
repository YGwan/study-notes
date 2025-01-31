# Ubuntu에 docker image 생성 후 서버 배포

<br>

### 1. 서버 포트가 열려 있는지 확인
``` shell
sudo ufw status
```

``` text
To                         Action      From
--                         ------      ----
8304/tcp                   ALLOW       Anywhere                  
22                         ALLOW       Anywhere
...
```
- 위와 같이 열려 있는 포트 목록이 띄워진다.

<br>

### 2. 서버 포트 열기
``` shell
sudo ufw allow {포트 번호}
```
- 그 후 다시 sudo ufw status을 하면 허용한 포트 번호가 ALLOW, Anywhere로 설정되어 있는 것을 확인할 수 있다.

<br>

### 3. Springboot 프로젝트 빌드하기
``` shell
./gradlew clean bootJar 
```
- 빌드하면, build/libs/ 폴더에 .jar 파일이 생성된다.

<br>

### 4. Dockerfile 생성
``` dockerfile
# Use Amazon Corretto 21 Alpine as the base image
FROM openjdk:21-slim

# Define where the application will reside
WORKDIR /app

# Define an argument for the dependency path
ARG DEPENDENCY=build/libs

# Copy the necessary files from the dependency directory
COPY ${DEPENDENCY}/*.jar app.jar

# Expose the application port (adjust if different)
EXPOSE 8081

# Define the entry point to run the application
ENTRYPOINT ["java", "-jar", "app.jar"]
```
- Springboot 서버를 실행할 수 있는 Dockerfile 생성

<br>

### 5. Dockerfile을 사용한 Docker 이미지 빌드
``` shell
docker build -t {이미지 명} .
```

<br>

### 6. Docker container 실행
``` shell
docker run -p {로컬 포트}:{컨테이너 내 포트} {컨테이너 명}
```

<br>

### 이미지 관리 (선택 사항)
- 만약 서버 이미지를 다른 곳에서도 사용한다고 하면, 이를 Docker Hub & Github GHCR & AWS 등을 사용해 관리할 수 있다.