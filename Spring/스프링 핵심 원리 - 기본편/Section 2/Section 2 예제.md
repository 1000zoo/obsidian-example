
## 비즈니스 요구사항과 설계

- 회원
	- 회원 가입 및 조회
	- 일반, VIP 두 가지 등급
	- 회원 데이터는 자체 DB or 외부 시스템 연동 (미확정)
		- 인터페이스로 구현
- 주문과 할인 정책
	- 회원은 상품을 주문할 수 있다.
	- 회원 등급에 따라 할인 정책을 적용
	- 할인 정책은 모든 VIP 는 1000원 할인 (나중에 변경 될 수 있다.)
		- 인터페이스로 구현

## 핵심
인터페이스를 우선 만들고, 구현체를 언제든지 갈아끼울 수 있도록 설계 => ([[다형성]] 이용)


## 회원 도메인 설계
![[Pasted image 20230928013657.png]]

- 메모리 회원 저장소: 개발 테스트 단계에서 사용될 저장소의 구현체
- DB 회원 저장소 & 외부 회원 저장소 : 실제 서비스에서 사용될 예정

## 회원 클래스 다이어그램
- 실제 서버를 실행하지 않고, 클래스 계층구조를 볼 수 있는 그림
![[Pasted image 20230928013847.png]]

## 회원 객체 다이어그램
- 클라이언트가 실제 사용하는 메모리 객체
![[Pasted image 20230928014259.png]]
- 회원 서비스: MemberServiceImpl


## 설계상의 문제점
#### [[OCP]] 원칙 준수 X
#### [[DIP]] 준수 X
`MemberServiceImpl.java` 에서
```java
private final MemberRepository memberRepository = new MemoryMemberRepository();
```
구체화 (MemoryMemberRepository)를 의존하고 있다.

- 의존관계가 인터페이스 뿐 아니라 구현까지 모두 의존하고 있다.
- 추후에 다시 설명


## 주문과 할인 도메인 전체
![[Pasted image 20230928021225.png]]
- 역할을 먼저 만들고, 구현은 나중에 생각한다.
- 구현체가 바뀌더라도, 역할들의 협력관계를 그대로 재사용 할 수 있다.

#### [[SRP]] 원칙이 지켜진 부분
```java
public class OrderServiceImpl implements OrderService {  
  
    private final MemberRepository memberRepository = new MemoryMemberRepository();  
    private final DiscountPolicy discountPolicy = new FixDiscountPolicy();  
  
    @Override  
    public Order createOrder(Long memberId, String itemName, int itemPrice) {  
        Member member = memberRepository.findById(memberId);  
        int discountPrice = discountPolicy.discount(member, itemPrice);  
  
        return new Order(memberId, itemName, itemPrice, discountPrice);  
    }  
}
```
- `OrderServiceImpl 이 할인과 관련된 내용을 알지 못한다.
- 즉, 할인 내용을 변경할 때, Order 부분을 변경할 필요 없음.
- 단일책임원칙을 잘 지키고 설계되어있다.
- discount 에는 회원의 등급만 들어가도 되지만, 추후의 확장성을 고려할 필요가 있다.

[[예제 2 테스트 코드]]