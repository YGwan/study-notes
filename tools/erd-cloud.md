### ERDCloud 광고 배너 제거 명령어

<br>

1. 크롬 개발자 도구 실행

2. Console 접근

3. 아래 명령어 실행

``` javascript
allow pasting

document.querySelector(".erd-ads-area").style.display = "none";
document.querySelector(".erd-container").style.width = "100%";
```
