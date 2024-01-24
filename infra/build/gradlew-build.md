### error : zsh: ./gradlew: bad interpreter: /bin/sh^M: no such file or directory

<br>

```
원인 : gradlew 파일이 Window 환경에서 sh 작성 후, 다른 환경에서 실행하여 발생한 문제이다. 

해결 방법: gradlew 파일의 윗줄을 #!/usr/bin/env sh 로 변경
```