RDB에는 컬렉션과 같은 형태의 데이터를 컬럼에 저장할 수 없다. 별도의 테이블을 생성해 컬렉션을 관리하게된다.

*컬렉션이란 그저 용도가 같거나 유사한 문서들을 그룹으로 묶은 것*

JPA 에서 컬렉션 객체임을 지정하는 방법은 @ElementCollection 어노테이션을 사용하는 방법이다.

```
// Member 클래스
@Entity
public class Member {
    @Id 
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    private Long id;
    
    private String name;
 
    @ElementCollection(fetch = FetchType.LAZY)
    @Builder.Default
    Private Set<MemberRole> roleSet = new HashSet<>();
    
    Public void addMemberRole(MemberRole memberRole){
    	roleSet.add(MemberRole);
    }
}
```

```
// MemberRole 클래스
public enum MemberRole {
	USER, MANAGER, ADMIN
}
```



## @ElementCollection 와 @OneToMany 의 차이

**@ElementCollection**

- 연관된 부모 Entity 하나에만 연관되어 관리된다. (부모 Entity와 독립적으로 사용 X)
- 항상 부모와 함께 저장되고 삭제되므로 cascade 옵션은 제공하지 않는다. (cascade = ALL 인 셈)
- 부모 Entity Id와 추가 컬럼(basic or embedded 타입)으로 구성된다.
- 기본적으로 식별자 개념이 없으므로 컬렉션 값 변경 시, 전체 삭제 후 새로 추가한다.

**@OneToMany **

- 다른 Entity에 의해 관리될 수도 있다.
- join table이나 컬럼은 보통 ID만으로 연관을 맺는다.



## 값 타입 컬렉션 제약사항

- **값 타입 컬렉션에 변경 사항이 발생하면, 주인 엔티티와 연관된 모든 데이터를 삭제하고, 값 타입 컬렉션에 있는 현재 값을 모두 다시 저장한다.** 
	-> 위험하다. 사용 권장 x
- 값 타입 컬렉션을 매핑하는 테이블은 모든 컬럼을 묶어서 기본키를 구성해야 함: null 입력X, 중복 저장X

## 해결방안

- 실무에서는 상황에 따라 값 타입 컬렉션 대신에 일대다 관계를 고려
- **일대다 관계를 위한 엔티티를 만들고, 여기에서 값 타입을 사용**
- 영속성 전이(Cascade) + 고아 객체 제거를 사용해서 값 타입 컬
	렉션 처럼 사용



출처 

- https://velog.io/@wnsqud70/값-타입-컬렉션
- https://live-everyday.tistory.com/209
- https://prohannah.tistory.com/133
