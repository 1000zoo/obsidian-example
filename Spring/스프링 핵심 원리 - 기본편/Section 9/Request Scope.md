- 웹 스코프는 웹 환경에서만 동작하기 때문에, [[웹 환경 추가]]가 필요하다.


# Request 예제
##### 예제 개발
동시에 여러 HTTP 요청이 오면, 정확히 어떤 요청이 남긴 로그인 지 구분하는 기능을 request 스코프를 이용하여 개발해보자.

### `MyLogger`
- request scope bean
```java
@Component  
@Scope(value = "request")  
public class MyLogger {  
  
    private String uuid;  
    private String requestURL;  
  
    public void setRequestURL(String requestURL) {  
        this.requestURL = requestURL;  
    }  
  
    public void log(String message) {  
        System.out.print("[" + uuid + "]");  
        System.out.print("[" + requestURL + "] ");  
        System.out.println(message);  
    }  
  
    @PostConstruct  
    public void init() {  
        uuid = UUID.randomUUID().toString();  
        System.out.print("[" + uuid + "] request scope bean create: " + this);  
    }  
  
    @PreDestroy  
    public void close() {  
        System.out.print("[" + uuid + "] request scope bean close: " + this);  
    }  
}
```

### `LogDemoController`

```java
@Controller  
@RequiredArgsConstructor  
public class LogDemoController {  
  
    private final LogDemoService logDemoService;  
    private final MyLogger myLogger;  
  
    @RequestMapping("log-demo")  
    @ResponseBody  
    public String logDemo(HttpServletRequest request) {  
        String requestURL = request.getRequestURL().toString();  
        myLogger.setRequestURL(requestURL);  
  
        myLogger.log("controller test");  
        logDemoService.logic("testId");  
        return "OK";  
    }  
}
```


### `LogDemoService`
```java
@Service  
@RequiredArgsConstructor  
public class LogDemoService {  
  
    private final MyLogger myLogger;  
  
    public void logic(String id) {  
        myLogger.log("serviceId = " + id);  
    }  
}
```

### 예제의 문제점
[[ScopeNotActiveException]]

### [[Provider]]로 해결한 뒤 결과
![[Pasted image 20231004120526.png]]
요청을 보낼 때 마다, 완전히 새로운 인스턴스가 생기게 된다.