### 객체로 추상화하기
* 비공개 필드, 비공개 로직
* 공개 메서드 선언부를 통해 외부 세계와 소통
  * 각 메서드의 기능은 객체의 책임을 드러내는 창구
* 객체의 책임이 나뉨에 따라 객체 간 협력이 발생

### 객체가 제공하는 것
* 절차 지향에서 잘 보이지 않았던 개념을 가시화
* 관심사가 한 군데로 모이기 때문에, 유지보수성 증가
  * 객체 내부에서 객체가 가진 데이터의 유효성 검증 책임을 가질 수 있다.
* 여러 객체를 사용하는 입장에서는, 구체적인 구현에 신경 쓰지 않고 보다 높은 추상화 레벨에서 도메인 로직을 다룰 수 있다.

### 새로운 객체를 만들 때 주의할 점
* **1개의 관심사로 명확하게 책임이 정의되었는지 확인하기**
  * 메서드를 추상화할 때와 비슷하다.
  * 객체를 만듦으로써 외부 세계와 어떤 소통을 하려고 하는지 생각해보자.
* **생성자, 정적 팩토리 메서드에서 유효성 검증이 가능하다.**
  * 도메인에 특화된 검증 로직이 들어갈 수 있다.
* **setter 사용 자제**
  * 데이터는 불변이 최고다. 변하는 데이터더라도 객체가 핸들링할 수 있어야 한다.
  * 객체 내부에서 외부 세계의 개입 없이 자체적인 변경/가공으로 처리할 수 있는지를 확인
  * 만약 외부에서 가지고 있는 데이터로 데이터 변경 요청을 해야 하는 경우, `set~`이라는 단순한 이름보다는 `update~`같이 의도를 드러내는 네이밍을 고려하자.
* **getter도 처음에는 사용자제. 반드시 필요한 경우에 추가하기**
  * 외부에서 객체 내 데이터가 필요하다고 getter를 남발하는 것은 무례한 행동이다!
* **객체에 메시지를 보내라!**
    
```java
Person person = new Persion();

// (1)
if (person.get지갑().get신분증().findAge() >= 19) {
    pass();
}

// (2)
if (person.isAgeGreaterThanOrEqualTo(19)) {
    pass();    
}
```

* 필드의 수는 적을수록 좋다.
  * 불필요한 데이터가 많을수록 복잡도가 높아지고 대응할 변화가 많아진다.
  * 필드 A를 가지고 계산할 수 있는 필드가 있다면, 메서드 기능으로 제공
  * 단, 미리 가공하는 것이 성능 상 이점이 있다면, 필드로 가지고 있는 것이 좋을 수도 있다.

```java
class Bill {
    
    private final List<Menu> menus;
    private final long totalPrice;
    
    public long calculateTotalPrice() {
        return this.menus.stream()
                .mapToLong(Menu::getPrice)
                .sum();
    }
}
```