### 변수 설정

```

[변수명]=["실제값"]

CONTAINER_NAME="anime-kr"

```

<br>

## 값 비교

- 모든 컨테이너의 ID를 표시하고, 그 중에서 지정된 이름과 일치하는 컨테이너만 필터링하여 표시
- docker ps -aq -f name="원하는 이름 변수"

<br>

### ※ anime-kr의 이름을 포함한 컨테이너들을 필터링하여 표시

```

docker ps -aq -f name="anime-kr"

```

<br>

### ※ anime-kr 단어만을 가진 컨테이너를 필터링하여 표시

```
docker ps -aq -f name="^anime-kr$"
```
