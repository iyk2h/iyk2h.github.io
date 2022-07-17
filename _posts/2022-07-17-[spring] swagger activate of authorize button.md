api 서버 구현 중에 JWT 토큰 인증 방식으로 구현하면 헤더에 JWT 토큰을 받아서 유효한지 검사하게 된다.

swagger 를 활용해 api 문서 작성과 테스트를 하기 위해 swagger 에 헤드에 값을 넣는 방법을 알아보자.



build.gradle 설정

``` 
implementation group: 'io.springfox', name: 'springfox-boot-starter', version: '3.0.0'
implementation group: 'io.springfox', name: 'springfox-swagger-ui', version: '3.0.0'
```



SwaggerConfig 설정

```
@Configuration
@RequiredArgsConstructor
public class SwaggerConfigV3 {
    @Bean
    public Docket api() {
        return new Docket(DocumentationType.OAS_30)
                .useDefaultResponseMessages(false)
                .securityContexts(Arrays.asList(securityContext()))
                .securitySchemes(Arrays.asList(apiKey()))
                .select()
                .apis(RequestHandlerSelectors.basePackage("/controller")) //" " 여기엔 패키지 경로 입력
                .paths(PathSelectors.any())
                .build()
                ;
    }

    private List<SecurityReference> defaultAuth() {
        AuthorizationScope authorizationScope = new AuthorizationScope("global", "accessEverything");
        AuthorizationScope[] authorizationScopes = new AuthorizationScope[1];
        authorizationScopes[0] = authorizationScope;
        return Arrays.asList(new SecurityReference("Authorization", authorizationScopes));
    }
    
    private SecurityContext securityContext() {
        return SecurityContext.builder()
            .securityReferences(defaultAuth())
            .build();
    }
    
    private ApiKey apiKey() {
        return new ApiKey("Authorization", "Authorization", "header");
    }
}
```



설정 완료 후



![image-20220717201733995](../images/image-20220717201733995.png)



Authorize 버튼이 생긴다.

![image-20220717204223684](../images/image-20220717204223684.png)

벨류 빈칸에

![image-20220717204238551](../images/image-20220717204238551.png)

JWT 값을 넣어서 Authorize 클릭



그럼

```
curl -X GET "http://localhost:8000/oauth/me" -H "accept: application/json" -H "Authorization: Bearer e0eXAJKV1QiJhbGciOJIUzU.eIiOiJodGwwMY29tIiwibmlja25hbWUiOiLsoJXsmrDshJ0iLCJpCI6MjQ2MxOTg1MyiZXhwIjxNjY1.1nZGGUYhDO6KKtF8BgikOWdyrqtBQuBz9NagjWIW3KlBIaaIGipdTB95AOhUfzvd"
```



이런 식으로 Header 에 값이 잘 들어가게 된다.



만약 Bearer 앞에 값을 Authorization : 값을 JWT로 바꾸고 싶으면 아래와같이 수정하면 된다.

```
    private List<SecurityReference> defaultAuth() {
        AuthorizationScope authorizationScope = new AuthorizationScope("global", "accessEverything");
        AuthorizationScope[] authorizationScopes = new AuthorizationScope[1];
        authorizationScopes[0] = authorizationScope;
        return Arrays.asList(new SecurityReference("JWT", authorizationScopes));
    }
    
        private ApiKey apiKey() {
        return new ApiKey("JWT", "Authorization", "header");
    }
```

```
url -X GET "http://localhost:8000/oauth/me" -H "accept: application/json" -H "JWT: Bearer e0eXAJKV1QiJhbGciOJIUzU.eIiOiJodGwwMY29tIiwibmlja25hbWUiOiLsoJXsmrDshJ0iLCJpCI6MjQ2MxOTg1MyiZXhwIjxNjY1.1nZGGUYhDO6KKtF8BgikOWdyrqtBQuBz9NagjWIW3KlBIaaIGipdTB95AOhUfzvd"
```

