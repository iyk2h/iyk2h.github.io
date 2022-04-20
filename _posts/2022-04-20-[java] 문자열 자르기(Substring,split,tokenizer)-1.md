### java에서 문자열 자르는 방법은 3가지가 있다.

- Substring
- split
- tokenizer





#### indexOf()

```java
String ex = "123-123";
int idx = ex.indexOf("-");

//결과값 : 인덱스 값 출력
// 3 
```



#### substring() : 문자열을 인덱스로 자른다.

``` java
//사용법
String.substring(start) //문자열  start위치부터 끝까지 문자열 자르기
String.substring(start,end) // 문자열  start위치 부터 end전까지 문자열 가져오기
```

```java
String ex = "123-123";
ex.substring(4); //123
ex.substring(2,4); //3-3
```



#### split() : 지정한 문자를 기준으로 문자열을 잘라 배열로 반환

```java
//1. 쉼표(,)로 문자열 잘라서 배열에 넣기
String str = "A,B,C";
String[] array = str.split(",");
		    
//출력				
for(int i=0;i<array.length;i++) {
System.out.println(array[i]);
}
		  
//결과값 
//array[0] = A
//array[1] = B
//array[2] = C
```



### charAt() : 지정된 인덱스에서 char 값을 반환 (아스키코드 값 반환)

```java
String ex = "123-123";

ex.charAt(0); // 49
ex.charAt(2); // 51

//만약 숫자로 출력하고 싶으면
int a = ex.charAt(0) - 48;
```



