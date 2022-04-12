2인이 개발하는 관계로 따로 필요성이 없어보임..

혼자 merge 규칙을 정해서 혼자 관리해보자.

### Branch Rules

------

- **mater** : 이 브랜치는 실제로 서비스 제공
- **release branch** : Release를 위해 사용되는 브랜치
- **develop** : 기능 및 하위 단위 브랜치. 실제 배포 전에 이 브랜치에서 확인 및 테스트, 해당 브랜치에 개발한 내역들이 쌓임.

### Merge

------

- **master ← release branch**  : release branch 를 통해서 merge
- **release branch ← develop** : Squash Commit을 남기는 방법으로 작업하기. release 에는 구체적인 변동 사항을 깔끔하게 정리

- **develop ← 하위** : Squash Commit을 남기는 방법으로 작업하기. develop에는 구체적인 모든 사항을 깔끔하게 정리



## ETC

Squash Commit 가져오기

`$ git reset --hard upstream/[BRANCH]`

새로운 브랜치 만들어서 Squash Commit 가져오기

`$ git checkout -b [NEW_BRANCH] upstram/[BRANCH]`

 `$ git checkout`을 사용해 Squash Commit 브랜치를 가져온다. 개인 gitgub 커밋, 리뷰어용 커밋 따로 관리



#### Reference:

https://techblog.woowahan.com/2553/

https://velog.io/@godori/Git-Rebase

https://baeji77.github.io/dev/git/etc/git-rebase-and-confilct-resolve/

https://www.youtube.com/watch?v=MIGliPrUMGE

[인텔리제이 - Git 사용법](https://sun5066.tistory.com/entry/%EC%9D%B8%ED%85%94%EB%A6%AC%EC%A0%9C%EC%9D%B4-Git-%EC%82%AC%EC%9A%A9%EB%B2%95%EB%A1%9C%EC%BB%AC-%EB%B8%8C%EB%9E%9C%EC%B9%98-Merge-Push)

