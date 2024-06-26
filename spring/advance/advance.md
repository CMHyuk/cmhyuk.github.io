### 쓰레드 로컬
* 쓰레드 로컬은 해당 쓰레드만 접근할 수 있는 특별한 저장소  

**ThreadLocal 사용법**  
값 저장: `ThreadLocal.set(xxx)`  
값 조회: `ThreadLocal.get()`  
값 제거: `ThreadLocal.remove()`

**쓰레드 로컬의 값을 사용 후 제거하지 않고 그냥 두면 WAS(톰캣)처럼 쓰레드 풀을 사용하는 경우에 심각한 문제가 발생**

* 저장 요청
1. 사용자A가 저장 HTTP를 요청했다.
2. WAS는 쓰레드 풀에서 쓰레드를 하나 조회한다.
3. 쓰레드 `thread-A` 가 할당되었다.
4. `thread-A` 는 `사용자A` 의 데이터를 쓰레드 로컬에 저장한다.
5. 쓰레드 로컬의 `thread-A` 전용 보관소에 `사용자A` 데이터를 보관한다.

* 저장 요청 종료
1. 사용자A의 HTTP 응답이 끝난다.
2. WAS는 사용이 끝난 `thread-A` 를 쓰레드 풀에 반환한다. 쓰레드를 생성하는 비용은 비싸기 때문에 쓰레드를 제거하지 않고, 보통 쓰레드 풀을 통해서 쓰레드를 재사용한다.
3. `thread-A` 는 쓰레드풀에 아직 살아있다. 따라서 쓰레드 로컬의 `thread-A` 전용 보관소에 `사용자A` 데이터도 함께 살아있게 된다.

-> 다른 사용자가 사용자 A의 데이터를 확인하게 되는 문제가 발생함

### 템플릿 메서드 패턴

- 장점
    - 핵심 기능과 부가기능을 나눌 수 있음
- 단점
    - 기존 로직을 건드려야함

### 프록시 패턴 vs 데코레이터 패턴

프록시 패턴 : 접근 제어가 목적  
데코레이터 패턴 : 새로운 기능 추가가 목적

### 프록시 패턴

- 장점
    - 기존 로직을 건들지 않아도 됨
- 단점
    - 적용 대상이 100개면 프록시 클래스도 100개 만들어야 함

### 인터페이스 기반 프록시 vs 클래스 기반 프록시

- 인터페이스가 없어도 클래스 기반으로 프록시를 생성 가능
- 클래스 기반 프록시는 해당 클래스에만 적용 가능, 인터페이스 기반 프록시는 인터페이스만 같으면 모든 곳에 적용 가능

### 클래스 기반 프록시 제약

- 부모 클래스의 생성자를 호출해야함
- 클래스에 final 키워드가 붙으면 상속이 불가능
- 메서드에 final 키워드가 붙으면 해당 메서드를 오버라이딩 x

### 리플렉션 사용하지 말자

애플리케이션을 동적으로 만들 수 있지만 컴파일 단계에서 오류를 잡아내지 못함

`getMethod("callA")` 을 실수로 `getMethod("callZ")` 로 해도 컴파일 오류 x

프로그래밍 언어가 발달하면서 타입 정보를 기반으로 컴파일 시점에 오류를 잡아준 덕분에 편했는데, 리플렉션은 그것을 역행하는 방식

JDK 동적 프록시는 인터페이를 구현 (implements) CGLIB은 구체 클래스를 상속(extends)

### CGLIB 제약

클래스 기반 프록시는 상속을 사용

- 부모 클래스의 생성자를 체크 -> CGLIB은 자식 클래스를 동적으로 생성하기 때문에 기본 생성자가 필요
- 클래스에 `final`키워드가 붙으면 상속 불가능 -> CGLIB에선 예외가 발생
- 메서드에 `final` 키워드가 붙으면 해당 메서드를 오버라이딩 할 수 없음 -> CGLIB에서는 프록시 로직이 동작 x

### 프록시 팩토리
- 인터페이스가 있는 경우에 JDK 동적 프록시를 적용하고, 그렇지 않은 경우에 CGLIB을 적용하려면?
  - 프록시 팩토리를 이용해 둘 대신에 `Adivce` 를 사용하면 됨

