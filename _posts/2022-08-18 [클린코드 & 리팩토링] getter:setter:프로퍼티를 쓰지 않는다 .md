## getter/setter/프로퍼티를 쓰지 않는다.

Entity에서 getter/setter 사용을 지양해 상태 노출을 최소화

객체의 상태를 가져오는 접근자를 사용하는 것은 괜찮지만, getter/setter를 사용해 객체 바깥에서 그 결괏값을 사용해 객체에 관한 결정을 내리는 것은 안 된다.

한 객체의 상태에 관한 결정은 어떤 것이든 그 객체 안에서만 이루어져야 한다. 즉, 객체에 메시지를 던져서 작업해야한다.

또한, getter/setter를 사용하게 되면 Open/Closed 원칙을 위반하게 된다.

getter는 객체의 상태 값을 가져오기 위해 꼭 필요하다면 getter는 사용해도 된다.

```java
// 잘못된 예
public class Product {
    private final Name name;
    private final Count count;

    public Jamie(Name name, Count count) {
        this.name = name;
        this.count = count;
    }

		public int setCount(int count) {
        this.count = count;
    }
    public int getCount() {
        return count;
    }
}
// 수량 - 1
product.setCount(product.getCount() - 1);
```

```java
// 좋은 예
public class Product {
    private final Name name;
    private final Count count;

    public Jamie(Name name, Count count) {
        this.name = name;
        this.count = count;
    }

    public void minusOneProduct() {
        this.count - 1;
    }
}
// 수량 - 1
product.minusOneProduct();
```

