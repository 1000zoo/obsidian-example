# 요약
- ApplicationContext 의 상위 인터페이스
- ApplicationContext 는 BeanFactory와 더불어 부가기능이 포함된 인터페이스
- BeanFactory 나 ApplicationContext를 [[Spring 컨테이너]]라 한다.

![[Pasted image 20230928222701.png]]

# BeanFactory
- `ApplicationContext` 의 상위 인터페이스
- [[Spring 컨테이너]] 의 최상위 인터페이스이다.
- 스프링 빈을 관리하고 조회하는 역할을 담당한다.
- `getBean()` 제공

# ApplicationContext 와의 차이
![[Pasted image 20230928222946.png]]
- [[ISP]] 원칙을 지켜, 기능마다 인터페이스를 나누었고,
- `ApplicationContext`는 해당 기능들을 상속받는 하위 인터페이스.

### 각 인터페이스 별 기능
###### MessageSource
- 메시지 소스를 활용한 국제화 기능
	- 한국에선 한국어, 영어권에서는 영어로 출력
	- 파일을 여러개로 분리해놓아서 
###### EnvironmentCapable
- 환경변수
	- 로컬, 개발, 운영등을 구분해서 처리
###### ApplicationEventPublisher
- 애플리케이션 이벤트
	- 이벤트를 발행하고 구독하는 모델을 편리하게 지원
###### ResourceLoader
- 파일, 클래스패스, 외부 등에서 리소스를 편하게 조회