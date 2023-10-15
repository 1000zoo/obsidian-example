# 에러 원인
- [[Request Scope]]의 생명주기는, request가 날라오고 나서 부터이다.
- 그러나 스프링 컨테이너에서 등록을 할 당시에는 request가 날라오기 전이다.
- 따라서 아직 활성화 되지 않은 scope가 등록되려 해서 생기는 에러였다.
	- request 스코프 빈이 아직 생성되지 않았다.

# 에러 해결 방법
- [[Provider]]를 이용한다.
- [[프록시 방식]]을 이용한다.


# Code (Provider)
- `LogDemoController`
```java
@Controller
@RequiredArgsConstructor  
public class LogDemoController {  
  
    private final LogDemoService logDemoService;  
    private final ObjectProvider<MyLogger> myLoggerProvider;
    // 생략
}
```
- `LogDemoService`
```java
@Service  
@RequiredArgsConstructor  
public class LogDemoService {  
  
    private final ObjectProvider<MyLogger> myLoggerProvider;
}
```

- `MyLogger` 객체들을 `ObjectProvider`로 받는다.

