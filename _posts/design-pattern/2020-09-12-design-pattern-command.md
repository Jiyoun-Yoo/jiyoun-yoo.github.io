---
title: 'Design Patter4: Command Pattern'
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
article_tag1: 1. Command 패턴이란?
article_tag2: 2. Command 패턴 적용 전
article_tag3: 3. Command 패턴 적용
article_section: Design Pattern
meta_keywords: design-pattern, java
last_modified_at: '2020-09-12 22:00:00 +0800'
---

비트캠프 서초본원 엄진영 강사님의 수업을 듣고 정리했습니다.

---
# Command Patter

- **커맨드 디자인 패턴은 기존 소스에 영향을 끼치지 않고 새 기능을 추가하는 방식이다.**

## 1. Command 패턴이란?

- 메서드의 객체화 설계 기법이다.
- 한 개의 명령어를 처리하는 메서드를 별개의 클래스로 분리하는 기법이다.
- 이렇게 하면 명령어가 추가될 때마다 새 클래스를 만들면 되기 때문에 기존 코드를 손대지 않아서 유지보수에 좋다.
- 즉 기존 소스에 영향을 끼치지 않고 새 기능을 추가하는 방식이다.
- 명령처리를 별도의 객체로 분리하기 때문에 실행 내역을 관리하기 좋고, 각 명령이 수행했던 작업을 다루기가 편하다.
- 인터페이스를 이용하면 메서드 호출 규칙을 단일화 할 수 있기 때문에 코딩의 일관성을 높여줄 수 있다.
- 단 기능 추가할 때마다 해당 기능을 처리하는 새 클래스가 추가되기 때문에 클래스 개수는 늘어난다.
- 그러나 유지보수 측면에서는 기존 코드를 변경하는 것 보다는 클래스 개수가 늘어나는 것이 좋다.
- 유지보수 관점에서는 소스 코드를 일관성 있게 유지보수 할 수 있는게 더 중요하다.

## 2. Command 패턴 적용 전

- 커맨드 패턴을 적용하기 전에는 새 기능을 추가할 때 마다 기존 코드를 변경해야 한다.
- 기존 코드에 새 코드를 추가하는 것은 기존 코드를 손댈 수 있는 위험성이 있다.
- 즉 잘되던 기능을 망치는 경우가 발생할 수 있다.

## 3. Command 패턴 적용

- 명령어를 처리하는 각 메서드를 클래스로 정의한 후 사용한다.
- 일관된 사용을 위해 인터페이스로 호출 규칙을 정의한다.
- 나중에 명령어가 추가되면 그 명령어를 처리할 클래스를 추가하면 된다.

### 0단계 - 기존 코드를 확인한다.

- 기존에는 XXXHandler에 여러 메서드를 두고 각 명령어에 따라 다른 메서드를 호출하는 방식으로 명령어를 처리한다.

`BoardHandler.java`

```java
public class BoardHandler {
  List<Board> boardList;

  public BoardHandler(List<Board> list) {
    this.boardList = list;
  }

  public void add() {
    System.out.println("[게시물 등록]");
  }

  public void list() {
    System.out.println("[게시물 목록]");
  }

  public void detail() {
    System.out.println("[게시물 상세보기]");
  }

  public void update() {
    System.out.println("[게시물 변경]");
  }

  public void delete() {
    System.out.println("[게시물 삭제]");
  }
}
```

- 새로운 기능을 추가하기 위해서는 기존 코드에 새 코드를 추가해야 한다.
- 또한 명령어를 추가한다면, 그 명령을 처리할 메서드도 추가해야 한다.

`App.java`

```java
loop:
  while (true) {
    String command = Prompt.inputString("명령> ");

    switch (command) {
      case "/board/add": boardHandler.add(); break;
      case "/board/list": boardHandler.list(); break;
      case "/board/detail": boardHandler.detail(); break;
      case "/board/update": boardHandler.update(); break;
      case "/board/delete": boardHandler.delete(); break;

      case "quit":
      case "exit":
        System.out.println("안녕!");
        break loop;
      default:
        System.out.println("실행할 수 없는 명령입니다.");
    }
  }
```

### 1단계 - Command 인터페이스를 적용한다.

- 명령을 처리하는 메서드의 호출 규칙인 Command 인터페이스를 정의한다.

```java
public interface Command {
  void execute();
}
```

### 2단계 - 명령을 처리하는 Command 구현체를 생성한다.

