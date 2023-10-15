[[의존관계 자동 주입]]

```java
@Autowired  
public MemberServiceImpl(MemberRepository memberRepository) {  
    this.memberRepository = memberRepository;  
}
```
- `MemberRepository` 의 구체화 클래스 중, @Component 애노테이션이 붙은 클래스를 자동으로 주입해준다.