```sql
ERROR 5084 --- [           main] com.zaxxer.hikari.pool.HikariPool        : HikariPool-1 - Exception during pool initialization.
```



이러한 오류가 나면 

application.properties 파일에

``` properties
spring.jpa.hibernate.ddl-auto = none
```

이 조건을 추가하면 된다.



이미 만들어진 테이블 생성하는데서 오류가 난듯하다.