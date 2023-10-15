# 기능
- getter setter 를 자동으로 알아서 만들어준다.
- toString 도 자동으로
- ==생성자가 필수가 아닐 때== `@RequiredArgsConstructor` 하나로 생성자를 생략할 수 있다.


### 예시 코드
```java
@Getter  
@Setter  
@ToString  
public class HelloLombok {  
  
    private String name;  
    private int age;  
  
    public static void main(String[] args) {  
        HelloLombok helloLombok = new HelloLombok();  
        helloLombok.setName("asd");  
  
        String name = helloLombok.getName();  
        System.out.println("name = " + name);  
        System.out.println("helloLombok = " + helloLombok);  
    }  
}
```
- getter & setter & toString 자동생성 예시

```java
@Component  
@RequiredArgsConstructor  
public class OrderServiceImpl implements OrderService {  
  
    private final MemberRepository memberRepository;  
    private final DiscountPolicy discountPolicy;
}
```
- 생성자가 제거된 모습
- 실제로는 생성자가 그대로 존재한다.

# 라이브러리 설치 방법
##### 프로젝트 생성 시
- `start.spring.io` 에서 프로젝트를 생성할때, 
- `Dependency` 에서 선택한다.

##### build.gradle 에서 추가.
- 자세한 내용은 구글링하면 될듯


### 인텔리제이 설정
![[Pasted image 20231002170850.png]]

