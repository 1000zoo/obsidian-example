# Dependency Lookup
- 의존관계를 외부에서 주입받는 [[DI]]와 상반되는 개념
- 직접 필요한 의존관계를 찾는다.

#### 간단한 DL 예시
```java
@Scope("singleton")  
static class ClientBean {  
	@Autowired
	private ApplicationContext ac;
  
    public int logic() {  
	    PrototypeBean prototypeBean = ac.getBean(PrototypeBean.class);
        prototypeBean.addCount();  
        return prototypeBean.getCount();  
    }  
}
```
#### 위 예시의 단점
- 이렇게 `ApplicationContext` 전체를 주입받게 되면, 스프링 컨테이너에 종속적인 코드가 된다.
- 단위 테스트도 어려워진다.

#### 스프링에서 제공하는 DL
[[ObjectProvider]]
`@Lookup` -> 잘 쓰진않음
