---
title: 'Design Patter1: Singleton Pattern'
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
article_tag1: 1. Singleton Pattern이란?
article_tag2: 2. Signleton Pattern 적용
article_section: Design Pattern
meta_keywords: design-pattern, java
last_modified_at: '2020-09-05 22:00:00 +0800'
---

비트캠프 서초본원 엄진영 강사님의 수업을 듣고 정리했습니다.

---
# Singleton Pattern

## 1. Singleton Pattern이란?

클래스의 객체를 두 개 이상 생성하지 못하도록 생성자에 직접 접근하는 것을 막고, 대신 객체를 생성하는 다른 스태틱 메서드를 제공하는 방식으로 클래스를 설계하는 방식이다.

### 객체를 하나만 생성하는 메서드의 원리

- 클래스를 선언하는데, **생성자의 접근 제한자를 private으로** 한다.
    - 접근 제한자를 private으로 하면 생성자를 외부에서는 호출할 수 없고 오직 내부에서만 호출할 수 있다.
- **인스턴스를 생성하는  스태틱 메서드를 선언**한다.
    - 이미 인스턴스가 있다면 그 인스턴스를 리턴하고, 기존에 생성된 인스턴스가 없다면 새로운 인스턴스를 생성하도록 한다.

> 인스턴스를 딱 한 개만 생성하여 공유하고 싶다면, Singleton 설계 방식으로 클래스를 정의하라!


## 2. Signleton Pattern 적용

### Singleton 적용 전

- 생성자를 따로 정의하지 않기 때문에 컴파일 과정에서 기본 생성자가 자동으로 추가된다.
  - 생성자를 호출할 때마다 인스턴스를 만들 수 있기 때문에 인스턴스를 여러 개 생성할 수 있다.

```java
class Car1 {
  String model;
  int cc;

  // 기본 생성자 자동 추가
  //public Car1() {}
}

public class Test01 {
  public static void main(String[] args) {
    // 인스턴스 생성
    Car1 c1 = new Car1();
    Car1 c2 = new Car1();

    System.out.println(c1 == c2);
  }
}
```

### Singleton 적용 후

- 생성자가 존재하지만 private으로 비공개 되어 있기 때문에 직접 호출할 수 없다.
- 생성자를 호출할 수 없으면 인스턴스를 생성할 수 없다.
- 다른 메서드를 호출하여 인스턴스를 생성하라는 의미다.

```java
class Car2 {
  String model;
  int cc;

  // 인스턴스 주소를 받을 클래스 필드를 선언한다.
  private static Car2 instance;

  // 1) 생성자를 정의하고 private으로 선언한다.
  private Car2() {}

  // 2) 인스턴스를 생성해주는 스태틱 메서드를 정의한다.
  public static Car2 getInstance() {
    if (Car2.instance == null) {
      // 아직 인스턴스를 생성한 적이 없다면,
      // 즉시 인스턴스를 생성한다.
      Car2.instance = new Car2();
    }

    // 이미 인스턴스가 있다면,
    // 기존에 변수에 저장된 인스턴스 주소를 리턴한다.
    return Car2.instance;
  }
}

public class Test02 {
  public static void main(String[] args) {

    // 생성자가 private으로 비공개 되어 있다.
    // 생성자를 호출할 수 없으면 인스턴스를 생성할 수 없다.
    //Car2 c1 = new Car2(); // 컴파일 오류!

    Car2 c2 = Car2.getInstance();
    Car2 c3 = Car2.getInstance();
    Car2 c4 = Car2.getInstance();

    System.out.println(c2 == c3);
    System.out.println(c3 == c4);
  }
}
```

### Singleton 연습

- 김밥 인스턴스를 한 개만 생성하도록 Singleton 패턴을 적용하라.

```java
class Kimbap {

  private static Kimbap instance;

  private Kimbap () {}

  public static Kimbap getInstance() {
    if(Kimbap.instance == null) {
      Kimbap.instance = new Kimbap();
    }
    return Kimbap.instance;
  }
}

public class Test03 {
  public static void main(String[] args) {
    // 아래 코드는 컴파일 오류!
    // Kimbap bap1 = new Kimbap();

    Kimbap bap2 = Kimbap.getInstance();
    Kimbap bap3 = Kimbap.getInstance();
    System.out.println(bap2 == bap3); // true
  }
}
```