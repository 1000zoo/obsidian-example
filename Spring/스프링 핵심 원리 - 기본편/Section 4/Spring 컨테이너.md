- AppConfig를 스프링 컨테이너에 등록하면, 컨테이너가 스프링 빈을 찾아서 사용한다.
- @Bean이 붙은 메소드 명을 스프링 빈의 이름로 사용한다.
- @Bean(name="") 로 이름을 변경 가능하다.

# [[AppConfig]]
```java
@Configuration  
public class AppConfig {  
  
    @Bean  
    public MemberService memberService() {}  
  
    @Bean  
    public OrderService orderService() {}  
  
    @Bean  
    public DiscountPolicy getDiscountPolicy() {}  
      
    @Bean  
    public MemberRepository getMemberRepository() {}  
}
```


- class에 `@Configuration` 어노테이션을, method에 `@Bean` 을 붙여준다.



# AppConfig 불러오는 부분

### 이 전 Test 코드
```java
public class MemberApp {  
  
    public static void main(String[] args) {  
        AppConfig appConfig = new AppConfig();  
        MemberService memberService = appConfig.memberService();  
        Member member = new Member(1L, "천지우", Grade.VIP);  
        memberService.join(member);  
  
        Member findMember = memberService.findMember(1L);  
        System.out.println("member = " + member.getName());  
        System.out.println("findMember = " + findMember.getName());  
    }  
}
```

### 수정 후
```java
public class MemberApp {  
  
    public static void main(String[] args) {  
        ApplicationContext applicationContext = new AnnotationConfigApplicationContext(AppConfig.class);  
        MemberService memberService = applicationContext.getBean("memberService", MemberService.class);  
  
        Member member = new Member(1L, "천지우", Grade.VIP);  
        memberService.join(member);  
  
        Member findMember = memberService.findMember(1L);  
        System.out.println("member = " + member.getName());  
        System.out.println("findMember = " + findMember.getName());  
    }  
}
```
- AppConfig 를 바로 불러오는 것이 아닌, `AnnotationConfigApplicationContext` 의 `getBean` 메서드를 통해 불러온다.
- `AnnotationConfigApplicationContext` <= 여기가 스프링 컨테이너라 할 수 있다.

### 쌤 더 복잡해진 거 같은데요???
스프링 컨테이너의 장점 => 어마어마한 장점이 있다.
