- `ObjectFactory`의 하위 인터페이스
- `ObjectFactory`에서 편의기능이 더 추가됨
## 기능
- 핵심 기능은, 스프링 컨테이너에 조회하는 것을 대신해주는 것.
- 프로토타입 스코프에만 국한된 것은 아님
- 별도의 라이브러리 설치가 필요하지 않다.
- 하지만 스프링에 의존한다.

### 사용예시
```java
@Scope("singleton")  
static class ClientBean {  
    @Autowired  
    private ObjectProvider<PrototypeBean> prototypeBeanProvider;  
  
    public int logic() {  
        PrototypeBean prototypeBean = prototypeBeanProvider.getObject();  
  
        prototypeBean.addCount();  
        return prototypeBean.getCount();  
    }  
}
```
- `ObjectProvider`가 PrototypeBean의 인스턴스를 알아서 잘 찾아와준다.
