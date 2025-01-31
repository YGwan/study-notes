# Ubuntu EC2에 스프링 프로젝트 배포

<br>

## 가정

<br>

- ### 프로젝트 코드는 github에 올라가있고 public으로 열려있다고 가정
- ### ubuntu EC2에는 기본적으로 git이 설치되어있다고 가정
- ### spring 환경 변수는 없다고 가정
- ### java 버전은 11버전을 사용한다고 가정

<br>

## 명령어 순서

1. 시스템 목록 최신 상태로 유지

``` shell
sudo apt update
```

<br>

2. project에서 사용하는 버전에 맞는 java 설치

``` shell
sudo apt install openjdk-11-jdk
```

<br>

3. java 버전 확인

``` shell
java -version
```

<br>

4. git clone 진행

``` shell
git clone {git repository 주소}
```
- public으로 레포지토리가 공개되어있기 때문에 github 계정과 비밀번호를 입력할 필요가 없음

<br>

5. 서버 배포 진행

``` shell
cd {프로젝트 경로}
sudo chmod 777 ./gradlew
./gradlew clean build
cd build/libs
nohup java -jar {.jar 파일} &
```
- 이때 "-SNAPSHOT-plain.jar" 이 아닌 "-SNAPSHOT.jar" 파일을 사용해야한다.

<br>

5. 백그라운드 상태에서 배포 로그 확인

``` shell
tail -f nohup.out
```
- nohup.out 파일은 위의 nohup 명령어를 실행한 파일 경로에 생성된다.

<br>

``` text

위의 명령어를 실행하면, 서버 배포가 완료됨
EC2 서버의 public IP를 확인하고, 인바운드 / 아웃바운드 규칙을 적용하여 외부에서 해당 서버에 접근이 가능하도록 설정할 수 있다.

```

<br>

---

## 번외

### 1. 배포할 서버 코드가 private 레포지토리로 github에 올라가 있는 경우

- git clone & pull 할때마다, github의 아이디와 패스워드(토큰 값)이 필요하다.
- 이는 매번 클론할때마다 github의 아이디와 패스워드를 입력해야 하기 때문에 번거롭고, CI/CD를 적용할때도 번거롭다.
- 해결방법

``` shell
git config --global credential.helper store
git pull origin main
# github 계정 및 비밀번호 입력
```
- 이후에 git clone & pull 시 github 계정 및 비밀번호를 입력하지 않아도됨
- ~/.git-credentials에 로그인 정보를 저장해둠
- but EC2에 접근 가능한 사용자들이 내 github 정보(아이디, 토큰 값)을 볼수 있다는 단점 존재

<br>

### 2. 환경 변수가 있는 경우
- 서버의 주요 데이터를 환경변수로 관리하는 경우 이를 EC2 인스턴스에 설정해줘야한다.
- ex) yml & properties 파일에서 ${변수명} 으로 값이 설정되어 있는 경우

<br>

### EC2에 환경변수 설정 방법

1. .bashrc 파일 열기 (home/ubuntu 경로에 존재)

``` shell
vi ~/.bashrc
```

<br>

2. .bashrc 파일 젤 아래에 환경 변수 값 추가 및 저장

``` shell
export {환경변수명}={값}
```

<br>

3. 환경 변수 적용

``` shell
source .bashrc
```

<br>

#### 그 후 코드를 클론 받고 서버를 실행시키는 위의 과정을 동일하게 진행하면 된다.

<br>

### .jar 배포 전용 shell 파일
``` shell
#!/bin/bash

# 스크립트 실행 중 오류 발생 시 중지
set -e

# 프로젝트 빌드
echo "🚀 Building the project..."
./gradlew clean build -x test

# JAR 파일 디렉터리로 이동
echo "📂 Moving to build/libs directory..."
cd build/libs/

# 기존 프로세스 종료 (선택 사항)
echo "🛑 Stopping any existing application..."
pkill -f '*.jar' || true

# JAR 파일 실행
echo "🚦 Starting the application..."
nohup java -jar *.jar > app.log 2>&1 &

echo "✅ Application started successfully!"
```
