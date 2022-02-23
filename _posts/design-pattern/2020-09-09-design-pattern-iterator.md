---
title: 'Design Patter3: Iterator Pattern'
layout: single
author_profile: true
read_time: true
categories:
- Design Pattern
tag:
- design-pattern
toc: true
toc_sticky: true
toc_label: Contents
description: 비트캠프 엄진영 강사님의 수업을 듣고 정리했습니다.
article_tag1: 1. Iterator란?
article_tag2: 2. Iterator Pattern?
article_tag3: 3. Iterator Pattern 적용
article_section: Design Pattern
meta_keywords: design-pattern, java
last_modified_at: '2020-09-09 22:00:00 +0800'
---

비트캠프 서초본원 엄진영 강사님의 수업을 듣고 정리했습니다.

---
# Iterator Pattern

데이터 목록에서 값을 꺼내는 것을 별도의 객체로 분리하는 설계 방식

## 1. Iterator란?

LinkedList, ArrayList, Stack, Queue 등에서 컬렉션에 따라 값을 넣고 꺼낼 때 호출하는 메서드의 이름이 다르다. 따라서 컬렉션의 타입이 다르더라도 값을 조회하는 방법을 통일하기 위해  호출규칙(인터페이스)를 정의하고, 값을 꺼내주는 객체를 정의한다. 이 때, 값을 꺼내주는 객체를 Iterator라 한다.

## 2. Iterator Pattern?

- 객체 목록을 관리하는 컬렉션(collection)에서 목록 조회 기능을 별도의 객체로 캡슐화하는 설계 기법이다.
- 컬렉션의 관리 방식(data structure)에 상관없이 일관된 목록 조회 방법을 제공할 수 있다.
- 컬렉션을 변경하지 않고도 다양한 방식의 목록 조회 기법을 추가할 수 있다.
- 즉 데이터 목록을 관리하는 객체를 직접 사용하여 값을 꺼내는 것이 아니라, 값을 꺼내는 주는 별도의 객체의 도움을 받아 값을 꺼낸다.
- 이 때, 값을 꺼내주는 객체를 `Iterator`라 부른다.

>  Iterator 패턴을 이용하면, 자료 구조와 상관없이 일관된 방법으로 목록의 값을 조회할 수 있다.

## 3. Iterator Pattern 적용

각 컬렉션마다 서로 다른 방식으로 값을 넣고 꺼내는 방식 대신 `hasNext()`, `next()`라는 메서드를 선언하여 값을 조회한다. 

- Iterator 인터페이스를 만든다.
- Iterator 인터페이스를 구현하는 ListIterator, StackIterator, QueueIterator 클래스를 만든다.
- AbstractList, Stack, Queue에서 각각의 Iterator객체를 생성하는 Iterator 메서드를 만든다.
- 직접 컬렉션의 메서드를 호출하지 않고 iterator를 통해 값을 조회한다.

### 1단계 : Iterator 인터페이스를 만든다.

- 데이터 목록을 조회하는 기능을 캡슐화하여 인터페이스로 정의한다.
- 값을 꺼내주는 객체의 사용 규칙 정의
- 값을 일관성 있게 꺼내기 위해 사용 규칙을 정의한다.

```java
// 데이터 목록 조회 기능을 캡슐화하여 그 사용 규칙을 정의한다.
// => 목록으로 다루려는 데이터의 타입을 제네릭으로 처리한다.

public interface Iterator<E> {
  // 데이터 목록에서 꺼낼 값이 있다면 true, 없다면 false
  boolean hasNext();

  // 데이터 목록에서 값을 꺼낸다.
  E next();
}
```

### 2단계 : 인터페이스 구현체를 정의한다.

- `ArrayList` 에 대한 `Iterator` 구현체를 정의한다.
- `List` 구현체의 목록을 조회하는 기능을 수행한다.
    - `ArrayList` 나 `LinkedList` 는 AbstractList라는 추상 클래스를 구현하는데, 이 추상 클래스가 ListIterator 클래스를 사용한다. 따라서 모두 같은 인터페이스를 갖기 때문에 각각 별개로 **반복자(Iterator)**를 만들 필요는 없다.

```java
import java.util.NoSuchElementException;

public class ListIterator<E> implements Iterator<E> {
  List<E> list;
  int cursor;

  public ListIterator(List<E> list) {
    this.list = list;
  }

  @Override
  public boolean hasNext() {
    return cursor < list.size();
  }

  @Override
  public E next() {
    if (cursor == list.size())
      throw new NoSuchElementException();

    return list.get(cursor++);
  }
}
```

- `hasNext()` : 꺼낼 것이 있나요?
- `next()` : 있다면 하나 꺼내 주세요.

### 3단계 - `List` 구현체가 `Iterator` 객체를 리턴하도록 규칙을 추가한다.

- List 구현체는 ArrayList와 LinkedList가 있다.
- List 인터페이스에 컬렉션의 반복자를 리턴해주는 추상 메서드를 추가하면, 서브 클래스는 이 규칙을 반드시 구현해야만 한다.

```java
public interface List<E> {
  boolean add(E e);
  void add(int index, E element);
  E get(int index);
  E set(int index, E element);
  E remove(int index);
  Object[] toArray();
  E[] toArray(E[] arr);
  int size();

  // 컬렉션의 반복자를 리턴해주는 규칙을 추가
  Iterator<E> iterator();
}
```

### 4단계 - `List` 구현체가 `Iterator` 객체를 리턴하도록 `iterator()` 메서드를 구현한다.

- `AbstractList` 클래스 변경하는데, `List` 인터페이스에 추가된 `iterator()` 규칙을 구현한다. `iterator()`는 해당 리스트 전용 iterator를 생성해서 리턴하도록 구현한다.
- `ArrayList` 나 `LinkedList`는 이 클래스를 상속 받기 때문에 수퍼 클래스에서만`iterator()` 를 구현하면 된다.

