DTO를 사용해 값을 입출력하는데 에러가 뜬다.



에러 내용은

Cannot construct instance of ` XXXDto` (no Creators, like default constructor, exist): cannot deserialize from Object value (no delegate- or property-based Creator)



문제 원인은 DTO를 재구성하는데 생성자가 없기 때문이다.



기존에 DTO는 Builder 로만 객체를 생성했었다.

```java
@Getter
@Builder
public class XXXDto {
	//	~~~
}
```



오류를 해결하기 위해 @AllArgsConstructor, @NoArgsConstructor 를 추가해줘야한다.

```java
@Getter
@Builder
@AllArgsConstructor
@NoArgsConstructor
public class XXXDto {
	//	~~~
}
```

이유는

`@AllArgsConstructor` 어노테이션은 모든 필드 값을 파라미터로 받는 생성자를 만들어주고,`@NoArgsConstructor` 어노테이션은 파라미터가 없는 기본 생성자를 생성해준다.