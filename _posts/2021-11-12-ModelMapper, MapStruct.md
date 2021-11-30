### ModelMapper, MapStruct의 의존성설정, 매핑 사용법과 차이점

가장 큰 차이점은 속도의 차이가 있다.

ModelMapper 은 modelMapper.map 매핑이 일어날 때 리플렉션이 발생하고

MaStruct 는 컴파일 시점에서 구현체를 만들어 리플렉션이 발생하지 않는다

*리플렉션은 구체적인 클래스 타입을 알지 못해도, 컴파일한 클래스 정보를 활용해 그 클래스의 메소드, 타입, 변수들에 접근할  수 있도록 해 동적으로 프로그래밍이 가능하도록 지원하는 API

*동적으로 프로그래밍 -> 런타임 시점에 타입을 결정

즉, ModelMapper은 런타임에 매핑이 일어나고 MaStruct은 컴파일 시점에 구현체를 만든다.

### Reference 

ModelMapper - http://modelmapper.org/user-manual/

MapStruct - https://mapstruct.org/documentation/reference-guide/

