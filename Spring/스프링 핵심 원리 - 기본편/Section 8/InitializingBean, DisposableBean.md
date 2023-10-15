
# 요약
- 해당 방식은 스프링 초기에 나온 방법들이다.
- 더 나은 방법들이 있어서 잘 사용하지 않는다.

## 사용 예시
```java
public class NetworkClient implements InitializingBean, DisposableBean {
// 기존 코드
    @Override  
    public void afterPropertiesSet() throws Exception {  
        connect();  
        call("초기화 연결 메시지");  
    }  
  
    @Override  
    public void destroy() throws Exception {  
        disconnect();  
    }  
}
```
- `afterPropertiesSet`: `InitializingBean` 의 메서드
	- 생성자 생성 및 의존관계 주입 후에 호출되는 메서드
- `destroy`: `DisposableBean`의 메서드
	- `ac.close()` 호출 시, 객체가 사라지기 전에 호출됨
![[Pasted image 20231004061144.png]]

## 단점
- 스프링 전용 인터페이스라, 해당 코드가 스프링 전용 인터페이스에 의존한다.
- 초기화, 소멸 메서드의 이름을 변경할 수 없다.
