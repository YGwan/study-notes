# host.docker.internal

### Docker 내부에서 host의 ip를 알아야 하는 경우
- host.docker.internal 사용

### 사용 방법
docker-compose에서 localhost를 사용하는 컨테이너가 있을 때,

``` shell
extra_hosts:
- host.docker.internal:host-gateway
```

를 추가해주고, localhost -> host.docker.internal로 변경해서 사용