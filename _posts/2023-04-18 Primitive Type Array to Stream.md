### Primitive Type Array to Stream

```java
import java.util.Arrays;
import java.util.stream.DoubleStream;
import java.util.stream.IntStream;
import java.util.stream.LongStream;
import java.util.stream.Stream;

public class Main {

    public static void main(String[] args) {
        // Example with int[]
        int[] arr = {1, 2, 3, 4, 5};

        // Convert int[] to IntStream
        IntStream intStream = Arrays.stream(arr);

        // Example with double[]
        double[] arr2 = {1.1, 2.2, 3.3, 4.4, 5.5};

        // Convert double[] to DoubleStream
        DoubleStream doubleStream = Arrays.stream(arr2);

        // Example with long[]
        long[] arr3 = {1L, 2L, 3L, 4L, 5L};

        // Convert long[] to LongStream
        LongStream longStream = Arrays.stream(arr3);

        // Example with char[]
        char[] chars = {'a', 'b', 'c', 'd', 'e'};

        // Convert char[] to Stream<Character>
        // Stream<Character> charStream = Arrays.stream(chars); (오류)
        Stream<Character> charStream = new String(chars).chars()
                .mapToObj(c -> (char) c);
    }
}
```

### char[] 는 왜 다르지?

```java
char[] chars = {'a', 'b', 'c', 'd', 'e'};

// 이 부분에서 오류가 난다.
// Stream<Character> charStream = Arrays.stream(chars);
```

여기서 오류니는 이유는 Arrays.stream()에서 []char 을 지원해주지 않기 때문이다.

[Why are char[\] the only arrays not supported by Arrays.stream()?](https://stackoverflow.com/questions/60037413/why-are-char-the-only-arrays-not-supported-by-arrays-stream)



### char[][] to Stream

```java
char[][] chars = new char[5][5];
Stream<char[]> stream5 = Arrays.stream(chars);
```

chars 배열은 char[]로 이루어져 있다. char[] == 객체
char[]은 .toString() 과 같이 Object 클래스에서 상속되는 관련 메서드 및 속성을 가지고 있어서 객체입니다.
그래서 2차원 배열 char[][]가 Stream으로 사용될 수 있는 이유입니다.