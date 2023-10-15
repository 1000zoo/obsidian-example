
[[Spring 컨테이너 설정 형식]]
# [[Spring 컨테이너]]가 생성되는 과정

```java
  
ApplicationContext ac = new AnnotationConfigApplicationContext(AppConfig.class);
```
- `ApplicationContext` 를 [[Spring 컨테이너]]라 한다.
- `ApplicationContext` 는 인터페이스이다.
- Spring 컨테이너는 XML 기반으로 만들거나, 애노테이션 기반의 자바 설정 클래스로 만들 수 있다.
	- 주로 후자의 경우를 많이 쓴다.

- 정확히는 `BeanFactory` 와 `ApplicationContext`로 구분하여 이야기한다.
- [[BeanFactory]]

---
## 스프링 컨테이너 생성
![[Pasted image 20230928210416.png]]

## 스프링 빈 등록
[[스프링 빈 조회]]
![[Pasted image 20230928210624.png]]
- `Bean`어노테이션이 붙은 메소드들을 저장한다. (\<Bean Name, Bean Object>)
- `Bean` 이름은 항상 다른 이름을 부여해야한다.

## Spring Bean 의존관계 설정
![[Pasted image 20230928210920.png]]
#### 참고
	스프링은 빈을 생성하고, 의존관계를 주입하는 단계가 나누어져있다.
자세한 내용은 [[의존관계 자동 주입]]

