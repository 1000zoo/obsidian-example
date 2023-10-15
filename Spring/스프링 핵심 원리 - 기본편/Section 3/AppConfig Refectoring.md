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

리팩토링 이후
```java
public class AppConfig {  
  
    public MemberService memberService() {  
        return new MemberServiceImpl(getMemberRepository());  
    }  
  
    public OrderService orderService() {  
        return new OrderServiceImpl(getMemberRepository(), getDiscountPolicy());  
  
    }  
    
    private DiscountPolicy getDiscountPolicy() {  
        return new FixDiscountPolicy();  
    }  
  
    private MemberRepository getMemberRepository() {  
        return new MemoryMemberRepository();  
    }  
}
```

- 리팩토링 이후에, 역할들이 나오고, 그에대한 구현이 명확하게 보여진다.
- 또한 `new MemoryMemberRepository()` 중복이 사라졌다.
- 구현을 변경하고 싶다면, `get~()`  메소드의 리턴만 변경해주면 된다.