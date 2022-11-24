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

@FunctionalInterface 를 붙여주는 게 좋다. 2개의 추상 메서드를 가지면 에러를 띄워준다.