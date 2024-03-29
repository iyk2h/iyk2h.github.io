# 상속(inheritance)

<br>

# 목차

- 자바 상속의 특징
- super 키워드
- 메소드 오버라이딩
- 다이나믹 메소드 디스패치 (Dynamic Method Dispatch)
- 추상 클래스
- final 키워드
- Object 클래스



<br>

---

## 자바 상속의 특징

> *"classes can be **derived** from other classes, thereby **inheriting** fields and methods from those classes."*

- Single inheritance (No diamond inheritance)
- `Object`를 제외한 모든 클래스는 암묵적으로 Object의 서브클래스
- 다단계 상속이 가능하고, 다중 상속을 지원하지 않는다.



<br>

## super 키워드

부모 클래스의 생성자나 메소드를 호출한다.

부모 생성자를 호출하는 경우를 특별히 `constructor chanining`이라고 부른다.

super()를 사용하면 슈퍼클래스의 no-argument 생성자가 호출됩니다. super(매개변수 목록)를 사용하면 일치하는 매개변수 목록이 있는 수퍼클래스 생성자가 호출됩니다.

만약 자식 클래스의 생성자에서 `super()`를 명시적으로 사용하지 않으면, 컴파일러가 부모 클래스의 no-arg 생성자를 호출하도록 코드를 삽입한다. 그런데 만약 부모 클래스에 no-arg 생성자가 없다면, 컴파일 에러가 발생한다.



<br>

## 메소드 오버라이딩

```java
class SuperClass {
    public void whoIAm() {
        System.out.println("I`m supper class.");
    }
}

class SubClass extends SuperClass {

    @Override
    public void whoIAm() {
        System.out.println("I`m sub class.");
    }
}

class Main {
    public static void main(String[] args) {
        SuperClass parent = new SuperClass();
        SubClass child = new SubClass();

        parent.whoIAm();
        child.whoIAm();
    }
}

//I`m supper class.
//I`m sub class.
```

 @Override 어노테이션은 개발자에게 "오버 라이딩된 메서드" 라고 알려주는 역할과 부모 클래스에 없는 메서드에 어노테이션을 붙이면 컴파일 에러가 난다.



|                          | Superclass Instance Method     | Superclass Static Method       |
| ------------------------ | ------------------------------ | ------------------------------ |
| Subclass Instance Method | Overrides                      | Generates a compile-time error |
| Subclass Static Method   | Generates a compile-time error | Hides                          |

오버라이딩 된 메소드의 Superclass의 메소드는 직접적으로 호출 불가.

하지만 Hides 상황에서는 Superclass의 메소드는 직접적으로 호출 가능.



<br>

## 다이나믹 메소드 디스패치 (Dynamic Method Dispatch)

"같은 클래스를 상속하고 있는 여러 클래스 중 어느 서브클래스를 사용할 것인가"를 런타임 시점까지 미룸으로서, 클래스 재사용성을 높이는 테크닉.

```java
class Parent {
    void run() {
        System.out.println("Parent.run()");
    }
}

class Child1 extends Parent {
    @Override
    void run() {
        System.out.println("Child1.run()");
    }
}

class Child2 extends Parent {
    @Override
    void run() {
        System.out.println("Child2.run()");
    }
}

class Main {
    public void main(String[] args) {
        Parent child1 = new Child1();
        Parent child2 = new Child2();
        
        child1.run();
        child2.run();
    }
}




// result

Child1.run()
Child2.run()
```



<br>

## 추상 클래스

```java
public abstract class GraphicObject {
   // declare fields
   // declare nonabstract methods
   abstract void draw();
}
```



- 다음 설명 중 하나라도 해당되는 경우 추상 클래스를 사용하는 것이 좋습니다.
	- 밀접하게 관련된 여러 클래스 간에 코드를 공유하려고 합니다.
	- 추상 클래스를 확장하는 클래스에 공통 메서드 또는 필드가 많거나 공용이 아닌 액세스 한정자(예: 보호됨 및 개인)가 필요합니다.
	- 정적이 아니거나 최종이 아닌 필드를 선언하려고 합니다. 이렇게 하면 자신이 속한 개체의 상태에 액세스하고 수정할 수 있는 메서드를 정의할 수 있습니다.
- 다음 설명 중 하나라도 해당되는 경우 인터페이스 사용을 고려하세요.
	- 관련 없는 클래스가 인터페이스를 구현할 것으로 예상됩니다. 예를 들어 ['Comparable'](https://docs.oracle.com/javase/8/docs/api/java/lang/Comparable.html) 및 ['Cloneable'](https://docs.oracle.com/javase/8/docs/api/java/lang/Cloneable.html) 인터페이스는 관련이 없는 많은 클래스에서 구현됩니다.
	- 특정 데이터 유형의 동작을 지정하려고 하지만 해당 동작을 구현하는 사용자는 상관하지 않습니다.
	- 형식의 다중 상속을 사용하려고 합니다.

https://docs.oracle.com/javase/tutorial/java/IandI/abstract.html



<br>

## final 키워드

final은 재정의하는 것을 막는 키워드이다.

- class
	- 클래스의 상속을 막는다.
- variable
	- 변수의 재할당을 막는다.
- method
	- 메서드의 오버라이딩을 막는다.



final의 오해

```java
import java.util.ArrayList;
import java.util.List;

class Main {

    public static void main(String[] args) {
        final List<Integer> list = new ArrayList<>();
        list.add(1);
        list.add(2);
        list.add(3);
        list.add(4);
        list.add(5);
        System.out.println(list); // [1, 2, 3, 4, 5]
      
      	list = new ArrayList<>(); // 오류! 재정의 금지!
    }
}
```



<br>

## Object 클래스

java.lang.Object 클래스는 모든 클래스의 최상위 클래스이다. 

| 메소드                                                       | 설명                                                    |
| ------------------------------------------------------------ | ------------------------------------------------------- |
| boolean equals(Object obj)                                   | 두 객체가 같은 지 비교한다.(같으면 true, 틀리면 false)  |
| String toString()                                            | 객체의 문자열을 반환한다.                               |
| protected Object clone()                                     | 객체를 복사한다.                                        |
| protected void finalize()                                    | 가비지 컬렉션 직전에 객체의 리소스를 정리할때 호출한다. |
| Class getClass()                                             | 객체의 클레스형을 반환한다.                             |
| int hashCode()                                               | 객체의 코드값을 반환한다.                               |
| void notify()                                                | wait된 스레드 실행을 재개할 때 호출한다.                |
| void notifyAll()                                             | wait된 모든 스레드 실행을 재개할 때 호출한다.           |
| void wait()                                                  | 스레드를 일시적으로 중지할 때 호출한다.                 |
| void wait(long timeout),<br /> void wait(long timeout, int nanos) | 주어진 시간만큼 스레드를 일시적으로 중지할 때 호출한다. |


<br>