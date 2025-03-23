# Tmux란
- tmux는 터미널 멀티플렉서(Terminal Multiplexer)로, 하나의 터미널 안에서 여러 세션, 창, 패널을 동시에 사용할 수 있게 해주는 매우 강력한 도구이다.
- 사용자가 단일 단말기 창 또는 원격 터미널 세션 안에서 여러 별도의 터미널 세션에 액세스할 수 있도록 여러 가상 콘솔을 다중화하는데 사용할 수 있는 응용 소프트웨어이다.

<br>

### Tmux 주요 개념
- Session : 독립된 터미널 작업 공간
- Window : 세션 내 탭처럼 작동하는 화면
- Panes : 동일한 윈도우에서 분리된 부분

<br>

### Tmux 주요 명령어
- Window & Panes도 있지만, 기본적으로 사용하는 세션을 기반으로 명령어를 정리

<br>

### tmux 시작 & 종료
``` shell
- tmux : 새 세션 시작
- tmux new -s [세션명] : 이름 있는 새 세션 시작
- exit : 현재 패널 종료
- tumx kill-session -t [세션명] : 특정 세션 종료
- tmux kill-server : 모든 세션 종료
```

<br>

### 세션
``` shell
- tmux ls : 실행 중인 세션 목록 보기
- tmux attach -t [세션명] : 특정 세션에 붙기
- tmux detach & <Control+b d> : 특정 세션에서 빠져나오기 (detach) 
```

<br><br><br>