# Dockerfile
- docker 이미지를 작성할때 주로 사용
- 이미지는 스크립트 기반인데, dokerfile 문법으로 이루어져 이를 기반으로 이미지를 생성함
- 

``` shell
FROM : 베이스 이미지 지정

RUN : 쉘 명령어 실행. 이미지 생성시 일종의 layer를 만들 수 있는 단계로, 보통 베이스 이미지에 패키지(프로그램)을 추가로 설치하여 새로운 이미지를 만들 때 사용한다.

CMD : 컨테이너가 실행되고 가장 처음 실행될 명령어. 하나의 Dockerfile에서 한가지만 설정됨

EXPOSE : 오픈되는 포트 설정

ENV : 환경 변수 설정

ADD : 파일 또는 디렉토리 추가

COPY : 파일 또는 디렉토리 추가

VOLUME : 외부 마운트 포인트 생성

WORKDIR : 작업 디렉토리 설정

ARGS : 빌드 시점에서만 사용되는 환경 변수 설정

USER : RUN, CMD, ENTRYPOINT를 실행하는 사용자

LABEL : key-value 데이터 형식으로 메타 데이터를 넣을 수 있는 기능.

```