## 제어자(modifier)

- 클래스와 클래스의 멤버(멤버 변수, 메서드)에 부가적인 의미 부여

	- 접근 제어자 public, protected, (default), private
	- 그 외 static, final, abstract, native, transient, synchronized, volatile, strictfp

- 하나의 대상에 여러 제어자를 같이 사용가능(접근 제어자는 하나만)

- ```java
	public class ModifierEx {
	  public static final int a;
	  
	  public static void main(){};
	}
	```



### static - 클래스의 공통적인

| 제어자 | 대상     | 의미                                                         |
| ------ | -------- | ------------------------------------------------------------ |
| static | 멤버변수 | - 모든 인스턴스에 공통적으로 사용되는 클래스 변수가 된다<br />- 클래스 변수는 인스턴스를 생성하지 않고도 사용 가능하다.<br />- 클래스가 메모리에 로드될 때 생성된다. |
| static | 메서드   | - 인스턴스를 생성하지 않고도 호출이 가능한 static 메서드가 된다.<br />- static메서드 내에서는 인스턴스멤버들을 직접 사용할 수 없다. |

```java
class StaticEx {
  static int a = 1;							// 클래스 변수(static변수)
  static int b = 2;							// 클래스 변수(static변수)
  
  static { 											// 클래스 초기화 블럭
														    // static변수의 복잡한 초기화 수향
  }
  
  static int max(int a, int b) { // 클래스 메서드(static메서드)
    return a > b ? a : b; // iv, instance method 사용 불가
  }
}
```



### final - 마지막의, 변경될 수 없는

| 제어자 | 대상                      | 의미                                                         |
| ------ | ------------------------- | ------------------------------------------------------------ |
| final  | 클래스                    | 변경될 수 없는 클래스, 확장될 수 없는 클래스가 된다<br />그래서 final로 지정된 클래스는 다른 클래스의 조상이 될 수 없다. |
| final  | 메서드                    | 변경될수 없는 메서드, final로 지정된 메서드는 오버라이딩을 통해 재정의 될 수 없다. |
| final  | 멤버변수 / <br />지역변수 | 변수 앖에 final이 붙으면, 값을 변경할 수 없는 상수가 된다.   |



### abstract - 추상의, 미완성의

| 제어자   | 대상   | 의미                                                         |
| -------- | ------ | ------------------------------------------------------------ |
| abstract | 클래스 | 클래스 내에 추상 메서드가 선언되어 있음을 의미한다.          |
| abstract | 메서드 | 선언부만 작성하고 구현부는 작성하지 않은 추상 메서드임을 알린다. |

```java
//미완성 클래스 = 미완성 설계도
abstract class AbstractEx{  // 추상 클래스(추상 메서드를 포함한 클래스)
  abstract void move();			// 추상 메서드(구현부가 없는 메서드)
}
AbstractEx a = new AbstractEx(); // 에러. 추상 클래스의 인스턴스 생성 불가
```

추상 클래스를 상속받아서 완전한 클래스를 만든후에 인스턴스 생성 가능
