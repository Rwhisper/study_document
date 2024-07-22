# Spring 프레임워크 이해하기

## 1. 서론

### 1.1. Spring이란?

Spring은 자바를 사용하는 개발자들에게 편리함과 생산성을 제공하는 프레임워크입니다. 쉽게 말해, Spring은 자바 프로그램을 만들 때 자주 필요로 하는 기능들을 미리 만들어서 제공해주는 도구입니다. 이것을 사용하면 코드를 더 간결하고 효율적으로 작성할 수 있습니다.

### 1.2. 왜 Spring을 사용해야 할까?

Spring을 사용하면 복잡한 작업을 단순하게 만들 수 있습니다. 예를 들어, 데이터베이스와 연결하거나 웹 애플리케이션을 만들 때 많은 코드를 작성해야 하는데, Spring이 이런 작업을 쉽게 만들어 줍니다.

## 2. Spring의 주요 기능

### 2.1. IoC (Inversion of Control, 제어의 역전)

IoC는 객체들의 생성과 관리를 Spring이 대신 해준다는 개념입니다. 보통 우리가 직접 객체를 만들고 관리해야 하지만, Spring이 이를 대신하여 필요할 때 객체를 만들어 주고, 필요하지 않으면 없애줍니다.

#### 예시

```java
public class Car {
    private Engine engine;

    // Car 생성자
    public Car(Engine engine) {
        this.engine = engine;
    }

    public void drive() {
        engine.start();
        System.out.println("Car is driving");
    }
}
