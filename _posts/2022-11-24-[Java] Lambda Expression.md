함수와 메서드 차이

함수는 클래스에 독립적, 메서드는 클래스에 종속적



java : oop 언어 + 함수형(fp) 언어



람다식이란 ( Lambda Expression)

함수를 간단한 식으로 표현하는 방법

```java
// function
int max (int a, int b) {
  return a > b ? a: b;
}
```

```java
// lambda
(a, b) -> a > b ? a : b
```



### 람다식 작성하기

1. 메서드 이름과 반환 타입을 제거하고 -> 를 불록 {} 앞에 추가한다.

// 익명 함수로 사용 사실은 익명 객체!

~~int max~~ (int a, int b) -> {
  return a > b ? a: b;
}

2. 반환값이 있는 경우, 식이나 값만 적고 return문 생략 가능! + 끝에 ; 안 붙인다.
	1. 블록{} 안의 문장이 하나뿐 일 때 괄호 생략 가능

(int a, int b) -> a > b ? a: b

3. 매개변수의 타입이 추론 가능하면 생략 가능하다. (대부분 생략 가능)

(a, b) -> a > b ? a: b

### 람다식 작성 주의 사항

1. 매개변수가 하나인 경우 () 생략 가능

a -> a + a (O)

(int a) -> a + a   =>  int a -> a + a (X)



### 람다식은 익명 함수가 아닌 <u>익명 객체다</u>

(a, b) -> a > b ? a: b 

==

```java
new Object() {
  int max(int a, int b){
    return a > b ? a: b ;
  }
}
```

결국 람다식은 객체이다. 이유는 자바 특성상 메서드만 존재할 수 없기때문에 객체 안에 있어야한다.

```java
Object obj = new Object() {
  int max(int a, int b){
    return a > b ? a: b ;
  }
};
```



하지만
obj.max(1,4) //이렇게 호출은 불가하다.

obj.max(1,4) 이렇게 사용하려면 함수형 인터페이스가 필요하다.



### 함수형 인터페이스

단 하나의 추상 메서드만 선언된 인터페이스

함수형 인터페이스 작성시 매개변수와 반환 타입이 맞아야한다.

@FunctionalInterface 를 붙여주는 게 좋다. 2개의 추상 메서드를 가지면 에러를 띄워준다.

```java
//<< interface >>
@FunctionalInterface
interface myFunction {
  public abstract int max(int a, int b);
}
```

```java
MyFuntion f = new MyFuntion() {
  public int max(int a, int b) {
    return a > b ? a : b;
  }
};
```

```java
int value = f.max(3, 5); // 사용 가능 MyFuntion에 max()가 있음
```

위 식을 람다식으로 표현하면

```java
MyFuntion f = (a, b) -> a > b ? a : b;
int value = f.max(3, 5); // 실제로는 람다식이 호출된다.
```



### 함수형 인터페이스 타입의 매개변수, 반환타입

#### 함수현 인터페이스 타입의 매개변수

```java
void aMethod(MyFuntion f) {
  f.myMethod(); // MyFuntion에 정의된 메서드 호출
}
```

```java
MyFuntion f = () -> System.out.println("myMethod()");
aMethod(f);
```

```java
// 위 두 문장을 합친 것
// f 대신에 람다식을 바로 넣음
aMethod( () -> System.out.println("myMethod()"))
```

#### 함수형 인터페이스 타입의 반환 타입

```java
// MyFuntion는 함수형 인터페이스
MyFuntion myFuntion() {
  MyFuntion f = () ->{};
  return f;
}
// 두 문장을 합치면
MyFuntion myFuntion() {
  return () ->{};
}
```



### java.util.function 패키지

- 자주 사용되는 다양한 함수형 인터페이스를 제공해준다.

#### 기본형 함수형 인터페이스

가장 기본이 되는 함수형 인터페이스, 매개변수가 없거나 하나인 경우

| **FuntionalInterface** | **method**        | **설명**                 |
| ---------------------- | ----------------- | ------------------------ |
| java.lang.Runnalbe     | void run()        | 매개변수, 반환 모두 없음 |
| (공급자) Supplier<T>   | T get()           | 매개변수 없음, 반환 T    |
| (소비자) Comsumer<T>   | void accept(T t)  | 매개변수 T, 반환 없음    |
| (함수) Function<T, R>  | R apply(T t)      | 매개변수 T, 반환 R       |
| (조건식) Predicate<T>  | boolean test(T t) | 매개변수 T, 반환 boolean |

```java
Predicate<String> isEmptyStr = s -> s.Length() == 0;
String s = "";

if(isEmptyStr.test(s)) // == if(s.length() == 0)
  System.out.println("This is empty");
```

#### 매개변수가 2개인 함수형 인터페이스

매개변수가 2개인 인터페이스

| **FuntionalInterface** | **method**             | **설명**                   |
| ---------------------- | ---------------------- | -------------------------- |
| BiComsumer<T, U>       | void accept(T t, U u)  | 매개변수 2개, 반환 없음    |
| BiPredicate<T, U>      | boolean test(T t, U u) | 매개변수 2개, 반환 boolean |
| BiFunction<T, U, R>    | R apply(T t, U u)      | 매개변수 2개, 반환 R       |

