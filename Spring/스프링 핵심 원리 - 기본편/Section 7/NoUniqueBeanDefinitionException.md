# 에러 원인
등록된 빈이 2개 이상일 경우 발생하는 에러

```java
@Component  
public class FixDiscountPolicy implements DiscountPolicy {}
// ---
@Component  
public class RateDiscountPolicy implements DiscountPolicy{}
```
- 같은 추상화의 구현체 두 클래스를 `@Component` 애노테이션을 붙이면 에러가 발생한다.
- discountPolicy 라는 이름으로 두 개가 매칭되기 때문

# 해결 방법

### [[@Autowired]]  필드명 매칭
중복되는 필드명을 변경해준다.
```java
@Autowired  
public OrderServiceImpl(MemberRepository memberRepository, DiscountPolicy fixDiscountPolicy) {  
    this.memberRepository = memberRepository;  
    this.discountPolicy = fixDiscountPolicy;  
}
```

- 타입 매칭의 결과가 2 개 이상일 때, 필드명과 파라미터 명으로 빈 이름을 매칭
### @Qualifier
- 주입 시 추가적인 방법을 제공하는 것
- 빈 이름을 변경하는 것은 아니다.
- 만약 `@Qualifier` 로 지정된 빈을 찾지 못하면, 해당 이름의 빈을 가져오긴 한다.
	- 하지만 `@Qualifier` 는 `Qualifier` 를 찾는 용도로만 사용하자.
	- 빈 이름도 없으면 `NoSuchBeanDefinitionException` 발생

```java
@Component  
@Qualifier("mainDiscountPolicy")  
public class RateDiscountPolicy implements DiscountPolicy{}

// ----
public OrderServiceImpl(MemberRepository memberRepository, @Qualifier("mainDiscountPolicy") DiscountPolicy discountPolicy) {  
    this.memberRepository = memberRepository;  
    this.discountPolicy = discountPolicy;  
}
```

### @Primary
- `@Autowired` 시에 여러 빈이 매칭되면 `@Primary`가 우선권을 가진다.


## 두 개 모두 필요한 경우에는???
[[조회한 빈이 모두 필요할 때]]