
@EqualsAndHashCode(of = "id") 을 주는 이유는 객체각 연관관계가 있을 경우 스택 오버 플로우가 발생할 수 있다고 한다.

of 안에 연관관계 있는 값을 넣으면 안된다.

이러한 이유로 @Data 어노테이션을 함부로 쓰면 안된다.



@EqualsAndHashCode(of = "id")  를 이용하면 아래와 같은 equals 코드가 자동 생성된다.

``` java
public boolean equals(final Object o) {
  if (o == this) {
    return true;
  } else if (!(o instanceof Event)) {
    return false;
  } else {
    Event other = (Event)o;
    if (!other.canEqual(this)) {
      return false;
    } else {
      // 이 부분을 보면 ID만 가지고 구현되있다.
      Object this$id = this.getId();
      Object other$id = other.getId();
      if (this$id == null) {
        if (other$id != null) {
          return false;
        }
      } else if (!this$id.equals(other$id)) {
        return false;
      }

      return true;
    }
  }
}
```



추가로 EqualsAndHachCode 에 관한 좋은 블로그기 있다. 

https://jojoldu.tistory.com/134

엔티티 선언할때 참고해도 좋은 글이다.
