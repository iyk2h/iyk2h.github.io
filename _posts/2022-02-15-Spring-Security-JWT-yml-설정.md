``` yml
server:
  port: 8080
  servlet:
    context-path: /
    encoding:
      charset: UTF-8
      enabled: true
      force: true
      
spring:
  datasource:
    driver-class-name: org.postgresql.Driver
    url: jdbc:postgresql://127.0.0.1:5432/security
    username: dbmsUserName #본인에게 맞는 아이디, 비밀번호 입력하세요
    password: **** 
    
  mvc:
    view:
      prefix: /templates/
      suffix: .mustache

  jpa:
    hibernate:
      ddl-auto: update #create update none
      naming:
        physical-strategy: org.hibernate.boot.model.naming.PhysicalNamingStrategyStandardImpl
    show-sql: true
    database: postgresql
    database-platform: org.hibernate.dialect.PostgreSQLDialect
```

