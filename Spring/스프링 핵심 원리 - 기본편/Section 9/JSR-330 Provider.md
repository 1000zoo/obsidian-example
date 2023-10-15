- `javax.inject.Provider`라는 자바 표준을 사용하는 방법

- gradle에 라이브러리를 추가해야한다.

## 사용 예시
```java
@Scope("singleton")  
static class ClientBean {  
    @Autowired  
    private Provider<PrototypeBean> prototypeBeanProvider;  
  
    public int logic() {  
        PrototypeBean prototypeBean = prototypeBeanProvider.get();  
  
        prototypeBean.addCount();  
        return prototypeBean.getCount();  
    }  
}
```
- `provider`의 `get()`을 호출하면 내부에서는 스프링 컨테이너를 통해 해당 빈을 찾아서 반환한다. 
	- [[DL]]
- 자바 표준이고 기능이 단순하여 단위테스트를 만들기 좋다.
- 스프링이 아닌 다른 컨테이너에서도 사용할 수 있다.

## 메뉴얼
![[Pasted image 20231004101504.png]]