- 각 명령어를 처리하는 메서드를 별도의 XXXCommand 클래스를 만들어 분리한다.

```java
public class BoardAddCommand implements Command {
  List<Board> boardList;

  public BoardAddCommand(List<Board> list) {
    this.boardList = list;
  }

  @Override
  public void execute() {
    System.out.println("[게시물 등록]");
  }
}
```

```java
public class BoardListCommand implements Command {
  List<Board> boardList;

  public BoardListCommand(List<Board> list) {
    this.boardList = list;
  }

  @Override
  public void execute() {
    System.out.println("[게시물 목록]");
  }
}
```

```java
public class BoardDetailCommand implements Command {
  List<Board> boardList;

  public BoardDetailCommand(List<Board> list) {
    this.boardList = list;
  }

  @Override
  public void execute() {
    System.out.println("[게시물 조회]");
  }
}
```

```java
public class BoardUpdateCommand implements Command {
  List<Board> boardList;

  public BoardUpdateCommand(List<Board> list) {
    this.boardList = list;
  }

  @Override
  public void execute() {
    System.out.println("[게시물 변경]");
  }
}
```

```java
public class BoardDeleteCommand implements Command {
  List<Board> boardList;

  public BoardDeleteCommand(List<Board> list) {
    this.boardList = list;
  }

  @Override
  public void execute() {
    System.out.println("[게시물 삭제]");
  }
}
```

### 3단계 - 사용자가 명령어를 입력했을 때 `Command` 구현체를 실행하도록 변경한다.

- `App` 클래스가 XXXCommand 객체를 통해 처리하도록 변경한다.

`App.java`

```java
loop:
  while (true) {
    String command = Prompt.inputString("명령> ");

    switch (command) {
      case "/board/add": boardAddCommand.execute(); break;
      case "/board/list": boardListCommand.execute(); break;
      case "/board/detail": boardDetailCommand.execute(); break;
      case "/board/update": boardUpdateCommand.execute(); break;
      case "/board/delete": boardDeleteCommand.execute(); break;

      case "quit":
      case "exit":
        System.out.println("안녕!");
        break loop;
      default:
        System.out.println("실행할 수 없는 명령입니다.");
    }
  }
```

### 4단계 - `/hello` 명령을 추가한다.

- 커맨드 패턴을 적용하여 애플리케이션 아키텍처를 변경되었다.
- 커맨드 패턴을 적용할 경우 새 기능 추가가 쉽다는 것을 확인할 수 있다.

```
명령> /hello
안녕하세요!

명령>
```

`App.java`

```java
loop:
  while (true) {
    String command = Prompt.inputString("명령> ");

    switch (command) {
      	case "/board/add": boardAddCommand.execute(); break;
        case "/board/list": boardListCommand.execute(); break;
        case "/board/detail": boardDetailCommand.execute(); break;
        case "/board/update": boardUpdateCommand.execute(); break;
        case "/board/delete": boardDeleteCommand.execute(); break;
        case "/hello": helloCommand.execute(); break;

        case "quit":
        case "exit":
          System.out.println("안녕!");
          break loop;
        default:
          System.out.println("실행할 수 없는 명령입니다.");
    }
  }
```

### 5단계 - `HashMap`을 이용하여 커맨드 객체를 관리한다.

- 낱개의 레퍼런스로 커맨드 객체를 관리하던 방식을 `Map`을 이용하여 관리한다.
- 명령어를 처리할 때는 `Map`에서 커맨드 객체를 찾아 실행한다.

`App.java`

```java
  // 커맨드 객체를 저장할 맵 객체를 준비한다.
  Map<String, Command> commandMap = new HashMap<>();

  // 맵 객체에 커맨드 객체를 보관한다.
  List<Board> boardList = new ArrayList<>();
  commandMap.put("/board/add", new BoardAddCommand(boardList));
  commandMap.put("/board/list", new BoardListCommand(boardList));
  commandMap.put("/board/detail", new BoardDetailCommand(boardList));
  commandMap.put("/board/update", new BoardUpdateCommand(boardList));
  commandMap.put("/board/Delete", new BoardDeleteCommand(boardList));

loop:
  while (true) {
    String inputStr = Prompt.inputString("명령> ");

    switch (inputStr) {
      case "quit":
      case "exit":
        System.out.println("안녕!");
        break loop;
      default:
        Command command = commandMap.get(inputStr);
          if (command != null) {
            command.execute();
          } else {
            System.out.println("실행할 수 없는 명령입니다.");
          }
    }
  }
```