매개변수가 3개는 제공되지 않음. 필요하면 만들어서 사용하면 된다.

#### 입력과 반환이 같은 타입인 함수형 인터페이스

| **FuntionalInterface**           | **method**        | **설명**                                |
| -------------------------------- | ----------------- | --------------------------------------- |
| (단항 연산자) UnaryOperation<T>  | T apply(T t)      | 매개변수 1개, 매개변수와 같은 타입 반환 |
| (이항 연산자) BinaryOperation<T> | T apply(T t, T t) | 매개변수 2개, 매개변수와 같은 타입 반환 |



### Predicate의 결합

and(), or(), negate()로 두 Predicate를 하나로 결합(default메서드, Static 메서드, 추상 메서드)

```java
Predicate<Integer> p = i -> i < 100;
Predicate<Integer> q = i -> i < 200;
Predicate<Integer> r = i -> i%2 == 100;
Predicate<Integer> notP = p.negate(); // i >= 100
Predicate<Integer> all = i -> notP.and(q).or(r); // 100<=i && i<200 || i%2==0
Predicate<Integer> all2 = i -> notP.and(q.or(r)); // 100<=i && ( i<200 || i%2==0 )
System.out.println(all.test(2)); //true
System.out.println(all2.test(2)); //false
System.out.println(all.test(2)); //true
System.out.println(all2.test(2)); //false
```

등가비교를 위한 Predicate의 작성에는 isEqual()를 사용한다.(static메소드)

```java
Predicate<String> p = Predicate.isEqual(str1);
Boolean result = p.test(str2) // str1과 str2가 같은지 비교한 결과를 반환
// 위 두 문장을 합친 것
boolean result = Predicate.isEqual(str1).test(str2);
```



### CollectionFramework 함수형 인터페이스

| **인터페이스** | **메서드**                                     | **설명**                         |
| -------------- | ---------------------------------------------- | -------------------------------- |
| Collection     | boolean removeif(Predicate<E> filter)          | 조건에 맞는 요소를 삭제          |
| List           | void replaceAll(UnaryOperator<E> opertator)    | 모든 요소를 반환 값으로 대체     |
| Iterable       | void forEach(Consumer<T> action)               | 모든 요소를 순회하여 action 수행 |
| Map            | V compute(K key, BiFunction<K,V,V> f)          | 지정된 키의 값에 작업 f 수행     |
|                | V computeIfAbsent(K key, Function<K,V> f)      | 키가 없으면, 작업 f수행 후 추가  |
|                | V computeIfPresent(K key, BiFunction<K,V,V> f) | 지정된 키가 있을 때, 작업 f 수행 |
|                | V merge(K key, V value, BiFunction<V,V,V> f)   | 모든 요소에 병합작업 f 수행      |
|                | void forEach(BiConsumer<K,V> action)           | 모든 요소에 작업 action 수행     |
|                | void replaceAll(BiFunction<K,V,V> f)           | 모든 요소에 치환작업 f 수행      |



### 메서드 참조(method reference)

하나의 메서드만 호출하는 람다식은 '메서드 참조'로 간단히 할 수 있다.

| 종류                            | 람다                       | 메서드 참조       |
| ------------------------------- | -------------------------- | ----------------- |
| static메소드 참조               | (x) -> ClassName.method(x) | ClassName::method |
| 인스턴스메소드 참조             | (obj, x) -> obj.method(x)  | ClassName::method |
| 특정 객체의 인스턴스메소드 참조 | (x) -> obj.method(x)       | obj::method       |

예시

```java
Integer method(String s) {
  return Integer.parseInt(s);
}
```

1차 람다식

```java
Function<String, Integer> f = (String s) -> Integer.parseInt(s);
```

최종 람다식

```java
Function<String, Integer> f = Integer::parseInt;
//Function에서 String 입력인 것을 알고 있기 때문에 String 생략 가능
```



### 생성자의 메소드 참조

#### 생성자와 메서드 참조

```java
Supplier<MyClass> s = () -> new MyClass();
//메소드참조로 수정
Supplier<MyClass> s = MyClass::new;

// 매개변수 1개인 경우
Function<Integer, MyClass> s = (i) -> new MyClass(i);
// 인자로 Integer타입을 주는 것을 알고 있으므로, i는 생략 가능
//메소드참조로 수정
Function<Integer, MyClass> s = MyClass::new;

//매개변수 2개인 경우
BiFunction<Integer, Character, MyClass> s = (i, c) -> new MyClass(i, c);
//메소드참조로 수정
BiFunction<Integer, Character, MyClass> s = MyClass::new;

//배열과 메소드참조
Function<Integer, int[]> f = x-> new int[x];
Function<Integer, int[]> f = int[]:new;
//배열 만들기
Function<Integer, int[]> f = int[]::new;
int[] array = f.apply(5);
System.out.println(array.length); //5 출력
```

