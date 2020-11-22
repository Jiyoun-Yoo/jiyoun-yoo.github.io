---
title: 'Design Patter6: Observer Pattern'
layout: single
author_profile: true
read_time: true
comments: true
share: true
related: true
categories:
- Design Pattern
tag:
- design-pattern
toc: true
toc_sticky: true
toc_label: Contents
description: 비트캠프 엄진영 강사님의 수업을 듣고 정리했습니다.
article_tag1: 1. Observer Pattern?
article_tag2: 2. Observer Pattern 적용 전
article_tag3: 3. Observer Pattern 적용 하기 
article_section: Design Pattern
meta_keywords: design-pattern, java
last_modified_at: '2020-10-12 22:00:00 +0800'
---

비트캠프 서초본원 엄진영 강사님의 수업을 듣고 정리했습니다.

---
# **Observer Pattern**

## 1. Observer Pattern?

- 특정 객체의 상태 변화에 따라 수행해야 하는 작업이 있을 경우, 기존 코드를 손대지 않고 손쉽게 기능을 추가하거나 제거할 수 있는 설계 기법이다.
- 발**행(publish)/구독(subscribe) 모델** 이라고 부르기도 한다.
- 발행 측(publisher)에서는 구독 객체(subscriber)의 목록을 유지할 컬렉션을 가지고 있다.
- 또한 구독 객체를 등록하거나 제거하는 메서드가 있다.
- 구독 객체를 **리스너(listener)** 또는 **관찰자(observer)**라 부르기도 한다.

## 2. Observer Pattern 적용 전

### 프로젝트 완료

```java
public class Car {
  public void start() {
    System.out.println("시동을 건다.");
  }

  public void run() {
    System.out.println("달린다.");
  }

  public void stop() {
    System.out.println("시동을 끈다.");
  }
}
```

```java
public class Test01 {
  public static void main(String[] args) {
    Car car = new Car();
    car.start();
    car.run();
    car.stop();
  }
}
```

### 프로젝트 완료 후 기능 추가

- Observer Pattern을 적용하기 전에는 프로젝트 완료 후 기능을 추가하는 상황이 발생한다면, 기존 코드를 수정하여 새로운 기능을 추가해야 한다.

    (1) 자동차의 시동을 걸 때 안전벨트 착용 여부를 검사하는 기능을 추가한다.

    ⇒ 기존 Car 클래스의 start() 메서드에 코드를 추가

    (2) 자동차 시동 걸 때 엔진 오일 검사 기능을 추가한다.

    ⇒ Car 클래스의 start() 메서드에 해당 기능을 수행하는 코드를 추가한다.

    (3) 자동차 시동 걸 때 브레이크 오일 검사 기능을 추가한다.

    ⇒ Car의 start() 메서드에 해당 코드 추가

```java
public class Car {
  public void start() {
    System.out.println("시동을 건다.");

    // 1월 20일 - 자동차 시동을 걸 때 안전 벨트 착용 여부를 검사하는 기능을 추가
    System.out.println("안전벨트 착용 여부 검사");

    // 2월 30일 - 자동차 시동을 걸 때 엔진 오일 유무를 검사하는 기능을 추가
    System.out.println("엔진 오일 유무 검사");

    // 3월 2일 - 자동차 시동을 걸 때 브레이크 오일 유무를 검사하는 기능을 추가
    System.out.println("브레이크 오일 유무 검사");
  }

  public void run() {
    System.out.println("달린다.");
  }

  public void stop() {
    System.out.println("시동을 끈다.");
  }
}
```

- 기능 업그레이드 후 또 다른 기능을 추가하게 된다면, 마찬가지로 기존 코드를 수정하여 새로운 기능을 추가해야 했다.

    (4) 시동 끌 때 자동차 전조등을 자동으로 끄는 기능을 추가한다.

    ⇒ Car의 stop() 메서드에 해당 코드 추가

    (5) 시동 끌 때 썬루프를 자동으로 닫기

    ⇒ Car의 stop() 메서드에 해당 코드 추가

```java
public class Car {
  public void start() {
    System.out.println("시동을 건다.");
    
    // 1월 20일 - 자동차 시동을 걸 때 안전 벨트 착용 여부를 검사하는 기능을 추가
    System.out.println("안전벨트 착용 여부 검사");
    
    // 2월 30일 - 자동차 시동을 걸 때 엔진 오일 유무를 검사하는 기능을 추가 
    System.out.println("엔진 오일 유무 검사");
    
    // 3월 2일 - 자동차 시동을 걸 때 브레이크 오일 유무를 검사하는 기능을 추가
    System.out.println("브레이크 오일 유무 검사");
  }
  
  public void run() {
    System.out.println("달린다.");
  }
  
  public void stop() {
    System.out.println("시동을 끈다.");
    
    // 4월 15일 - 자동차 시동을 끌 때 전조등 자동 끄기 기능을 추가
    System.out.println("전조등을 끈다.");
    
    // 5월 5일 - 자동차 시동을 끌 때 썬루프 자동 닫기 기능을 추가
    System.out.println("썬루프를 닫는다.");
  }
}
```

