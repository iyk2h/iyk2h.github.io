## devtools 라이브러리 의존성 추가

### maven

```xml
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-devtools</artifactId>
    <version>2.0.4.RELEASE</version>
</dependency>
```

### Gradle

```apl
compile group: 'org.springframework.boot', name: 'spring-boot-devtools', version: '2.0.4.RELEASE'
```



## application 옵션 추가

### **application.yml**

``` yaml
spring:
  devtools: 
    livereload:
      enabled: true
  freemarker:
    cache: false
  thymeleaf:
    cache: false
```

### **application.properties**

``` properties
spring.devtools.livereload.enabled=true
spring.freemarker.cache=false
spring.thymeleaf.cache=false
```



#### 소스 변경 후 저장 -> 새로고침 -> 변경 사항 적용

