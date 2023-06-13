## 커밋 메시지의 형식

```null
<type>(<scope>): <short summary>
<BLANK LINE>
<body>
<BLANK LINE>
<footer>
```

커밋 메시지의 각 줄은 100자를 넘기지 말아야 한다.



#### `<type>`에 들어갈 수 있는 항목들

- feat : 새로운 기능 추가

- fix : 버그 수정

- docs : 문서 관련

- style : 스타일 변경 (포매팅 수정, 들여쓰기 추가 등)

- refactor : 코드 리팩토링

- test : 테스트 관련 코드

- build : 빌드 관련 파일 수정

- ci : CI 설정 파일 수정

- perf : 성능 개선

- chore : 그 외 자잘한 수정

	

#### `<scope>`에 들어갈 수 있는 항목들

어디가 변경되었는지, 변경된 부분은 모두 들어갈 수 있다.

함수가 변경되었으면 함수 이름, 메소드가 추가되었으면 클래스 이름

scope는 생략 가능합니다.



#### `<short summary>` 요약 설명

- 첫글자를 대문자로 쓰지 마세요. 소문자로 쓰세요.

- 명령문, 현재 시제로 작성합니다.

	> 변경되었으면 : "change"를 사용한다. "changed"나 "changes"를 사용하지 않는다.

- 마지막에 마침표(.)를 붙이지 마세요



### 메시지 내용 (Message Body)

- 명령문, 현재 시제로 작성하길 권장한다.
- 변경한 이유와 변경 전과의 차이점을 설명한다.



### 메시지 하단 (Message Footer)

#### 주요 변경 내역들 (Breaking Changes)

모든 주요 변경 내역들은 다음과 함께 하단에 언급되어야 합니다.

- 변경점 (description of the change)
- 변경 사유 (justification)
- 마이그레이션 지시 (migration instructions)

#### 해결된 이슈 (Referencing Issues)

해결된 이슈는 커밋 메시지 하단에 `Closes #<이슈번호>` 와 같이 기록되어야 한다.

```null
Closes #123
```

이슈가 여러개인 경우

```null
Closes #111, #222
```





참고 

https://gist.github.com/stephenparish/9941e89d80e2bc58a153

https://velog.io/@outstandingboy/Git-%EC%BB%A4%EB%B0%8B-%EB%A9%94%EC%8B%9C%EC%A7%80-%EA%B7%9C%EC%95%BD-%EC%A0%95%EB%A6%AC-the-AngularJS-commit-conventions#%EC%BB%A4%EB%B0%8B-%EB%A9%94%EC%8B%9C%EC%A7%80-%ED%97%A4%EB%8D%94-commit-message-header
