- 자동 등록과 수동 등록 중 무엇을 사용해야할까?

#### 정리
편리한 자동기능을 기본으로 사용
직접 등록하는 기술 지원 객체는 수동으로
다형성을 적극 활용하는 비즈니스 로직은 수동등록 고민

# 자동 등록을 기본으로 사용한다.
- 스프링이 나오고 나서 점점 자동 등록을 사용한다.
- 여러 애노테이션들로 계층에 맞추어 일반적인 애플리케이션 로직을 자동으로 스캔
	- `@Componet`, `@Controller` `@Service` `@Repository`

- 자동으로 빈 등록을 해도, [[OCP]], [[DIP]] 모두 지킬 수 있다.
	- 기껏해야 애노테이션 몇개 수정


# 수동등록을 사용하는 케이스

#### 애플리케이션 로직
###### 업무 로직 빈: 웹을 지원하는 컨트롤러, 핵심 비즈니스 로직이 있는 서비스 등등
- 보통 비즈니스 요구사항을 개발할 때 추가되거나 변경된다.
###### 기술 지원 빈: 기술적인 문제나, 공통 관심사 (AOP) 를 처리할 때
- 업무 로직을 지원하기 위한 하부 기술이나 공통 기술


- 업무 로직의 경우, 숫자도 매우 많고, 어느정도 유사한 패턴이 있다. 따라서 ==자동등록==을 사용하는 것이 유리하다. 또한 문제가 발생했을 때, 어디가 문제인지 명확하게 잘 들어난다.

- 기술 지원 로직의 경우, 업무 로직에 비해 매우 적고, 애플리케이션 전반에 걸쳐 광범위하게 영향을 미친다. 업무 로직과는 다르게 문제가 잘 들어나지 않는다. 따라서 가급적 수동 빈 등록을 사용해서 명확하게 들어내는 것이 좋다.


- 비즈니스 로직의 경우에도 다형성을 적극 활용할 때, 수동등록을 하여, 딱 보았을 때 이해가 되게 하는 것이 좋다. (혹은 특정 패키지에 같이 묶어두어 자동등록)