- 디폴트: 싱글톤

### 싱글톤 스코프
```java
@Test  
void singletonBeanFind() {  
    AnnotationConfigApplicationContext ac = new AnnotationConfigApplicationContext(SingletonBean.class);  
  
    SingletonBean singletonBean1 = ac.getBean(SingletonBean.class);  
    SingletonBean singletonBean2 = ac.getBean(SingletonBean.class);  
  
    Assertions.assertThat(singletonBean1).isSameAs(singletonBean2);  
  
    ac.close();  
}  
  
@Scope("singleton")  
static class SingletonBean {  
    @PostConstruct  
    public void init() {  
        System.out.println("SingletonBean.init");  
    }  
  
    @PreDestroy  
    public void destroy() {  
        System.out.println("SingletonBean.destroy");  
    }  
}
```

![[Pasted image 20231004073814.png]]

### [[프로토타입 스코프]]
```java  
    @Test  
    void prototypeBeanFind() {  
  
        AnnotationConfigApplicationContext ac = new AnnotationConfigApplicationContext(PrototypeBean.class);  
  
        PrototypeBean prototypeBean1 = ac.getBean(PrototypeBean.class);  
        PrototypeBean prototypeBean2 = ac.getBean(PrototypeBean.class);  
  
        Assertions.assertThat(prototypeBean1).isNotSameAs(prototypeBean2);  
  
        ac.close();  
    }  
  
    @Scope("prototype")  
    static class PrototypeBean {  
  
        @PostConstruct  
        public void init() {  
            System.out.println("PrototypeBean.init");  
        }  
  
        @PreDestroy  
        public void destroy() {  
            System.out.println("PrototypeBean.destroy");  
        }  
    }
```
![[Pasted image 20231004074240.png]]
- 초기화 메서드 (`init()`) 이 두 번 실행된다.
- 소멸 메서드 (`destroy()`)가 실행되지 않는다.
	- 필요시 직접 호출해야 한다.
		- ex) `prototypeBean1.destroy()`
