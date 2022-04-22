### 왜 StringBuilder 사용할까?



java 에서 많은 문자열을 연결하면 많은 중간 문자열 객체가 생성되어 비효율적인 코드가 생성된다고 한다.

이유는 자바에서 String 객체는 변경 불가능하다. 한 번 생성되면 내용을 바꿀 수 없단 뜻이다. 따라서 하나의 문자열을 다른 문자열과 연결하면 새 문자열이 생성되고, 이전 문자열은 가비지 컬렉터로 들어간다.

``` java
String str= "a" + "b" + "c" + "d" + "e";
str= "ab" + "c" + "d" + "e";
str= "abc" + "d" + "e";
str= "abcd" + "e";
str= "abcde";
```



그래서 이러한 메모리 낭비를 위해 StringBuilder를 사용한다. StringBuilder는 변경 가능한 문자열을 만들어주기 때문이다.



StringBuilder 에서의 append() 를 보면

``` java 
public AbstractStringBuilder append(String str) {
        if (str == null) {
            return appendNull();
        }
        int len = str.length();
        ensureCapacityInternal(count + len);
        putStringAt(count, str);
        count += len;
        return this;
    }
```

배열에 문자를 추가하는 형태로 메모리 낭비가 덜하다.



#### 사용법

``` java
public class Main
{
    public static void main(String[] args)
    {
        StringBuilder sb = new StringBuilder();
        sb.append("문자열 ").append("연결");
//        String str = sb;   // String에 StringBuilder를 그대로 넣을 순 없다. toString()을 붙여야 한다
        String str = stringBuilder.toString();
      
        System.out.println(sb);
        System.out.println(str);
    }

}
```





#### Reference

https://www.codejava.net/java-core/the-java-language/why-use-stringbuffer-and-stringbuilder-in-java