### 기존 코드를 변경할 때 나타날 수 있는 문제점

- 어떤 고객은 해당 기능이 필요 없을 수도 있다. 이런 경우, 조건문을 추가하여 기능의 동작 여부를 제어해야 한다.
- 코드가 복잡해진다. 이미 디버깅과 테스트가 완료된 기존 코드를 변경하면 새 버그가 발생할 수 있다.
- 기존 코드를 수정하게 되면, 이전 버전을 사용하려고 할 때 문제가 발생한다.

> 기존 코드를 손대지 않고 새 기능을 추가하려면 bserver 패턴으로 설계하라!

### 결론!

- 기존의 프로그래밍 방식은 특정 상태에서 수행하는 기능을 추가할 때 기존 클래스에 계속 코드를 추가해야 했다.
- 기존 코드에 계속 새 코드를 추가하는 방식은 유지보수에 좋지 않다.
- Observer 패턴을 적용하면 기존 클래스를 손대지 않고 특정 상태에서 수행하는 작업을 쉽게 추가할 수 있다.

## 3. Observer Pattern 적용 하기

### Observer 패턴 적용 과정

1) publisher의 상태가 바뀔때마다 subscriber에 대해 호출할 메서드 규칙 정의

2) subscriber를 publisher에 등록하고 제거하는 메서드와 컬렉션 추가

3) publisher의 상태가 바뀌었을 때 subscriber에게 통지하는 코드 추가

### 1단계 : 호출 규칙을 정의한다.

- 자동차 시동을 켜고 끌 때 호출될 규칙을 정의한다.
- 인터페이스에 시동을 켤 때와 시동을 끌 때 호출할 메서드를 정의한다. 보통 메서드의 이름은 동사로 시작하는데, 옵저버에게 통지할 때 호출하는 메서드는  명사구의 상태 이름으로 정의할 수 있다.

```java
public interface CarObserver {
	// 자동차 시동을 켤 때 호출될 메서드
	//  - 시동 걸 때 뭔가 작업하고 싶다면 이 메서드에 그 코드를 작성하면 된다.
  void carStarted();

  // 자동차 시동을 끌 때 호출될 메서드
	//  - 시동 끌 때 뭔가 작업하고 싶다면 이 메서드에 그 코드를 작성하면 된다.
  void carStopped();
}
```

### 2단계 : subscrber를 등록하고 제거하는 메서드와 컬렉션을 추가한다.

- Car클래스(publisher)에 Car 클래스의 상태에 따라 각각의 메서드를 호출할 CarObserver 객체를 담을 Collection을 만든다.
- 옵저버 객체를 Collection에 담을 addCarObserver()와 옵저버 객체를 Collection에서 삭제할 removeCarObserver() 메서드를 추가한다.

```java
public class Car {
  //--------------------------------------------------------------
  // Observer 디자인 패턴 적용
  //  - Publisher 쪽에 추가해야 하는 필드와 메서드

  // 관찰자(Observer/Listener/Subscriber)의 객체 주소를 보관한다.
  List<CarObserver> observers = new ArrayList<>();

  // 자동차의 상태 변경을 보고 받을 관찰자를 등록한다.
  public void addCarObserver(CarObserver observer) {
    observers.add(observer);
  }

  // 자동차의 상태 변경을 보고 받는 관찰자를 제거한다.
  public void removeCarObserver(CarObserver observer) {
    observers.remove(observer);
  }
  //--------------------------------------------------------------
	
	public void start() {
    System.out.println("시동을 건다.");
  }

  public void run() {
    System.out.println("달린다.");
  }

  public void stop() {
    System.out.println("시동을 끈다.");
}
```

### 3단계 : publisher의 상태를 subscriber에게 통지할 코드를 추가한다.

