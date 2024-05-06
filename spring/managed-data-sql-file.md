# data.sql 관리

<br>

### data.sql 경로 커스텀
- 기본 경로는 resource 하위의 application.yml (경로 설정을 따로 안해도 됨)
- 커스텀 방법 - ex) resource 하위의 sql 파일 안 data.sql 파일
    ``` properties
    spring.sql.init.data-locations=classpath:sql/data.sql
    ```

<br>

### data.sql 활성화 방법
``` properties
spring.sql.init.mode=always
```
<br>

### data.sql 무효화하는 방법
``` properties
spring.sql.init.mode=never
```