```java
public abstract class AbstractList<E> implements List<E> {
  protected int size;

  @Override
  public int size() {
    return size;
  }

  // 인터페이스 새로 추가된 규칙,
	// `Iterator` 구현체를 리턴하는 메서드를 정의한다.
  @Override
  public Iterator<E> iterator() {
    return new ListIterator<E>(this);
  }
}
```

### 5단계 : Handler 에서 목록을 조회할 때 `Iterator` 를 사용한다.

- 전체 목록을 조회할 때 `Iterator` 객체를 사용한다.
- 만약 목록의 일부만 조회하면다면 인덱스를 직접 다루는 이전 방식을 사용해야 한다.

```java
public void list() {
  System.out.println("[게시물 목록]");

  Iterator<Board> iterator = boardList.iterator();

  while (iterator.hasNext()) {
    Board board = iterator.next();
    System.out.printf("%d, %s, %s, %s, %d\n",
      board.getNo(),
      board.getTitle(),
      board.getWriter(),
      board.getRegisteredDate(),
      board.getViewCount());
  }
}
```

### 6단계 - `Stack` 객체에 들어 있는 값을 꺼내 줄 `Iterator` 구현체를 준비하고 리턴한다.

- 2 - 4단계에서 진행한 방식과 동일하게 Iterator를 구현하여 StackIterator를 만든다.
- Stack은 LinkedList를 상속받는데, LinkedList는 AbstractList를 상속받는다. 따라서 AbstractList의 iterator() 메서드를 오버라이딩하여 StackIterator를 생성하는 메서드를 정의한다.

```java
import java.util.NoSuchElementException;

// Stack 객체의 목록 조회 기능을 담당한다.
public class StackIterator<E> implements Iterator<E> {
  Stack<E> stack;

  public StackIterator(Stack<E> stack) {
    this.stack = stack;
  }

  @Override
  public boolean hasNext() {
    return !stack.empty();
  }

  @Override
  public E next() {
    if (stack.empty())
      throw new NoSuchElementException();

    return stack.pop();
  }
}
```

- Stack 클래스를 변경하는데, AbstractList 에서 구현한 iterator()를 Stack 자료 구조에 맞춰 오버라이딩 한다.
- 스택은 한 번 pop() 하면 데이터가 제거되기 때문에, 복제본을 만들어 iterator()의 파라미터로 넣어준다.

```java
import java.util.EmptyStackException;

public class Stack<E> extends LinkedList<E> {
  @Override
  public Iterator<E> iterator() {
    try {
      return new StackIterator<E>(this.clone());
    } catch (Exception e) {
      throw new RuntimeException("스택 복제하는 중에 오류 발생!");
    }
  }
}
```

### 7단계 - `Stack`객체로부터 값을 직접 꺼내지 않고 `Iterator` 를 사용한다.

- Iterator 사용 전

```java
static void printCommandHistory(Stack<String> commandStack) {
  try {
    Stack<String> history = commandStack.clone();

    int count = 0;
    while (!history.empty()) {
      System.out.println(history.pop());
      count++;
    }
  } catch (Exception e) {
    System.out.println("history 명령 처리 중 오류 발생!");
  }
}
```

- Iterator 사용 후

```java
static void printCommandHistory(Iterator<String> iterator) {
  try {
    int count = 0;
    while (iterator.hasNext()) {
      System.out.println(iterator.next());
      count++;
    }
  } catch (Exception e) {
    System.out.println("history 명령 처리 중 오류 발생!");
  }
}
```

### 8단계 - `QueueIterator`를 만들고 객체에 들어 있는 값을 꺼내 줄 `Iterator` 구현체를 준비하고 리턴한다.

```java
import java.util.NoSuchElementException;

// Queue 객체의 목록 조회 기능을 담당한다.
public class QueueIterator<E> implements Iterator<E> {
  Queue<E> queue;

  public QueueIterator(Queue<E> queue) {
    this.queue = queue;
  }

  @Override
  public boolean hasNext() {
    return queue.size() > 0;
  }

  @Override
  public E next() {
    if (queue.size() == 0)
      throw new NoSuchElementException();

    return queue.poll();
  }
}
```

- Queue 클래스를 변경하는데, AbstractList 에서 구현한 iterator()를 Queue 자료 구조에 맞춰 오버라이딩 한다.
- Queue는 한 번 poll() 하면 데이터가 제거된다. 따라서 복제본을 만들어 사용한다.

```java
public class Queue<E> extends LinkedList<E> {
  @Override
  public Iterator<E> iterator() {
    try {
      return new QueueIterator<E>(this.clone());
    } catch (Exception e) {
      throw new RuntimeException("큐를 복제하는 중에 오류 발생!");
    }
  }
}
```

### 9단계 : `Queue`객체로부터 값을 직접 꺼내지 않고 `Iterator` 를 사용한다.

- 기존에는 Stack을 사용하는 printCommandHistory()와 Queue를 사용하는 printCommandHistory2()가 존재했다. 그런데 commandHistory()에 Iterator 패턴을 적용했기 때문에 리스트 타입에 관계 없이 값을 조회할 수 있게 되었다.
- 따라서  printCommandHistory2()를 삭제하고, printCommandHistory()를 사용하여 처리한다.

```java
static void printCommandHistory2(Queue<String> commandQueue) {
    try {
      Queue<String> history = commandQueue.clone();

      int count = 0;
      while (history.size() > 0) {
        System.out.println(history.poll());
        count++;

      }
    } catch (Exception e) {
      System.out.println("history2 명령 처리 중 오류 발생!");
    }
  }
```