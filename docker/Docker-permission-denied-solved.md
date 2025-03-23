# Docker permission denied 문제 해결
> permission denied while trying to connect to the Docker daemon socket at unix:///var/run/docker.sock: 
> Get "http://%2Fvar%2Frun%2Fdocker.sock/v1.48/containers/json": dial unix /var/run/docker.sock: connect: permission denied
- docker 다운로드 후 실행시 위와 같은 에러 발생
- sudo로 접근하면 기본적으로 해결되지만, 근본적인 이유는 X

<br>

## 해결 방법
- 현재 유저를 docker에 추가한다.

### 1. Docker 그룹 확인
```bash
getent group docker
```

<br>

### 2. 비어잇으면 그룹 생성
```bash
sudo groupadd docker
```

<br>

### 3. 현재 사용자 Docker 그룹에 추가
```bash
sudo usermod -aG docker $USER
```
- $USER는 현재 로그인한 사용자 이름을 자동으로 가져옴

<br>

### 4. 확인
```bash
sudo groups $USER
```

<br>

### 5. 변경 사항 적용
```bash
newgrp docker
```

<br>

### 6. docker 서비스 재시작
```bash
sudo systemctl restart docker
sudo systemctl status docker
```

<br><br><br>
