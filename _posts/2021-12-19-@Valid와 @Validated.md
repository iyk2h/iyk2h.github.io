

## **@Valid와 @Validated**

실무에서 컨트롤러 @ModelAttribute 모델에 바인딩하는 데 사용
해당 인터페이스는 두 개의 메세드로 구성
그리고 @Validated는 @Valid의 기능을 포함

```java
@Validated // 어노테이션
 
@Service
public class testService {
	public void Contact(@Valid Test test) {
	}
}
```

```java
@RequestMapping("/controller")
public Model testController(@Validated Test test) throws Exception {
}
```



### @Validated를 이용한 유효성 검증

요청 파라미터의 유효성 검증은 컨트롤러에서 처리하고 서비스나 레포지토리 계층에서는 유효성 검증을 하지 않는 것이 바람직

Spring에서는 이런 서비스 계층 등에서 파라미터를 검증해야 할 경우를 위해 인터셉터 기반으로 메소드의 요청을 가로채서 유효성 검증을 진행 할 수 있는 @Validated를 제공 @Validated는 Spring 프레임워크에서 제공하는 어노테이션

@Validated를 다음과 같이 클래스 레벨에 선언하면 해당 클래스에 유효성 검증을 위한 인터셉터(MethodValidationInterceptor) 등록 그리고 해당 클래스의 메소드들이 호출될 때 AOP의 포인트 컷으로써 인터셉터를 통해 유효성 검증이 진행

이를 통해 컨트롤러, 서비스, 레포지토리 등 계층에 무관하게 스프링 유효성 검증을 진행할 수 있다. (진행될 메소드에는 @Valid를 선언되어야 한다.)