```java
Target target = new Target();
ProxyFactory proxyFactory = new ProxyFactory(tartget);
proxyFactory.addAdvice(new TimeAdvice());
proxyFactory.getProxy();
// proxyFactory.setProxyTargetClass(true) 인터페이스가 있어도 무조건 CGLIB
```

**포인트컷**( `Pointcut` )
* 어디에 부가 기능을 적용할지, 어디에 부가 기능을 적용하지 않을지 판단하는 필터링 로직, 주로 클래스와 메서드 이름으로 필터링 이름 그대로 어떤 포인트(Point)에 기능을 적용할지 하지 않을지 잘라서(cut) 구분

**어드바이스**( `Advice` )  
* 이전에 본 것 처럼 프록시가 호출하는 부가 기능, 단순하게 프록시 로직이라 생각하면 됨

**어드바이저**( `Advisor` )  
* 단순하게 하나의 포인트컷과 하나의 어드바이스를 가지고 있는 것, 쉽게 이야기해서 **포인트컷1 + 어드바이스1**
* 정리하면 부가 기능 로직을 적용해야 하는데, 포인트컷으로 어디에? 적용할지 선택하고, 어드바이스로 어떤 로직을 적용할지 선택하는 것, 그리고 어디에? 어떤 로직?을 모두 알고 있는 것이 **어드바이저**

**AOP 적용 수 만큼 프록시가 생성된다고 착각하지만 프록시는 하나만 만들고, 하나의 프록시에 여러 어드바이저를 적용함**

### 빈 후처리기
스프링이 빈 저장소에 등록할 목적으로 생성한 객체를 빈 저장소에 등록하기 직전에 조작하고 싶다면 빈 후처리기를 사용하면 됨

**빈 등록 과정**  
**1. 생성:** 스프링 빈 대상이 되는 객체를 생성한다. ( `@Bean` , 컴포넌트 스캔 모두 포함)  
**2. 전달:** 생성된 객체를 빈 저장소에 등록하기 직전에 빈 후처리기에 전달한다.  
**3. 후 처리 작업:** 빈 후처리기는 전달된 스프링 빈 객체를 조작하거나 다른 객체로 바뀌치기 할 수 있다.  
**4. 등록:** 빈 후처리기는 빈을 반환한다. 전달 된 빈을 그대로 반환하면 해당 빈이 등록되고, 바꿔치기 하면 다른 객 체가 빈 저장소에 등록된다.

### 자동 프록시 생성기의 작동 과정  
**1. 생성:** 스프링 빈 대상이 되는 객체를 생성한다. ( `@Bean` , 컴포넌트 스캔 모두 포함)  
**2. 전달:** 생성된 객체를 빈 저장소에 등록하기 직전에 빈 후처리기에 전달한다.  
**3-1. Advisor 빈 조회:** 스프링 컨테이너에서 `Advisor` 빈을 모두 조회한다.  
**3-2. @Aspect Advisor 조회:** `@Aspect` 어드바이저 빌더 내부에 저장된 `Advisor` 를 모두 조회한다.  
**4. 프록시 적용 대상 체크:** 앞서 3-1, 3-2에서 조회한 `Advisor` 에 포함되어 있는 포인트컷을 사용해서 해당 객 체가 프록시를 적용할 대상인지 아닌지 판단한다. 이때 객체의 클래스 정보는 물론이고, 해당 객체의 모든 메서드 를 포인트컷에 하나하나 모두 매칭해본다. 그래서 조건이 하나라도 만족하면 프록시 적용 대상이 된다. 예를 들어 서 메서드 하나만 포인트컷 조건에 만족해도 프록시 적용 대상이 된다.  
**5. 프록시 생성:** 프록시 적용 대상이면 프록시를 생성하고 프록시를 반환한다. 그래서 프록시를 스프링 빈으로 등 록한다. 만약 프록시 적용 대상이 아니라면 원본 객체를 반환해서 원본 객체를 스프링 빈으로 등록한다.  
**6. 빈 등록:** 반환된 객체는 스프링 빈으로 등록된다.