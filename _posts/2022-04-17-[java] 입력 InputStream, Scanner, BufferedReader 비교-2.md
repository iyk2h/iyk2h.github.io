#### Scanner

![image-20220417174059429](/Users/youngkyoonim/TIL/iyk2h.github.io/images/image-20220417174059429.png)



주로 아래와 같이 사용하는데

```java 
Scanner sc = new Scanner(System.in)
```

오버리이딩 된 Scanner 를 보면

![image-20220417174237409](/Users/youngkyoonim/TIL/iyk2h.github.io/images/image-20220417174237409.png)

InputStream을 통해 입력된다.

자세히 보면 Scanner() 생성자들이 this를 통해서 private Scanner(Readable source, Pattern pattern) 으로 넘겨진다.

여기서 InputStreamReader가 나온다. 

##### InputStreamReader이란?

>An InputStreamReader is a **bridge from byte streams to character streams**: It reads bytes and decodes them into characters using a specified [`charset`](https://docs.oracle.com/javase/7/docs/api/java/nio/charset/Charset.html). The charset that it uses may be specified by name or may be given explicitly, or the platform's default charset may be accepted.
>
>InputStreamReader는 **"바이트 스트림에서 문자 스트림으로의 브리지" **입니다. 바이트를 읽고 지정된 문자 집합을 사용하여 바이트를 문자로 디코딩합니다. 사용하는 문자 집합은 이름으로 지정되거나 명시적으로 지정되거나 플랫폼의 기본 문자 집합이 허용될 수 있습니다.



전에 알아본 InputStream에서 1Byte씩 받은 문자를 문자단위인 character로 변환시키는 중개자 이다. 문자스트림이라고 불리기도 한다.



InputStream 은 Byte Type, 바이트 단위

InputStreamReader 은 char Type, 문자 단위



추가로, Scanner 가 느리다고 많이들 얘기하는데 느린 이유는 Scanner는 수많은 정규식을 통해 검사 된 문자열을 반환하기 때문에 느려진다. 정규식 자체도 느리지만 정규식의 양이 많다.



가볍게 정리해보면

Scanner 에서 InputStreamReader 를 사용하는 이유는 문자를 온전하게 받기 위함이고

Scanner의 메소드 next(), nextInt() 등은 타입에 맞게 정규식을 검사해서 상대적으로 느리다



##### 그럼 문자열은? 바로 BufferedReader!

