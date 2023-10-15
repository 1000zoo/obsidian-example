	잘 사용되고 있지는 않지만, 필요하다면 아래의 링크에서 자세한 내용 확인
[Link](https://spring.io/projects/spring-framework)

# Code
```xml
<?xml version="1.0" encoding="UTF-8"?>  
    <beans xmlns="http://www.springframework.org/schema/beans"  
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"  
       xsi:schemaLocation="http://www.springframework.org/schema/beans http://www.springframework.org/schema/beans/spring-beans.xsd">  
  
    <bean id="memberService" class="zoo.springbasic.member.MemberServiceImpl">  
        <constructor-arg name="memberRepository" ref="memberRepository" />  
    </bean>  
    <bean id="memberRepository" class="zoo.springbasic.member.MemoryMemberRepository" />  
  
    <bean id="orderService" class="zoo.springbasic.order.OrderServiceImpl">  
        <constructor-arg name="memberRepository" ref="memberRepository" />  
        <constructor-arg name="discountPolicy" ref="discountPolicy" />  
    </bean>  
    <bean id="discountPolicy" class="zoo.springbasic.discount.RateDiscountPolicy" />  
</beans>
```

## 대응
- `@Bean`: `<bean id="{method명} class="{클래스의 경로}"`
- 파라미터: `<contructor-arg name="{함수명?}" ref={"상대경로?"}`

# 테스트
### Code
```java
@Test  
void xmlAppContext() {  
    ApplicationContext ac = new GenericXmlApplicationContext("appConfig.xml");  
    MemberService memberService = ac.getBean("memberService", MemberService.class);  
    assertThat(memberService).isInstanceOf(MemberService.class);  
}
```

### Result
![[Pasted image 20230929000514.png]]