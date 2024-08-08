# 깃 repository 옮기기
- git 저장소(repository)를 커밋로그 포함, 그대로 옮기는 방법

#### 1. 원본 저장소를 복사한다.

``` shell
git clone --mirror [원본 저장소 경로] <또는 이름>
```

<br>

#### 2. 클론한 디렉토리 안으로 이동

``` shell
cd [원본 저장소 이름].git
```

<br>

#### 3. 새로 이동할 원격 저장소(B) 경로 지정

``` shell
git remote set-url --push origin [이동할 원격 저장소]
```

<br>

#### 4. 새 원격 저장소로 push

``` shell
git push --mirror
```
