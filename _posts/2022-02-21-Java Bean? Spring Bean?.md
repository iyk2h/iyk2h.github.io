### Bean 이란

반복적으로 코드를 따로 작성하여 재사용하기 위해 만들어진 클래스

빈은 속성과 메서드로 이루어져 있으며, 데이터의 처리를 담당



## Java Bean의 정의

데이터를 표현하는 것을 목적으로 하는 자바 클래스( JavaBean 규격서에 따라 작성 )

컴포넌트와 비슷한 의미로도 사용한다.



DTO 혹은 VO의 형태가 Java Bean이라고 생각하면 쉽다.

 

Java Bean 필드는 private로 구성되어 getter와 setter를 통해서만 접근할 수 있고, 전달 인자가 없는 생성자를 가지는 형태의 클래스이다.

모든 필드는 private로 getter/setter를 통해서만 접근 가능하다.

```java
public class Bean_ClassName [ implements java.io.Serializable ] {
	private String fieldName;    //필드는 private 선언
  
	public Bean_ClassName() { }    // 전달 인자가 없는 생성자

	public String getName() {    // 필드 값을 읽어오는 메소드 
		return name; 
	}
	public void setName(String name) {    // 필드 값을 저장하는 메소드
		this.name = name;
	}
}
```



### Java Bean의 규격

- 클래스는 패키지화 하여야 한다.
- 멤버변수는 프로퍼티(Property)라 칭한다.
- 클래스는 필요에 따라 직렬화가 가능하다.
- 프로퍼티의 접근자는 private이다.
- 프로퍼티마다 getter/setter 가 존재해야 하며, 그 이름은 각각 get/set으로 시작해야 한다.
- 위의 프로퍼티 getter/setter 메서드의 접근자는 public이어야 한다.
- 외부에서 프로퍼티에 접근은 메서드를 통해서 접근한다.
- 프로퍼티는 반드시 읽기/쓰기가 가능해야 하지만, 읽기 전용인 경우 getter만 정의할 수 있다.
- getter의 경우 파라미터가 존재하지 않아야 하고, setter의 경우 한 개 이상의 파라미터가 존재한다.
- 프로퍼티의 형이 boolean일 경우 get 메서드 대신 is메서드를 사용해도 된다.



## Spring Bean

Spring에서 Bean은 스프링 IoC컨테이너가 관리하는 Java 객체를 뜻한다.

*스프링 IoC컨테이너가 관리하는 객체란 스프링에 의해 생성되고, 라이프 사이클을 수행하고, 의존성 주입이 일어나는 객체 즉, 스프링에게 제어권을 넘긴 객체(개발자 관리 x)

