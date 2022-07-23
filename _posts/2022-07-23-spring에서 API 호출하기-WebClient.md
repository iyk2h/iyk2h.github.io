### **Spring WebClient**

**Spring WebClient는 Single Thread와 Non-Blocking방식을 사용**한다.



**Spring Web Client 특징**

- 싱글 스레드 방식을 사용
- Non-Blocking 방식을 사용
- JSON, XML을 쉽게 응답받는다.
- React Web 프레임워크인 [Spring WebFlux](https://docs.spring.io/spring-framework/docs/current/reference/html/index.html) 에서 Http Client로 사용됩니다.



**Spring Web Client 동작 원리**

![image-20220723174525037](/Users/youngkyoonim/TIL/iyk2h.github.io/images/image-20220723174525037.png)

출처:&nbsp;https://luminousmen.com/post/asynchronous-programming-blocking-and-non-blocking

- 각 요청은 Event Loop 내에 Job으로 등록이 된다.
- **Event Loop는 각 Job을 제공자에게 요청한 후, 결과를 기다리지 않고 다른 Job을 처리한다.**
- WebClient는 이렇게 이벤트에 반응형으로 동작하게 설계되었다.
- 그래서 반응성, 탄력성, 가용성, 비동기성을 보장하는 프레임워크를 사용합니다.

출처 : https://happycloud-lee.tistory.com/220



### RestTemplate, WebClient성능 비교

![image-20220723222709805](/Users/youngkyoonim/TIL/iyk2h.github.io/images/image-20220723222709805.png)
출처: https://alwayspr.tistory.com/44

