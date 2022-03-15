# 람다식

Java8 이후부터 람다식이 가능하게 되었다.



### 람다함수란

프로그래밍 언어에서 사용되는 개념으로 익명 함수를 칭하는 용어이다.

람다 대수는 수학에서 사용하는 함수를 보다 단순하게 표현하는 방법을 뜻한다.

람다의 근원은 수학과 기초 컴퓨터과학 분야에서의 람다 대수이다.



### 람다식 예제

``` java
Runnable runnable = new Runnable() { //익명 구현 객체
  public void run() { ~~~ } 
};
```

``` java
Runnable runnable = 90 -> { ~~~ }; //람다식
```



### 람다식 제한

람다식을 사용하기 위해서는 아래 조건을 모두 만족해야 한다.

- 인터페이스이어야 한다.
- 인터페이스에는 하나의 추상 메서드만 선언되어야 한다.
	- 오버라이드 해야 할 추상 메서드가 2개 이상인 경우 람다 표현식을 사용할 수 없다.



#### 람다식은 함수와 다른 변수 값을 전달하는 개념이 아닌, 행위를 전달한다고 생각하면 된다.

```java
public class Main {

    public static void main(String[] args) {
 
        Calculator calculator = new Calculator(30, 40);

        // a + b 행위
        int plus = calculator.result((a, b) -> {
            return a + b;
        });

        // a - b 행위
        int minus = calculator.result((a, b) -> {
            return a - b;
        });
    }
}
```

