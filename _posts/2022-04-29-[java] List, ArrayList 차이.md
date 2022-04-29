찾아본 결과 간단하게 

- List = interface
- ArrayList = class

이렇게 표현할 수 있다.



그럼 차이점은 무엇인가.



- **ArrayList <Object> list = new ArrayList <>();** (O)
- **List <Object> list = new ArrayList <>();**  (O)
- ~~**ArrayList <Object> list = new List <>();**~~  (X)

이렇게 보면 대충 느낌이 올것같다.

자바의 두가지 이점을 가지고 있는데 한가지는 다형성이고, 한가지는 유연성이다.

1. 다형성

	- **ArrayList <Object> list = new ArrayList <>();** (O)
		- 벤츠 list = new 벤츠();
	- **List <Object> list = new ArrayList <>();**  (O)
		- 자동차 list = new 벤츠();

	위와같이 클래스를 생성 할 때 자동차 타입으로 생성하게 되면 벤츠 뿐만아니라 현대, 쌍용 등 자동차 인터페이스를 구현한 클래스에서 사용할 수 있다.

	- ~~**ArrayList <Object> list = new List <>();**~~  (X)
		- ~~벤츠 list = new 자동차();~~ (X)

	반대로 위와 같이 클래스를 생성하면 오류가 난다.

	이유는 벤츠 자리는 자동차가 대체할 수 있지만, 자동차 자리는 벤츠가 대체 할 수 없다.

	

2. 유연성

여기서 제네릭(Generic)에 대한 개념을 볼 수 있다.

제네릭은 클래스의 타입을 내부에서 지정하는 것이 아닌 외부에서 사용자에 의해 지정되는 것을 뜻한다.

용도에 맞게

- **List <Object> list = new List <>();** 
- **List <Object> list = new ArrayList <>();**  
- **List <Object> list = new LinkedList <>();** 

위 3개의 list 는 다 다른 클래스 타입을 가질 수 있다.

이처럼 유연하게 용도에 맞게 필요에 의해 지정할 수 있는 이점이 있다.