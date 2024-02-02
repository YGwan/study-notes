# Seige Tools

### 설치 방법
```shell
brew install siege
```

### Site
https://formulae.brew.sh/formula/siege

### 설명
- HTTP regression testing and benchmarking utility
- 부하 테스트, 동시성 테스트 등을 할때 사용하면 용이

### Command
```shell
siege -c 200 -r 1 http://localhost:8080

# 200개의 Client가 1번 반복해서 http://localhost:8080에 요청을 보냄
```

### Options
- -c, --concurrent=X : 동시에 실행할 사용자 수를 지정합니다.
- -r, --reps=X : 각 사용자의 반복 횟수를 지정합니다.
- -t, --time=X : 테스트를 지정된 시간(초) 동안 실행합니다.
- -d, --delay=X : 각 요청 간의 지연 시간을 설정합니다 (초).
- -v, --verbose : 자세한 출력을 활성화합니다.
- -q, --quiet : 최소한의 출력으로 실행합니다.