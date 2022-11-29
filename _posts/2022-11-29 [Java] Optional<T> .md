T 타입 객체의 래퍼클래스 - Optional<T>

```java
public final class Optional<T> {
  private final T value; // T타입이 참조변수
  // T value는 모든 객체 저장 가능 NULL 포함
}
```

여기서 NULL 포함한 모든 객체 저장 가능한게 중요한 포인트다.

NULL을 직접 다룬다면 NullPonterException 발생할 위험이 크고, 조건문을통해서 NULL을 확인해야 하기 때문에 Optinal 객체를 사용한다.

Optinal는 객체기 때문에 주소를 가지고 있고, 그 주소가 가지고 있는 값이 NULL이기 때문에 NullPonterException 발생할 가능성이 없어진다.



NULL을 직접 다루지 않기 위해 String, arr 에서는 아래와 같이 사용된다.

```java
String str = ""; // (O)
String str = null; // (X)

int[] arr = new int[0]; // (O)
int[] arr = null; // (X)
```



### Optional<T> 객체 생성하기

```java
String str = "abc";
Optional<String> optVal = Optional.of(str);
Optional<String> optVal = Optional.of("abc");
Optional<String> optVal = Optional.of(null); // NullPonterException 발생 
Optional<String> optVal = Optional.ofNullable(null); // OK

// Optinal 초기화
Optional<String> optVal = Optional.empty(); // 빈 객체로 초기화
Optional<String> optVal = null; // 널로 초기화는 바람직하지 않다
```



### Optional<T> 객체의 값 가져오기

```java
Optional<String> optVal = Optional.of("abc");
String str1 = optVal.get(); // optVal의 value가 null이면 예외발생
String str2 = optVal.orElse(""); // optVal의 value가 null이면 "" 반환
String str3 = optVal.orElseGet(String::new); // 람다식 사용가능
String str4 = optVal.orElseThrow(NullPonterException::new); // 널이면 예외발생
```

#### isPresent()  - Optional객체의 값이 null이면 false, 아니면 true 반환

```java
// null이 아닐때만 작업해라
if(Optional.ofNullable(str).isPresent()) { // if(str!=null)
  System.out.println(str);
}
// 람다식
Optional.ofNullable(str).ifPresent(System.out::println);
// isPresent, ifPresent 비슷하지만 다름
```



### OptionalInt, OptionalLong, OptionalDouble

성능을 올릴려고 기본형 값을 감싸는 래퍼클래스

```java
public final class OptionalInt {
  prvate final boolean isPresent; // 값이 저장되어 있으면 true
  prvate final int value; // int타입의 변수
}
```

| Optional클래스 | 값을 반환하는 메서드 |
| -------------- | -------------------- |
| Optional<T>    | T get()              |
| OptionalInt    | int getAsInt()       |
| OptionalLong   | long getAsLong()     |
| OptionalDouble | double getAsDouble() |

```java
OptionalInt opt = OptionalInt.of(0); //OptionalInt에 0을 저장
OptionalInt opt2 = OptionalInt.empty(); //OptionalInt에 0을 저장

System.out.println(opt.isPresent()); // true
System.out.println(opt2.isPresent()); // false

System.out.println(opt.equls(opt2)); // false
// isPresent값과 value 값이 같아야지 같은 값으로 취급한다
```











