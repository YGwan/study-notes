# 깃 Stash 명령어

## Stash 사용 상황
- 긴급 버그 핫픽스
  - 기능 개발 중인데, 갑자기 프로덕션 긴급 버그를 고쳐야 할 때
  - 현재 작업 중인 변경사항을 커밋하기엔 완성도가 낮거나 커밋 로그가 어수선해질 때

<br>

- 브랜치 전환 전 작업 보관
  - 다른 브랜치로 급히 이동해야 할 때, 워킹 디렉토리를 깨끗하게 정리하고 싶을 때

<br>

- 리베이스나 머지 전 준비
  - 안전하게 리베이스(rebase) 또는 머지(merge)하기 위해, 로컬 수정사항을 임시로 치워두고 충돌 최소화

<br>

## 사용 플로우
#### 1.	변경사항 임시 저장

``` shell
git stash

&

git stash push -m "메세지"

```

<br>

#### 2. 저장된 stash 목록 확인

``` shell
git stash list

// ex
% git stash list         
stash@{0}: WIP on test: test
stash@{1}: WIP on test: test
stash@{2}: WIP on test: test
stash@{3}: WIP on test: test

```

<br>

#### 3. 원하는 스태시 적용 (apply & pop)

``` shell
git stash apply stash@{0}

&

git stash pop stash@{0}
```
- apply (적용만, 스태시는 그대로 남김)
- pop (적용 + 자동 삭제)
- 충돌 발생 시 일반 머지 충돌 해결 절차대로 수정 후 커밋
<br>

#### 4. 스태시 삭제

``` shell
git stash drop stash@{0}

&

git stash clear
```
- drop : 별도로 하나씩 삭제
- clear : 전체 삭제

<br>

#### 5. 변경 사항 커밋

``` shell
git add .
git commit -m "메세지"

```

<br>