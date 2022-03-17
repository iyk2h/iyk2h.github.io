> - MySQL 5.5 까지는 서브쿼리 최적화가 최악이라 웬만하면 Join으로 전환하자
> 	- 메인테이블의 row 수 만큼 서브 쿼리를 수행한다
> - MySQL 5.6 에서 서브 쿼리가 대폭 최적화 되었다.
> 	- 다만 최적화가 적용 안되는 조건들이 다수 존재한다
> - 버전/조건 관계 없이 좋은 성능을 내려면 **최대한 Join을 이용**하자
> - Join을 사용하기가 너무 어렵다면 Subquery는 사용하되, MySQL 5.5 이하라면 절대 사용하지 않는다.
> 	- 차라리 **쿼리를 나눠서 2번 실행** (메인쿼리/서브쿼리)하고 애플리케이션에서 조립하는게 낫다.
>
> Reference : https://jojoldu.tistory.com/520