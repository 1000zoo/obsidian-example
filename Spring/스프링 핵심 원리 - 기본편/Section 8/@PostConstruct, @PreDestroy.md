# 결론
이 방법을 사용하면 된다.
- 최신 스프링에서 권장하는 방법
- 애노테이션 하나만 붙히면 된다.
- javax 패키지이다.
	- 스프링에 종속적인 기술이 아니다.

## 예시 코드
```java
@PostConstruct  
public void init() {  
    System.out.println("NetworkClient.init");  
    connect();  
    call("초기화 연결 메시지");  
}  
  
@PreDestroy  
public void close() {  
    System.out.println("NetworkClient.close");  
    disconnect();  
}
```

### 결과
![[Pasted image 20231004062739.png]]

## 단점
- 코드를 고칠 수 없는 외부 라이브러리에는 적용하지 못한다.