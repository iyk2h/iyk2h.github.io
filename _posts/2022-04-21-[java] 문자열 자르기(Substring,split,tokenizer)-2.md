위에서 문자열 나누는 메소드를 알아봤는데, 클래스도 있다.

### StringTokenizer Class

문자열을 토큰화 하는 클래스로, 분리된 문자열 조각을 토큰이라 하고, 문자열을 여러 개의 토큰으로 분리해준다.



#### 생성자

```java
import java.util.StringTokenizer;


StringTokenizer st = new StringTokenizer(문자열); // \t\n\r\f 공백 문자, 탭 문자, 줄바꿈 문자, 캐리지 리턴 문자, 폼피드 문자 기준으로 토큰화 ( 문자열 분리 )
StringTokenizer st = new StringTokenizer(문자열, 구분자); // 구분자 기준으로 토큰화 ( 문자열 분리 )
StringTokenizer st = new StringTokenizer(문자열, 구분자, true/false); // default : false, true 시 구분자도 토큰화 된다. (ex. 문자열,구분자,문자열,구분자,...)
```



#### Method

| Method                             | 설명                                                         |
| ---------------------------------- | ------------------------------------------------------------ |
| int countTokens();                 | 구분자를 통해 생성되는 토큰(Token)에 개수                    |
| boolean hasMoreElements            | 토큰(Token)이 남아있는지를 판단                              |
| boolean hasMoreTokens              | 토큰(Token)이 남아있는지를 판단                              |
| Object nextElement()               | nextToken()과 동일하지만 반환형이 Object                     |
| String nextToken()                 | 다음 토큰(Token)에 해당하는 문자열 반환                      |
| String nextToken(String delimeter) | 구분자에 의해 나누어진 다음 토큰(Token)에 해당하는 문자열 반환 |



#### Method 활용

``` java
import java.util.StringTokenizer;
public class Method
{
	public static void main(String[] args)
	{
		StringTokenizer sample = new StringTokenizer("Hello~Java~World~!!", "~", false);

		System.out.println("생성된 토큰 수 : " + sample.countTokens());

		while(sample.hasMoreTokens())
		{
			System.out.println(sample.nextToken());
		}
	}
}
```



#### 추가 

``` java
import java.util.StringTokenizer;
public class Method
{
	public static void main(String[] args)
	{
    StringTokenizer sample = new StringTokenizer("str :Hello?hi~Java~World~:?!!", "~:?", true);
            System.out.println("생성된 토큰 수 : " + sample.countTokens());

            while(sample.hasMoreTokens())
            {
                System.out.println(sample.nextToken());
            }
	}
}

// 결과값
생성된 토큰 수 : 13
str 
:
Hello
?
hi
~
Java
~
World
~
:
?
!!
```

구분자 안에 포함되면 다 토큰화 한다. 또한 구분자 안에 포함된 값을 하나씩 토큰화 한다.