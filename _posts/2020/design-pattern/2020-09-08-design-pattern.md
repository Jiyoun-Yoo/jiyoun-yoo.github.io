---
title: 'Design Patter2: Factorh Method Pattern'
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
article_tag1: 1. 
article_tag2: 2. 
article_section: Design Pattern
meta_keywords: design-pattern, java
last_modified_at: '2020-09-08 22:00:00 +0800'
---

비트캠프 서초본원 엄진영 강사님의 수업을 듣고 정리했습니다.

---
# Factory Method

인스턴스 생성과정이 복잡할 때 사용하는 설계 기법이다.

## 1. Factory Method란?

복잡한 객체 생성 코드를 메서드에 캡슐화하고, 메서드 호출을 통해 인스턴스를 리턴 받는다.

⇒ 이런 메서드를 **`팩토리 메서드`**라 부른다. 

⇒ 보통 인스턴스의 팩토리 역할을 하는 클래스는 `XxxFactory`라는 이름을 짓는다.

## 2. Factory Method Pattern 적용

### Factory Method 적용 전

인스턴스를 만들 때, 인스턴스를 생성하고 그 인스턴스를 사용할 때 적합하도록 직접 초기화시킨다.

```java
class Car {
  String model;
  int cc;
  boolean sunroof;
}

public class Test01 {
  public static void main(String[] args) {
    // 인스턴스를 생성한다.
    Car c1 = new Car();

		// 사용에 적합하도록 직접 초기화시킨다.
    c1.model = "모닝";
    c1.cc = 1000;
    c1.sunroof = false;
    
    Car c2 = new Car();
    c2.model = "아반떼";
    c2.cc = 1500;
    c2.sunroof = true;
    
    Car c3 = new Car();
    c3.model = "티볼리";
    c3.cc = 2000;
    c3.sunroof = false;
    
    Car c4 = new Car();
    c4.model = "산타페";
    c4.cc = 2500;
    c4.sunroof = true;
  }
}
```

### Factory Method 적용 후

인스턴스를 생성할 때 호출할 메서드를 정의하고, 그 메서드에 인스턴스를 초기화하는 코드를 함께 작성한다. 

인스턴스를 생성하기만 하면, 사용할 준비가 완료된 인스턴스가 생성되는 것이다.

```java
class Car2 {
  String model;
  int cc;
  boolean sunroof;
}

class Car2Factory {
  // 인스턴스를 생성해주는 팩토리 메서드 정의
  public static Car2 create(String product) {
    Car2 c = new Car2();

    switch (product) {
      case "morning":
        c.model = "모닝";
        c.cc = 1000;
        c.sunroof = false;
        break;
      case "sonata":
        c.model = "소나타";
        c.cc = 1500;
        c.sunroof = true;
        break;
      case "tivoli":
        c.model = "티볼리";
        c.cc = 2000;
        c.sunroof = false;
        break;
      case "santafe":
        c.model = "산타페";
        c.cc = 2500;
        c.sunroof = true;
        break;
      default:
        return null;
    }
    return c;
  }
}

public class Test02 {
  public static void main(String[] args) {

		// 팩토리 메서드를 호출하여 인스턴스를 리턴받는다.
    Car2 c1 = Car2Factory.create("morning");
    Car2 c2 = Car2Factory.create("sonata");
    Car2 c3 = Car2Factory.create("tivoli");
    Car2 c4 = Car2Factory.create("santafe");
    Car2 c5 = Car2Factory.create("okok");

    System.out.println(c1.model);
    System.out.println(c2.model);
    System.out.println(c3.model);
    System.out.println(c4.model);
    System.out.println(c5.model);

  }
}
```
