#### BufferedReader

```java
BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
```



위에서 정리한게 이해됐다면 BufferedReader 도 금방 이해가 가능할거라 생각된다.



BufferedReader를 선언할 때 new BufferedReader(new InputStreamReader(System.in)) 를 사용한다.

즉, BufferedReader는 문자를 받는다.



우리는 문자열을 입력할때 문자열의 길이가 가변적이다. 그래서 Buffer(버퍼)를 통해 입력받은 문자를 쌓아둔 뒤 한 번에 **문자열처럼** 보내버린다.



BufferedReader의 입력 메소드로 readLine()을 많이 쓴다. 이 메소드는 한 줄 전체(공백 포함)를 읽기 때문에 char 배열을 하나하나 생성할 필요 없이 String 으로 리턴하여 바로 받을 수 있다는 장점을 가지고 있다.

즉, 문자를 가변적으로 받아 문자의 직렬화를 통해 문자열을 만들게 된다.



정리하면,

System.in -> InputStream  -> InputStreamReader -> BufferedReader

  	입력	  -> 	Byte type	-> 		char type			-> 		String



또한 BufferedReader는 따로 정규식 검사를 진행하지 않고, 버퍼에 저장해 String을 만든다.

그래서 Scanner에 비해 성능이 좋다.



