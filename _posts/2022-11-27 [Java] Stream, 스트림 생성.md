## 스트림이란?

스트림은 자바 8에서 추가된 기능으로 함수형 인터페이스인 람다를 활용할 수 있는 기술로 다양한 데이터 소스를 표준화된 방법으로 다루기 위한 것이다.

즉, 컬렉션과 배열을 스트림으로 만들면 이후 작업은 통일된다.



## 스트림의 특징

##### 스트림은 중간연산, 최종연산이 있는데 중간 연산은 0~n번 작업 가능, 최종 연산은 마지막에 0~1번 가능

#### 스트림은 데이터 소스로부터 데이터를 읽기만할 뿐 변경하지 않는다.

#### 스트림은 Iterator처럼 일회용이다. 필요하면 다시 생성해야 한다.

#### 최종 연산 전까지 중간연산이 수행되지 않는다. - 지연된 연산

```java
IntStream intStream = new Random().ints(1,46); // 1~45범위의 무한 스트림
intStream.distinct().limit(6).sorted() // 중간 연산 : 중복 제거.자르기.정렬
  .forEach(i->System.out.print(i+",")); //최종 연산
// 중간 연산으로 되어있는 게 바로 처리하는 게 아니라, 어떤 처리를 해야 하는지 표시만 한다. 이를 지연된 연산이라 한다.

```

#### 스트림은 작업을 내부 반복으로 처리한다.

```java
// 일반 포문
for(String str : strList){
  System.out.print(str);
}
// 스트림
stream.forEach(System.out::print);
// 내부 함수
void forEach(Consumer<? super T> action) {
  Object.requireNonNull(action); // 매개변수 널 체크
  for(T t : src){ // 내부 반복 (for문을 메서드 안으로 넣음)
		action.action(T);
	}
}
```

#### 스트림 작업을 병렬로 처리 - 병렬 스트림

```java
Stream<String> strStream = Stream.of("aa", "bb", "cc");
int sum = strStream.parallel() // 병렬 스트림으로 전환 (속성만 변경)
  .mapToInt(s -> s.length)).sum(); // 모든 문자열의 길이의 합
```

#### 기본형 스트림 - IntStream, longStream, DoubleStream

오토박싱&언박싱의 비효율이 제거됨(Stream<Integer> 대신 IntStream사용)

숫자와 관련된 유용한 메서드를 Stream<T>보다 더 많이 제공



## 스트림 생성

Collection인터페이스의 stream()으로 컬렉션을 스트림으로 변환

#### 컬렉션으로 생성

```java
List<String> list = List.of("aa", "bb");
Stream<String> stream = list.stream();
```

#### 배열로 생성

```java
String[] arr = new String[]{"aa", "bb"};
Stream<String> stream = Arrays.stream(arr);

Stream<String> specificStream = Arrays.stream(arr, 0, 1);
specificStream.forEach(System.out::println); // aa 출력
```

#### 기본 타입에 특화된 스트림 생성

```java
// 0, 1, 2
IntStream intStream = IntStream.range(0, 3);

// 0, 1, 2, 3
IntStream closedIntStream = IntStream.rangeClosed(0, 3);

// 0, 1, 2
LongStream longStream = LongStream.range(0, 3);

// 0.0, 0.3
DoubleStream doubleStream = DoubleStream.of(0, 3);
```

#### 임의의 수 (난수)

```java
IntStream intStream = new Random().ints() // 무한 스트림
  .limit(3); // 3개 제한
// 무한 스트림이라 개수 재한을 줘야한다.
IntStream intStream = new Random().ints(3, 5, 16) // 3개 재한 5 ~ 15 범위
```

#### Stream.iterate() 로 생성

`iterate` 메서드를 이용해 초기값과 람다를 인수로 받아 스트림 생성. 요청할 때마다 값을 생산할 수 있다.
무한 스트림을 사용해 만들기 때문에 `limit` 메서드로 크기를 제한해야 한다.

```java
// 0, 1, 2
Stream<Integer> stream = Stream.iterate(0, x -> x + 1).limit(3);
```

#### Stream.generate() 로 생성

생산된 각 값을 연속적으로 생산하지 않으며 인자가 없고 리턴값만 있는 `Supplier<T>`를 인수로 받는다.

무한 스트림을 사용해 만들기 때문에 `limit` 메서드로 크기를 제한해야 한다.

```java
// 1, 1, 1
Stream<Integer> stream = Stream.generate(() -> 1).limit(3);
```

#### 파일(Files)로 생성

`java.nio.Files` 클래스를 이용하여 스트림을 생성.

```java
Path path = Paths.get("~"); // 디렉토리 

Path filePath = Paths.get("~.txt"); // 파일
Stream<String> lines = Files.lines(path); // 라인 단위
```

#### 비어있는 스트림 생성

요소가 존재하지 않을 때 `null`과 같이 유효성 검사에서 사용할 수 있다.

```java
// 빈 스트림 생성
Stream<Object> empty = Stream.empty();
```

#### Stream.concat() 으로 스트림을 연결하여 생성

```java
List<String> list1 = List.of("aa", "bb");
List<String> list2 = List.of("cc", "dd");
Stream<String> stream = Stream.concat(list1.stream(), list2.stream());
// aa, bb, cc, dd
```



Reference:https://youtu.be/G2lPQB42GL8

