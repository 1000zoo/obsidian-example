# 직접 만드는 이유
```java
@Component  
@Qualifier("mainDiscountPolicy")  
public class RateDiscountPolicy implements DiscountPolicy{}
```
- 이렇게 할 경우, `mainDiscountPolicy` 의 철자가 틀릴 경우에, 컴파일 에러가 나는 것이 아닌 런타임 에러가 발생하기 때문에, 에러수정에 머리가 아플 수 있기 때문.

# 방법
```java
@Target({ElementType.FIELD, ElementType.METHOD, ElementType.PARAMETER, ElementType.TYPE, ElementType.ANNOTATION_TYPE})  
@Retention(RetentionPolicy.RUNTIME)  
@Inherited  
@Documented  
@Qualifier("mainDiscountPolicy")  
public @interface MainDiscountPolicy {  
  
}
```
- 이런 식으로 만들면 된다.
- 사용하는 법은 `@Qualifier("mainDiscountPolicy")` 가 들어가던 자리에
- `@MainDiscountPolicy` 를 붙히면 된다.

```java
@Autowired  
public OrderServiceImpl(MemberRepository memberRepository, @MainDiscountPolicy DiscountPolicy discountPolicy) {  
    this.memberRepository = memberRepository;  
    this.discountPolicy = discountPolicy;  
}
```
- 요런식으로
- 


### 웬만하면 `@Primary` 사용
- 너무 무분별하게 사용하지 말자!