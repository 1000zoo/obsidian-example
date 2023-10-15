
[[Spring 컨테이너]] <= 변경된 `AppConfig`
# 코드
```java
public class AppConfig {  
  
    public MemberService memberService() {  
        return new MemberServiceImpl(new MemoryMemberRepository());  
    }  
  
    public OrderService orderService() {  
        return new OrderServiceImpl(  
                new MemoryMemberRepository(),  
                new FixDiscountPolicy()  
        );  
    }  
}
```

`AppConfig`를 위와 같이 짜주고, 각각의 구현체들을 `AppConfig`를 통해서 구현하게 되면, 각 구현체들은 더이상 다른 구현체에 의존하지 않을 수 있다.

- `AppConfig`는 실제 동작에 필요한 구현 객체를 생성한다.
- `AppConfig`는 생성한 객체 인스턴스의 레퍼런스를 생성자를 통해서 주입해준다.

더 이상 `MemberServiceImpl` 은 `MemoryMemberRepository` 와 [[의존관계]]에 있지 않다.
[[의존관계]] 에 대한 고민은 외부에 맡기고, **실행에만 집중한다.**

---

### 클래스 다이어그램
![[Pasted image 20230928131536.png]]
- [[DIP]] 완성: `MemberServiceImpl`은 이제 `MemberRepository` 인 추상에만 의존하면 된다.!!
=> [[DI]]

# 테스트
- beforeEach 를 통해 매 테스트 전에 생성해준다.
```java
public class MemberServiceTest {  
  
    MemberService memberService;  
  
    @BeforeEach  
    void beforeEach() {  
        AppConfig appConfig = new AppConfig();  
        memberService = appConfig.memberService();  
    }  
  
    @Test  
    void join() {  
        // given  
        Member member = new Member(1L, "천지우", Grade.VIP);  
  
        // when  
        memberService.join(member);  
        Member findMember = memberService.findMember(1L);  
  
        // then  
        Assertions.assertThat(member).isEqualTo(findMember);  
    }  
}
```

# 정리
- 관심사를 확실하게 분리하였다.
- AppConfig 는 공연 기획자이다.
- 이제 각 구현체들은, 담당 기능을 실행만 책임지면 된다.
- `OrderServiceImpl`은 기능을 실행하기만 하면 된다.
- [[사용영역과 구성영역]] 이 구분되었다.
- [[AppConfig Refectoring]]을 통해, 그 안에서도 확실한 역할을 부여해주었다.