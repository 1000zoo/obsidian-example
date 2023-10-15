- [[싱글톤 패턴]]을 위해서 존재한다.

# 이상한 점
- [[AppConfig]] 에서 `new MemoryMemberRepository`가 두 번 호출된다.
	- `memberService` 에서 한 번, `orderService` 에서 한 번.
- 문제가 없을것인가?

### 테스트
```java
@Test  
@DisplayName("Configuration singleton 이 지켜지는지")  
void configurationTest() {  
    ApplicationContext ac = new AnnotationConfigApplicationContext(AppConfig.class);  
  
    MemberServiceImpl memberService = ac.getBean("memberService", MemberServiceImpl.class);  
    OrderServiceImpl orderService = ac.getBean("orderService", OrderServiceImpl.class);  
    MemberRepository memberRepository = ac.getBean("getMemberRepository", MemberRepository.class);  
  
    MemberRepository memberRepository1 = memberService.getMemberRepository();  
    MemberRepository memberRepository2 = orderService.getMemberRepository();  
  
    Assertions.assertThat(memberRepository).isSameAs(memberRepository1);  
    Assertions.assertThat(memberRepository1).isSameAs(memberRepository2);  
}
```

#### 결과
- `memberService` 에서 불러오나, `orderService`에서 불러오나, `getMemberRepository` 에서 직접 불러오나, 다 똑같은 Instance가 호출된다.

- 각자 한 번씩만 호출된다.


### 그러는 이유는?
[[@Configuration과 바이트코드 조작의 마법]]