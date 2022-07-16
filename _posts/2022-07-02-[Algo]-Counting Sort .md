### 요약

핵심 아이디어

- 카운팅 정렬(계수 정렬)은 입력을 반복하고 각 항복이 발생하는 횟수를 새로운 배열에 카운트한다. 카운트한 배열을 사용해 정렬한다.

장점 

- 시간복잡도는 O(n) 으로 엄청난 성능을 보여주는 알고리즘이다.

- 대표적인 빠른 정렬 알고리즘보다 성능이 좋다. 큌 정렬, 힙 정렬, 합병 정렬 등의 시간복잡도는 O(nlogn)  으로 빠른 성능을 가지고 있다.

단점

- 입력값의 범위를 미리 알고 있을때만 사용하는게 좋다.
	- 정렬을 하기 위해 새로운 배열을 선언해주어야 한다. 즉, 입력값의 범위가 커지면 메모리 낭비가 된다.
	- ex) 5개의 원소를 정렬하고 하는데, 수의 범위가 0~5000 이라면 새로운 배열의 사이즈는 5000이 된다.

작동 애니메이션 URL

- https://www.cs.miami.edu/home/burt/learning/Csc517.091/workbook/countingsort.html



### 구현

```java
  public static int[] countingSort(int[] array, int maxValue) {

    // 배열 안에 있는 값을 카운팅 하는 과정
    int counts[] = new int[maxValue + 1];
    int sortedArray[] = new int[array.length];
    
    for (int item : array) {
        counts[item] += 1;
    }

    // counts 배열에 count값을 누적하는 과정
    int numItemsBefore = 0;
    for (int i = 0; i < counts.length; i++) {
      // counts 값의 카운틴된 값의 수를 count에 저장
      int count = counts[i];
      // 직전의 누적 값을 저장
      counts[i] = numItemsBefore;
      // 카운트값 누적
      numItemsBefore += count;
    }

    //누적된 counts의 배열을 이용해 정렬
    for (int item : array) {
        // counts[item]을 통해 자릿수에 값 저장 
        sortedArray[ counts[item] ] = item;
        // 값 정렬 후 자릿수 1 증가
        counts[item] += 1;
    }

    return sortedArray;
}
```



카운팅된 값을 누적시켜서 새로 저장하는 이유는

ex)

정렬 전 배열 : [3, 3, 3, 2, 1, 2, 3, 2, 2, 1]

counts : [0,2,4,4,0,0]

누적 후 counts : [0, 0, 2, 6, 10, 10]

누적 후 counts 는 정렬 할 때 값들의 index가 된다.

counts[item] += 1 을 하는 이유도, index값을 올려줌으로써 카운트된 수 만큼 저장되게 하기 위함이다.



### 정리

값을 직접 비교하는게 아닌 누적된 값 많큼 수를 저장하는것이기 때문에 속도는 다른 정렬보다 빠르다.

정렬을 하려면 정렬할 배열의 값의 범위+1의 새로운 배열을 만들어야 하는 단점이 있다. 즉, 값의 개수는 작은데 범위가 큰 경우 메모리 낭비가 생기게 되는 단점이 있다. 또한 정렬하기 위해 수의 범위를 알고 있어야한다.

자바에서 1차원 배열 객체 하나의 크기는 최대 integer.MAX_VALUE 미만으로만 가능하기 때문에 거의 안쓰인다. 그래서 대부분 언어에서는 QuickSort나  Timsort를 사용한다. 
