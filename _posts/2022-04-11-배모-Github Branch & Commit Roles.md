## Git

### Branch 전략


#### Type

| 제목   | 내용                               |
| ------ | ---------------------------------- |
| feat   | 새로운 기능 / 특징                 |
| fix    | 버그를 고침                        |
| hotfix    | 긴급 버그를 고침                       |
| refact | 프로덕션 코드를 리팩토링           |
| style  | Code의 스타일, 포맷 등이 바뀐 경우 |
| test   | 테스트 코드 추가 및 업데이트       |
| docs   | 도큐먼트 / 문서화 업데이트         |
|chore| 프로덕션 코드가 바뀌지 않은 가벼운 일들|
| deps   | Dependency와 관련 있는 내용        |



## Branch Naming

- format

```
<제목>-<내용>
```

- example

```
feat-login_screen  # 새로운 기능/로그인 화면 개발 
```

## commit message

- format

```
<형상 관리 규칙 제목>: <comment>
```

- example
	- `feat: getService 기능 추가`
	- `fix: getService 문제 제거`
	- `refactor: logic refactoring`
	- `style: 탭을 띄어쓰기로 바꿈`
	- `test: getService에 대한 Mock Test`
	- `doc: README.md에 대한 설명 추가`
	- `chore: 빌드 스크립트 추가`
	- `deps: mvc dependency 버전 변경`





#### Reference

- https://github.com/Mash-Up-MapC/MapC-backend/issues/17
- https://github.com/mash-up-kr/9tique-android/wiki/2.-Git
- [[Git] Github 같은 저장소 함께 쓰기(feat. Github Flow)](https://fomaios.tistory.com/entry/Git-Github-%EA%B0%99%EC%9D%80-%EC%A0%80%EC%9E%A5%EC%86%8C-%ED%95%A8%EA%BB%98-%EC%93%B0%EA%B8%B0feat%ED%98%91%EC%97%85%ED%95%98%EA%B8%B0)
- https://rose-prepared-583.notion.site/Git-Branch-cb7891a287b049a7965659fb2679e5e1
- http://karma-runner.github.io/0.10/dev/git-commit-msg.html
- https://sparkbox.com/foundry/semantic_commit_messages