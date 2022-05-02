개발 환경

```
SpringBoot 2.6.1
gradle
Swagger 3.0.0
```



의존성 추가

```
/* build.gradle */

dependencies {
    // ..
    implementation 'io.springfox:springfox-boot-starter:3.0.0'
    // ..
}
```

Seagger 3.x 부터 `pringfox-boot-starter` 하나로 하위에 필요한 모든 라이브러리가 포함된다.



Config 추가

```
@Configuration
public class SwaggerConfig {

    @Bean
    public Docket api() {
        return new Docket(DocumentationType.OAS_30)
                .useDefaultResponseMessages(false)
                .select()
                .apis(RequestHandlerSelectors.basePackage("com.example.beamo.controller")) //@@@@자신의 Controller 위치 @@@@
                .paths(PathSelectors.any())
                .build()
                .apiInfo(apiInfo());
    }

    private ApiInfo apiInfo() {
        return new ApiInfoBuilder()
                .title("Practice Swagger")
                .description("practice swagger config")
                .version("1.0")
                .build();
    }
}
```



접속

- Swagger3: http://localhost:8080/swagger-ui/index.html



접속이 안되면

여기 [블로그](https://jackyee.tistory.com/24) 참고


