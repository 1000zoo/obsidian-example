# 요약
BeanDefinition 으로 스프링 빈 메타정보를 추상화 한다.
# BeanDefinition
- 스프링이 다양한 설정 형식을 지원하게 해주는 인터페이스
- 자바 코드든, XML 코드든 일단 읽고 `BeanDefinition`을 만들면 된다.
- 빈 설정 메타정보라 한다.
- @Bean , \<bean>  당 각각 하나씩 메타정보가 생성된다.
- [[Spring 컨테이너]]는 이 메타정보를 기반으로 스프링 빈을 생성한다.

![[Pasted image 20230929004130.png]]

# 메타정보 확인하기
### 테스트 코드
```java
AnnotationConfigApplicationContext ac = new AnnotationConfigApplicationContext(AppConfig.class);  
  
@Test  
@DisplayName("빈 설정 메타정보 확인")  
void findApplicationBean() {  
    String[] beanDefinitionNames = ac.getBeanDefinitionNames();  
    for (String beanDefinitionName : beanDefinitionNames) {  
        BeanDefinition beanDefinition = ac.getBeanDefinition(beanDefinitionName);  
  
        if (beanDefinition.getRole() == BeanDefinition.ROLE_APPLICATION) {  
            System.out.println("beanDefinitionName = " + beanDefinitionName +  
                    " beanDefinition = " + beanDefinition  
            );  
        }  
    }  
}
```
 
### 결과 보는 법
![[Pasted image 20230929004908.png]]