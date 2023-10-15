# 목표
같은 의미를 가진 두 [[Instance]] (객체)를 Set에 중복없이 담고싶다.

# 방법
우선 두 메소드를 override 해주어야 한다.
- boolean equals(Object o)
- int hashCode()

#### 1. int hashCode()
고유값을 가질 수 있도록, 가지고 있는 속성들을 해시화한다.
```java 
@Override  
public int hashCode() {  
    return Objects.hash(title, artistName);  
}
```
### 2. boolean equals(Object o)
자체적인 주소값이 같은지 확인해주고,
같은 클래스인지 확인해주고
같은 hash 값을 같는 지 확인해준다.
```java
@Override  
public boolean equals(Object o) {  
    if (this == o) return true;  
    if (o == null || getClass() != o.getClass()) return false;
    return this.hashCode() == o.hashCode();  
}
```

`hash 값의 비교는, 간혹 서로 다른 객체가 같은 해시값을 갖는 경우가 있으므로, 각 객체들의 속성을 직접 비교해 주는 것이 옳다. 하지만 코드의 간략화를 위해 일단 해시값으로 비교를 함.`