# nGrinder Tool

nGrinder란 네이버에서 진행한 오픈 소스 프로젝트로 서버의 부하 테스트를 위한 도구이다.

### 설치
- https://github.com/naver/ngrinder/releases 사이트에서 war 파일 설치

### 실행

``` shell
ngrinder 실행

java -Djava.io.tmpdir=/Users/yonggwan/ngrinder -jar ngrinder-controller-3.5.8.war --port=8300
```

### agent 설치
- http://localhost:8300/ 접근
- id : admin, pwd : admin 입력
- Download Agent 클릭
- 압축 해제
    ```shell
    tar -xvf ngrinder-agent-3.5.5-p1-localhost.tar 
    ```

### agent 실행
```shell
./run_agent.sh
```

### TIP
- controller가 실행된 상태에서 agent를 실행해 줘야한다.
- test를 하려면 agent가 켜져 있어야 한다. ( agent가 request를 보내기 때문에 )

### 용어
- TPS는 "Transactions Per Second"의 약자로 초당 처리가능한 트랜잭션의 수를 의미한다.
- Vuser는 "Virtual User"의 약자로, 가상 사용자를 의미한다.

### Report 용어
- TPS: 평균 TPS
- Peak TPS: 최고 TPS
- Mean Test Time: 평균 테스트 시간
- Executed Tests: 테스트 실행 횟수
- Successful Tests: 테스트 성공 횟수
- Errors: 에러 횟수
- Run time: 테스트 실행시간

### 테스트 정리
- TPS 수치가 높고 Mean Test Time이 낮을수록 성능이 좋다.
