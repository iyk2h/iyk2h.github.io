## import문

- 클래스를 사용할 때 패키지이름을 생략할 수 있다.
- 컴파일러에게 클래스가 속한 패키지를 알려준다.
- java.lang패키지의 클래스는 import하지 않고도 사용할 수 있다. ex) println, String ...

```java
inport java.util.Date;

class ImportTest {
  Date today = new Date();
}
```



## inport문의 선언

- import문을 선언하는 방법은 다음과 같다.

```
inport 패키지명.클래스명;
또는
inport 패키지명.*; -> 모든 클래스
```

- import문은 컴파일 시에 처리되므로 프로그램의 성능에 영향없다.
- 다음의 두 코드는 서로 의미가 다르다

```
inport java.util.*;
inport java.text.*;
// 아래 코드와 의미가 다름
inport java.*; -> java 패키지의 모든 클래스(패키지는 포함안됨)
```

- 이름이 같은 클래스가 속한 두 패키지를 import할 때는 클래스 앞에 패키지명을 붙여줘야한다.



## static import문

- static멤버를 사용할 때 클래스 이름을 생략할 수 있게 해준다.

```java
inport static java.lang.Math.random;
inport static java.lang.System.out; // System.out을 out만으로 참조 가능

System.out.println(Math.random()); -> out.println(random());
```