```java
public class Car {
  List<CarObserver> observers = new ArrayList<>();

  public void addCarObserver(CarObserver observer) {
    observers.add(observer);
  }

  public void removeCarObserver(CarObserver observer) {
    observers.remove(observer);
  }

  public void start() {
    System.out.println("시동을 건다.");
    //------------------------------------------------------------
    // Observer 디자인 패턴:
    //  - publisher의 상태가 바뀌었을 때 subscriber에게 통지한다.
    //  - 즉 subscriber(observer/listener)에 대해 규칙(CarObserver 인터페이스)에 따라 메서드를 호출한다.
    //    예) 자동차의 시동을 걸면, 등록된 관찰자들에게 알린다.
    for (CarObserver observer : observers) {
      observer.carStarted();
    }
    //------------------------------------------------------------
  }

  public void run() {
    System.out.println("달린다.");
  }

  public void stop() {
    System.out.println("시동을 끈다.");
    //------------------------------------------------------------
    // Observer 디자인 패턴:
    //  - publisher의 상태가 바뀌었을 때 subscriber에게 통지한다.
    //  - 즉 subscriber(observer/listener)에 대해 규칙(CarObserver 인터페이스)에 따라 메서드를 호출한다.
    //    예) 자동차의 시동을 끄면, 등록된 관찰자들에게 보고한다.
    for (CarObserver observer : observers) {
      observer.carStopped();
    }
    //------------------------------------------------------------
  }
}
```

### 4단계: 새로운 기능을 추가한다.

- 프로젝트 완료한 다음 시간이 지난 후, 자동차의 시동을 걸 때 안전벨트 착용 여부를 검사하는 기능을 추가한다.

    (1) 자동차의 시동을 걸릴 때 보고를 받을 객체(SafeBeltCarObserver)를 준비한다.

    (2) 시동 걸 때 수행할 기능을 정의한다. 즉 carStarted() 메서드 정의한다.

    (3) Car 객체에 관찰자를 등록한다.

```java
public class SafeBeltCarObserver implements CarObserver {
  @Override
  public void carStarted() {
    System.out.println("안전벨트 착용 여부 검사");
  }

  @Override
  public void carStopped() {}
}
```

```java
public class Test01 {
  public static void main(String[] args) {

    Car car = new Car();

    // 새 기능이 들어있는 객체를 Car(publisher)에 등록한다.
    //  - Car 클래스를 손대지 않고 새 기능을 추가하는 방법이다.
    //  - 이것이 Observer 패턴으로 구조와시킨 이유이다.
    car.addCarObserver(new SafeBeltCarObserver());
    // Car 객체의 상태가 바뀔 때 실행될 코드를 별도의 클래스로 정의한 다음,
    // Car 객체에 등록한다.

    car.start();
    // Car 객체는 start()가 호출되면
    // 등록된 모든 subscriber(observer/listener)에게 통지(메서드 호출)한다.

    car.run();
    car.stop();
  }
```

- 업그레이드를 수행한 다음 시간이 지난 후 자동차 시동 걸 때 엔진 오일 검사 기능을 추가한다.

    (1) 엔진오일 검사하는 옵저버(EngineOilCarObserver)를 정의한다.

    (2) Car 객체에 등록한다.

```java
public class EngineOilCarObserver implements CarObserver {
  @Override
  public void carStarted() {
    System.out.println("엔진 오일 유무 검사");
  }

  @Override
  public void carStopped() {}
}
```

```java
public class Test01 {
  public static void main(String[] args) {
    Car car = new Car();

    car.addCarObserver(new SafeBeltCarObserver());

    // 엔진 오일을 검사할 옵저버를 등록한다.
    car.addCarObserver(new EngineOilCarObserver());

    car.start();
    car.run();
    car.stop();
  }
}
```

- Observer Pattern을 적용하면 다양한 기능을 추가하거나 삭제할 수 있다.

    (1) 새로운 기능을 수행할 클래스를 정의한다.

```java
public class BrakeOilCarObserver implements CarObserver {
  @Override
  public void carStarted() {
    System.out.println("브레이크 오일 유무 검사");
  }

  @Override
  public void carStopped() {}
}
```

```java
public class LightOffCarObserver implements CarObserver {
  @Override
  public void carStarted() {}

  @Override
  public void carStopped() {
    System.out.println("전조등을 끈다.");
  }
}
```

```java
public class SunRoofCloseCarObserver implements CarObserver {
  @Override
  public void carStarted() {}

  @Override
  public void carStopped() {
    System.out.println("썬루프를 닫는다.");
  }
}
```

(2) 새 기능을 수행하는 옵저버를 추가한다.

```java
public class Test01 {
  public static void main(String[] args) {
    Car car = new Car();

    car.addCarObserver(new SafeBeltCarObserver());
    car.addCarObserver(new EngineOilCarObserver());
    car.addCarObserver(new BrakeOilCarObserver());
    car.addCarObserver(new LightOffCarObserver());
    car.addCarObserver(new SunRoofCloseCarObserver());

    car.start();
    car.run();
    car.stop();
  }
}
```

