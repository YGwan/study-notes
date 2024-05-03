# Entity 중 공통 속성 값이 있을 경우 관리 방법

### EX : 생성 시간 & 업데이트 시간 관리 base-entity 설정

<br>

#### 1. base-entity 생성

``` java
@Getter
@MappedSuperclass
@EntityListeners(AuditingEntityListener.class)
public abstract class BaseEntity {

    @CreatedDate
    private LocalDateTime createdTime;

    @LastModifiedDate
    private LocalDateTime updatedTime;
}

```
- @MappedSuperclass : 이 어노테이션이 적용된 클래스의 속성과 매핑 정보가 하위 엔티티 클래스에 상속됨 (공통 매핑 정보를 정의하기 위해 사용되는 어노테이션)
- @EntityListeners(AuditingEntityListener.class) : 해당 엔티티의 생명주기 이벤트를 모니터링 & AuditingEntityListener에서 정의된 동작을 수행하도록 지시
- AuditingEntityListener.class는 주로 데이터베이스의 변화를 추적하고, 예를 들어 생성일자와 수정일자를 자동으로 관리하기 위해 사용됨

<br>

#### 2. 스프링에 적용

``` java
@EnableJpaAuditing
@Configuration
public class JpaConfig {

}
```
@EnableJpaAuditing
- spring-data-jpa 의존성에 포함되어 있는 어노테이션
- 엔티티 객체가 생성되거나 변경되었을때 자동으로 값 설정
