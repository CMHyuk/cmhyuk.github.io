## 제네릭 사용 주의사항
1. 제네릭 타입의 객체는 생성이 불가
제네릭 타입 자체로 타입을 지정하여 객체를 생성하는 것은 불가능 한다. 즉, new 연산자 뒤에 제네릭 타입 파라미터가 올수는 없다.

```java
class Sample<T> {
public void someMethod() {
        // Type parameter 'T' cannot be instantiated directly
        T t = new T();
    }
}
```

2. static 멤버에 제네릭 타입이 올 수 없음
아래처럼 static 변수의 데이터 타입으로 제네릭 타입 파라미터가 올 수 없다. 왜냐하면 static 멤버는 클래스가 동일하게 공유하는 변수로서 제네릭 객체가 생성되기도 전에 이미 자료 타입이 정해져 있어야 하기 때문이다. 즉, 논리적인 오류인 것이다.

```java
class Student<T> {
    private String name;
    private int age = 0;

    // static 메서드의 반환 타입으로 사용 불가
    public static T addAge(int n) {

    }
}
```

3. 제네릭으로 배열 선언 주의점
기본적으로 제네릭 클래스 자체를 배열로 만들 수는 없다.

```java
class Sample<T> { 
}

public class Main {
    public static void main(String[] args) {
        Sample<Integer>[] arr1 = new Sample<>[10];
    }
}
```

하지만 제네릭 타입의 배열 선언은 허용된다.
위의 식과 차이점은 배열에 저장할 Sample 객체의 타입 파라미터를 Integer로 지정한다는 뜻이다. 즉,new Sample<Integer>() 인스턴스는 저장이 가능하며, new Sample<String>() 인스턴스는 저장이 불가능하다는 소리이다.

출처: https://inpa.tistory.com/entry/JAVA-☕-제네릭Generics-개념-문법-정복하기 [Inpa Dev 👨‍💻:티스토리]