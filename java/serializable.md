#### 자바 직렬화
자바 직렬화는 자바 개발자 입장에서는 상당히 쉽고 빠르게 사용할 수 있도록 만든 기술이다.

#### 장점
기본적으로 프레임워크에서 자바 직렬화로 제공하는 이유는 앞서 말한 자바 직렬화 장점과 일맥상통한다. 개발자가 신경 안 쓰고 빠르게 개발할 수 있다.
JSON 또는 CSV 등 형태의 포맷을 이용하면 직렬화 또는 역직렬화시에 특정 라이브러리를 도입해야 쉽게 개발이 가능하며,
구조가 복잡하면 직접 매핑시켜줘야 하는 작업도 포함하게 된다.
그것에 비해 자바 직렬화는 비교적 복잡한 객체도 큰 작업 없이 (java.io.Serializable 인터페이스만 구현해주면)
기본 자바 라이브러리만 사용해도 직렬화와 역직렬화를 할 수 있다.

#### 주의점
* 특별한 문제없으면 자바 직렬화 버전 serialVersionUID의 값은 개발 시 직접 관리해야 한다. 
* serialVersionUID의 값이 동일하면 멤버 변수 및 메서드 추가는 크게 문제가 없다. 
* 멤버 변수 제거 및 이름 변경은 오류는 발생하지 않지만 데이터는 누락된다.

역직렬화 대상의 클래스의 멤버 변수 타입 변경을 지양해야 합니다. 자바 역직렬화시에 타입에 엄격합니다.
나중에라도 타입 변경이 되면 직렬화된 데이터가 존재하는 상태라면 발생할 예외를 경우의 수를 다 신경 써야 합니다.

#### 용량 문제
자바 직렬화시에 기본적으로 타입에 대한 정보 등 클래스의 메타 정보도 가지고 있기 때문에 상대적으로 다른 포맷에 비해서 용량이 큰 문제가 있다.
특히 클래스의 구조가 거대해지게 되면 용량 차이가 커지게 된다. 예를 들면 클래스 안에 클래스 또 리스트 등 이런 형태의 객체를 직렬화 하게 되면 내부에 참조하고 있는 모든 클래스에 대한 메타정보를 가지고 있기 때문에 용량이 비대해지게 된다.
그래서 JSON 같은 최소의 메타정보만 가지고 있으면 테스트로 된 포맷보다 같은 데이터에서 최소 2배 최대 10배 이상의 크기를 가질 수 있다.


**"긴 시간 동안 외부에 저장하는 의미 있는 데이터들은 자바 직렬화를 사용하지 말자."**

1. 외부 저장소로 저장되는 데이터는 짧은 만료시간의 데이터를 제외하고 자바 직렬화를 사용을 지양한다. 
2. 역직렬화시 반드시 예외가 생긴다는 것을 생각하고 개발한다. 
3. 자주 변경되는 비즈니스적인 데이터를 자바 직렬화을 사용하지 않는다. 
4. 긴 만료 시간을 가지는 데이터는 JSON 등 다른 포맷을 사용하여 저장한다.


참고 - https://techblog.woowahan.com/2551/