### 5단계 : 리팩토링

- 옵저버에 통지하는 코드를 별도의 메서드로 분리하여 유지보수 하기 좋게 만든다.

```java
public class Car {

  List<CarObserver> observers = new ArrayList<>();

  public void addCarObserver(CarObserver observer) {
    observers.add(observer);
  }

  public void removeCarObserver(CarObserver observer) {
    observers.remove(observer);
  }

  // 리팩토링: 메서드 추출(extract method)
  //  - 특정 기능을 수행하는 코드를 이해하기 쉽도록 외부 메서드로 추출하는 것
  private void notifyObserversOnStarted() {
    for (CarObserver observer : observers) {
      observer.carStarted();
    }
  }

  private void notifyObserversOnStopped() {
    for (CarObserver observer : observers) {
      observer.carStopped();
    }
  }

  public void start() {
    System.out.println("시동을 건다.");

    notifyObserversOnStarted();
  }

  public void run() {
    System.out.println("달린다.");
  }

  public void stop() {
    System.out.println("시동을 끈다.");

    notifyObserversOnStopped();
  }
}
```

### 6단계 : 추상 메서드 활용

- CarObserver 구현체를 만들 때, 인터페이스에 선언된 모든 메서드를 구현해야 한다. 관심없는 메서드라도 구현해야 한다.
- 예)
    - SafeBeltCarObserver는 시동 걸 때 작업을 수행한다. 그래서 carStarted() 메서드에 코드를 삽입하였다.
    - 그런데 인터페이스를 구현하려면 모든 메서드를 정의해야 하기 때문에 관심이 없는데도 불구하고 carStopped() 메서드도 구현하였다. 물론 코드가 없는 빈 메서드이다.
- 위와 같은 경우, (여러 개의 메서드 중에서 주로 일부 메서드만 구현하는 경우) **추상 클래스를 사용하여 메서드를 미리 구현**해 놓으면  인터페이스 구현체를 정의하기 편하다!

- 인터페이스

```java
public interface CarObserver 
  void carStarted();
  void carStopped();
}
```

- 추상 메서드
    - 인터페이스 구현체가 메서드를 정의하기 쉽도록 이 클래스에서 미리 모든(또는 일부) 메서드를 구현하였다. 이 클래스의 존재 이유는 인터페이스 구현체가 메서드를 정의하기 쉽도록  미리 구현된 메서드를 상속해주는 일을 한다.
    - 즉 이 클래스 자체를 사용하려는 것이 아니다. 추상 메서드가 없지만, 추상 클래스로 선언함으로써 개발자에게 이 클래스의 역할을 알리는 효과가 있다.

```java
// 인터페이스를 구현한 추상 클래스는
// 보통 그 클래스 이름을 'Abstract-'로 시작한다.
public abstract class AbstractCarObserver implements CarObserver {

  @Override
  public void carStarted() {
    // 서브 클래스에게 구현된 메서드를 상속해주기 때문에 수퍼클래스에서 미리 구현한다.
    // 단, 아무런 코드를 넣지 않는다.
  }

  @Override
  public void carStopped() {
    // 서브 클래스에게 구현된 메서드를 상속해주기 때문에 수퍼클래스에서 미리 구현한다.
    // 단, 아무런 코드를 넣지 않는다.
  }
}
```

- 각 기능을 수행하는  Observer를 추상 클래스를 상속받도록 수정한다.
    - 이전 버전에서는 인터페이스를 직접 구현했지만, 이번 버전에서는 추상 클래스를 상속 받아 간접적으로 구현한다.
    - 수퍼 클래스(추상 클래스)에서 모든 메서드를 정의했기 때문에 굳이 정의하지 않아도 되는 메서드는 정의하지 않는다.

```java
public class SafeBeltCarObserver extends AbstractCarObserver {
  @Override
  public void carStarted() {
    System.out.println("안전벨트 착용 여부 검사");
  }

	// carStopped()는 정의하지 않는다.
}
```

```java
public class EngineOilCarObserver extends AbstractCarObserver {
  @Override
  public void carStarted() {
    System.out.println("엔진 오일 유무 검사");
  }
}
```

```java
public class BrakeOilCarObserver extends AbstractCarObserver {
  @Override
  public void carStarted() {
    System.out.println("브레이크 오일 유무 검사");
  }
}
```

```java
public class LightOffCarObserver extends AbstractCarObserver {
  @Override
  public void carStopped() {
    System.out.println("전조등을 끈다.");
  }
}
```

```java
public class SunRoofCloseCarObserver extends AbstractCarObserver {
  @Override
  public void carStopped() {
    System.out.println("썬루프를 닫는다.");
  }
}
```