JPA를 적용하고 나서 Entity  생성 시 변수 명을 그대로 매핑 안하고 언더바 형식 카멜을(UserName => user_name) 으로 자동 매핑해준다. 



이 부분을 변수 명과 DB칼럼명을 그대로 매핑 하려면



application.properties 에 추가해주면 된다.

``` properties
spring.jpa.hibernate.naming.physical-strategy=org.hibernate.boot.model.naming.PhysicalNamingStrategyStandardImpl
```




application.yml 경우 

``` yaml
jpa:
    hibernate:
      ddl-auto: none
      naming:
        physical-strategy: org.hibernate.boot.model.naming.PhysicalNamingStrategyStandardImpl

```



