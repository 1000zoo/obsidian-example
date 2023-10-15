- 스프링 컨테이너는 싱글톤 레지스트리다.
- 따라서 스프링 빈이 싱글톤이 되도록 보장해주어야한다.
	- 이미 불러온 클래스라면, 다시 불러오지 않는다.


# 테스트
우선 `AppConfig` 빈의 클래스를 출력해보자.

```java
@Test  
void configurationDeep() {  
    ApplicationContext ac = new AnnotationConfigApplicationContext(AppConfig.class);  
    AppConfig bean = ac.getBean(AppConfig.class);  
  
    System.out.println("bean.getClass() = " + bean.getClass());  
}
```
### 출력결과
```
bean.getClass() = class zoo.springbasic.AppConfig$$EnhancerBySpringCGLIB$$6b226f66
```

- 순수한 클래스라면 `zoo.springbasic.AppConfig` 까지만 출력이 되어야한다.
	- `@Configuration` 을 지우면, 순수한 클래스가 출력된다.
	- 지워도 빈이 잘 등록이 된다.
	- 하지만, 싱글톤이 깨지게된다.
		- 또한 스프링 컨테이너가 관리하지 않는다.
- 즉 내가 만든 클래스가 아니라, 스프링 빈을 등록하는 과정속에서 생겨난 클래스이다.
	- 스프링이 CGLIB 라는 바이트코드 조작 라이브러리를 사용해서 AppConfig 클래스를 상속받는 임의의 다른 클래스를 만들고, 그 클래스를 스프링 빈으로 등록한다.

![[Pasted image 20230929030350.png]]

