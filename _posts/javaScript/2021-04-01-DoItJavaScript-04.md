---
title: '[Do it! 자바스크립트 + 제이쿼리 입문] 04 객체'
categories:
- JavaScript
tag:
- [javaScript, jQuery]
last_modified_at: '2021-04-01 22:00:00 +0800'
---

출처 : [Do it! 자바스크립트 + 제이쿼리](http://www.easyspub.co.kr/20_Menu/BookView/253/PUB)

---

# 04-1 객체

## (1) 객체란?

- 자바스크립트는 **객체(Object)** 기반 언어이다.
- 객체는 기능과 속성을 가지고 있다. 주변의 모든 사물을 객체라 한다.
- 예) TV라는 객체에는 켜다, 끄다, 음을 소거하다, 볼륨을 높이다/낮추다 등의 기능이 있다.
- 자바스크립트에는 다양한 객체가 있는데, 객체가 가진 기능을 사용할 수 있다. 이런 기능들을 **메서드(Method)**라 한다. 또한 객체는 **속성(Property)**을 가지고 있다.
- 자바스크립트 객체의 메서드와 속성을 사용하는 기본형은 다음과 같다.

```javascript
① 객체.메서드();
② 객체.속성; 또는 ③ 객체.속성=값;
```

① 객체의 메서드를 실행한다.

② 객체의 속성값을 가져온다.

③ 객체의 속성값을 바꾼다.

- 자바스크립트에서 TV의 기능(메서드)은 다음과 같이 사용해야 한다.

```javascript
TV.켜다(); 
TV.끄다();
```

- 객체가 가지고 있지 않은 메서드를 사용할 수는 없다.

```javascript
TV.앞으로 전진(); // (X)
자동차.앞으로 전진(); // (O)
```

- 자바스크립트에서 TV의 너비와 색상, 속성 정보를 알아내고 싶다면, 아래와 같이 적용할 수 있다.

```javascript
// TV의 속성값을 가져온다.
TV.width;
TV.color; 

// TV의 속성값을 바꾼다.
TV.color = black;
```

## (2) 객체의 종류

- 자바스크립트의 객체는 크게 내장 객체, 브라우저 객체 모델(**BOM**, Browser Object Model), 문서 객체 모델(**DOM**, Document Object Model)로 나눌 수 있다.

### 내장 객체

- 내장 객체는 자바스크립트 엔진에 내장되어 있어 필요한 경우에 생성해서 사용할 수 있다.
- 내장 객체로는 문자(String), 날짜(Date), 배열(Array), 수학(Math) 객체 등이 있다.
- 예) 오늘 날짜를 알고싶다면, Date 객체를 생성하여 오늘 날짜를 알려주는 메서드 `getDate()`를 사용하면 된다.

### 브라우저 객체 모델

- 브라우저 객체 모델(**BOM**)은 **브라우저에 계층 구조로 내장되어 있는 객체**를 말한다.
- 브라우저 객체로는 window, screen, location, history, navigator 객체 등이 있다.
- 브라우저(window)는 document와 location 객체의 상위 객체이다.
- 예) 자바스크립트를 이용해 현재 열려 있는 사이트에서 다른 사이트로 이동하려면 location 객체에 참조 주소(`href`) 속성을 바꾸면 된다.

```javascript
window.location.href="사이트 URL"
```

### 문서 객체 모델

- 문서 객체 모델(**DOM**)은 **HTML 문서 구조**를 말한다. HTML 문서의 기본 구조는 최상위 객체로 `<html>`이 있으며, 그 하위 객체로는 `<head>`와 `<body>`가 있다.
- 예를 들어 자바스크립트를 이용해 이미지의 src 속성을 바꾸고 싶다면 지정된 `<img>`를 선택해 src 속성을 바꿔야 한다. 이때 지정 요소를 제대로 선택해서 가져오려면 문서 객체의 구조를 잘 이해하고 있어야 한다.
- 문서 객체 모델에서는 HTML의 모든 요소들을 문서 객체로 선택하여 자유롭게 속성을 바꿀 수 있고, 선택한 문서 객체에 원하는 스타일(CSS)을 적용할 수도 있다.
- 자바스크립트의 문서 객체 모델은 IE8 이하 버전에서는 호환성이 덜어지기 때문에, 이러한 점을 극복하기 위해 제이쿼리 문서 객체 모델을 많이 사용한다.

# 04-2 내장 객체

- 내장 객체(Built-in Object)란 브라우저의 자바스크립트 엔진에 내장된 객체라 하며, 필요한 경우 객체를 생성해서 사용할 수 있다.
- 내장 객체로는 문자(String), 날짜(Date), 배열(Array), 수학(Math), 정규 표현 객체(RegExp Object)등이 있다.

## (1) 내장 객체 생성하기

- 객체를 생성할 때는 `new`라는 키워드와 생성 함수를 사용한다.

```javascript
참조 변수(인스턴스 이름) = new 생성 함수();
```

- 변수가 생성된 객체를 참조하는데, 변수를 이용해 참조한다는 말은 앞으로 생성된 객체를 이용할 때 참조 변수를 사용하겠다는 의미이다.
- 예) `new` 키워드와 기본 객체 생성 함수 `Object()`를 이용해 객체를 생성한다. 생성된 객체는 변수 tv가 참조하고 있다. 이를 이용해 객체의 속성과 메서드를 생성한다.

```javascript
var tv = new Object();
tv.color = "white";
tv.prive = 300000;
tv.info = funtion() {
	document.write("tv 색상: " + this.color, "<br>");
	document.write("tv 가격: " + this.price, "<br>");
}

var car = {
	color: "black",
	price: 5000000,
	info: funtion() {
		document.write("car 색상: " + this.color, "<br>");
		document.write("car 가격: " + this.price, "<br>");
	}
};

document.write("<h1>tv 객체 메서드 호출</h1>");
tv.info();

document.write("<h1>car 객체 메서드 호출</h1>");
car.info();	  

```

## (2) 날짜 정보 객체

- 날짜나 시간 관련 정보를 제공받고 싶을 때는 날짜 객체(Date Object)를 생성한다. 날짜 정보 객체는 날짜와 관련된 작업을 할 때 유용한 객체이다. 날짜 정보 객체를 이용하면 달력과 특정 기념일 D-day 계산기도 만들 수 있다.
- 현재 날짜 정보를 제공하는 Date 객체는 다음과 같이 생성한다.

```javascript
참조 변수 = new Date();
```

- 특정 날짜의 정보를 제공받아야 하는 경우에는 특정 날짜 정보 객체를 만들어야 한다.

```javascript
참조 변수 = new Date("연/월/일");
참조 변수 = new Date(연, 연-1, 일);
```

### 날짜 관련 메서드

- **날짜 정보를 가져올 때(GET)**
    - `getFullYear()` : 연도 정보를 가져옴
    - `getMonth()` : 월 정보를 가져옴(`현재 월 - 1`)
    - `getDate()` : 일 정보를 가져옴
    - `getHours()` : 시 정보를 가져옴
    - `getMinutes()` : 분 정보를 가져옴
    - `getSeconds()` : 초 정보를 가져옴
    - `getMillisecondcs()` : 밀리초 정보를 가져옴(1/1,000초 단위)
    - `getTime()` : 1970년 1월 1일부터 경과된 시간을 밀리초로 표기함
    - `toGMTString()` : GMT 표준 표기 방식으로 문자형 데이터로 반환함
- **날짜 정보를 수정할 때(SET)**
    - `setFullYear()` : 연도 정보만 수정함
    - `setMonth()` : 월 정보만 수정함(월 - 1)
    - `setDate()` : 일 정보만 수정함
    - '요일'은 날짜를 바꾸면 자동으로 바뀌므로 setDay()는 없음
    - `setHours()` : 시 정보만 수정함
    - `setMinutes()` : 분 정보만 수정함
    - `setSeconds()` : 초 정보만 수정함
    - `setMilliseconds()` : 밀리초 정보만 수정함
    - `setTime()` : 1970년 1월 1일부터 경과된 시간을 밀리초로 수정함
    - `toLocaleString()` : 운영 시스템 표기 방식으로 문자형 데이터로 반환함

### 현재 날짜 객체와 특정 날짜 객체 이용하기

- 현재 날짜 객체

```javascript
var today = new Date();
var nowMonth = today.getMonth(),
		nowDate = today.getDate(),
		nowDay = today.getDay();

document.write("<h1>오늘 날짜 정보</h1>");
document.write("현재 월: " + nowMonth + "<br>");
document.write("현재 일: " + nowDate + "<br>");
document.write("현재 요일: " + nowDay + "<br>");
```

- 특정 날짜 객체

```javascript
var worldcup = new Date(2020,4,31);
var theMonth = worldcup.getMonth(),
		theDate = worldcup.getDate(),
		theDay = worldcup.getDay();

document.write("<h1>월드컵 날짜 정보</h1>");
document.write("2002월드컵 몇 월: " + nowMonth + "<br>");
document.write("2002월드컵 며칠: " + nowDate + "<br>");
document.write("2002월드컵 무슨 요일: " + nowDay + "<br>");
```

- 요일을 나타낼 때, `0`은 일요일을 나타내고 `1`부터 `6`까지는 월요일부터 토요일을 나타낸다.

### 날짜 계산기

- 현재 날짜부터 특정 날짜까지 며칠이 남았는지 구하는 형식은 다음과 같다. 이때 남은 일 수는 밀리초(`1/1,000` 초) 단위로 계산한다.

```
남은 일 수(밀리초) = 특정 날짜 객체 - 현재 날짜 객체
```

- 밀리초로 계산한 시간 값

```
1초 = 1,000(msc)
1분(60초) = 1,000 * 60                 // 60,000(msc)
1시간(60분) = 1,000 * 60 * 60           // 3,600,000(msc)
1일(60분*24) = 1,000 * 60 * 60 * 24    // 86,400,000(msc)
```

- 예) 올해 연말까지 며칠이 남았는지 알아보는 프로그램을 작성한다.

```javascript
var today = new Date();
var nowYear = toget.getFullYear();

var theDate = new Date(nowYear, 11, 31); // 올해 12월 31일
var diffDate = theDate.getTime() - today.getTime(); // 특정 날짜 - 현재 날짜(밀리초 단위)

var result = Math.ceil(diffDate / (60 * 1000 * 60 * 24));
// 계산한 값을 일 단위로 계산한 다음 오늘 날짜까지 포함시키기 위해 
// Math.ceil() 메서드를 사용하여 반올림한다.

document.write("연말까지는 " + result + "일 남았습니다.");
```

## (3) 수학 객체

- 자바스크립트 내장 객체는 수하고가 관련된 기능과 속성을 제공하는 수학 객체(Math Object)가 있다. 더하기, 곱하기, 나누기 등은 산술 연산자를 사용하면 되지만, 최댓값, 최솟값, 반올림값 등은 산술 연산자로 구할 수 없다. 이런 경우 수학 객체 메서들 이용하여 수학과 관련된 일련의 작업들을 처리한다.

### 수학 객체의 메서드 및 상수

- `Math.abs(숫자)` : 숫자의 절댓값 반환
- `Math.max(숫자1, 숫자2, 숫자3, 숫자4)` : 숫자 중 가장 큰 값 반환
- `Math.pow(숫자, 제곱값)` : 숫자의 거듭제곱값을 반환
- `Math.random()` : 0 ~ 1 사이의 난수를 반환
- `Math.round(숫자)` : 소수점 첫째 자리에서 반올림하여 정수를 반환
- `Math.ceil(숫자)` : 소수점 첫째 자리에서 무조건 올림하여 정수를 반환
- `Math.floor(숫자)` : 소수점 첫째 자리에서 무조건 내림하여 정수를 반환
- `Math.sqrt(숫자)` : 숫자의 제곱근값을 반환
- `Math.PI()` : 원주율 상수를 반환

### `Math.random()` 활용하기

- `random()` 사용하면 `0`과 `1` 사이에서 난수가 발생한다. 또한 `random()` 메서드를 사용하여 `0`과 `1`사이가 아닌 임의로 지정한 숫자의 구간에서 난수가 발생하도록 할 수 있다.
- `0`부터 `10`까지의 난수를 반환

```javascript
Math.random()*10; // 0부터 10까지 실수로 난수 반환
```

- `0`부터 `10`까지의 정수로만 난수를 반환하려면 `Math.floor()`를 이용해야 한다. `floor()` 메서드는 값을 내리기 때문에 `10`이 아닌 `11`을 곱한다.

```javascript
Math.floor(Math.random()*11); // 0부터 11까지 난수를 발생하여 소수점 값을 제거
```

- `Math.random()`를 이용하여 `120 ~ 150` 사이의 난수를 정수로만 발생하게 하려면 다음와 같이 한다.

```javascript
Math.floor(Math.random()*31);       // 0부터 30까지 정수로 난수 발생
Math.floor(Math.random()*31) + 120; // 120부터 150까지 정수로 난수 발생
```

- 난수를 발생하게 하여 자신이 원하는 구간 사이에서 정수가 발생하게 하려면 다음과 같은 공식을 적용한다.

```javascript
Math.floor(Math.random()*(최댓값-최솟값+1)) + 최솟값;
```

### '가위, 바위, 보' 게임

- 사용자가 '가위, 바위, 보'를 적어 컴퓨터가 내려는 가위, 바위, 보를 추측해 맞추는 게임이다.

```javascript
document.write("<h1>가위, 바위, 보 게임</h1>");

var game = prompt("가위, 바위, 보 중 선택하세요!", "가위");
var gameNum;
switch(game) {
	case "가위":
		gameNum = 1; break;
	case "바위':
		gameNum = 2; break;
	case "보':
		gameNum = 3; break;
	default: alert("잘못 작성했습니다.");
		location.reload();
}

var com = Math.ceil(Math.random()*3); // 1~3 사이의 난수 발생

document.write("<img src = \"images/math_img_>" + com + ".jpg\">");

if (gameNum == com) {
	document.write("<img src=\"images/game_1.jpg\">");	
} else {
	document.write("<img src=\"images/game_2.jpg\">");
}
```

## (4) 배열 객체

- 변수에는 데이터가 한 개만 저장된다. 여러 개의 데이터를 하나의 장소에 저장하려면 배열 객체(Array Object)를 생성해야 한다. 배열은 '**나눌 배**'와 '**열거할 열**'을 사용해 만든 글자로, 글자 뜻 그대로 하나의 저장소를 나눠서 데이터를 열거라하는 의미이다.
- 배열 객체를 생성하는 기본적인 방법은 세 가지가 있다.

```javascript
① var 참조변수 = new Array();
	참조 변수[0] = 값1; 참조 변수[1] = 값2; 참조 변수[2] = 값3; ... 참조 변수[n-1] = 값n;
② var 참조 변호 = new Array(값1, 값2, 값3, ... 값n);
③ var 참조 변수 = [값1, 값2, 값3, ... 값n]
```

- 객체 생성 예) 각각의 데이터는 배열로 나누어진 저장소에 나열되고, 각각의 저장소에는 인덱스 번호가 부여된다. 인덱스 번호는 `0`부터 시작한다.

```javascript
var d = new Array();
d[0] = 30;
d[1] = "헬로우";
d[2] = true;
```

```javascript
var d = new Array(30, "헬로우", true);
```

```javascript
var d = [30, "헬로우", true];
```

### 배열 객체에 저장된 데이터 불러오기

- 배열 객체에 저장된 데이터를 불러올 때는 다음과 같은 기본형을 사용한다.

```javascript
참조 변수[인덱스 번호];
```

- 배열에 저장된 데이터를 불러오는 예

```javascript
var arr = [30, "헬로우", true];

document.write(arr[0]);
document.write(arr[1]);
document.write(arr[2]);
```

### 배열 객체의 메서드와 속성

- `join(연결 문자)` : 배열 객체의 데이터를 연결 문자 기준으로 1개의 문자형 데이터로 반환한다.
- `reverse()` : 배열 객체의 데이터 순서를 거꾸로 바꾼 후 반환한다.
- `sort()` : 배열 객체의 데이터를 오름 차순으로 정렬한다.
- `slice(index1, index2)` : 배열 객체의 데이터 중 원하는 인덱스 구간만큼 잘라서 배열 객체로 가져온다.
- `splice()` : 배열 객체의 지정 데이터를 삭제하고 그 구간에 새 데이터를 삽입할 수 있다.
- `concat()` : 2개의 배열 객체를 하나로 결합한다.
- `pop()` : 배열에 저장된 데이터 중 마지막 인덱스에 저장된 데이터를 삭제한다.
- `push(new data)` : 배열 객체의 마지막 인덱스에 새 데이터를 삽입한다.
- `shirt()` : 배열 객체에 저장된 데이터 중 첫 번째 인덱스에 저장된 데이터를 삭제한다.
- `unshift(new data)` : 배열 객체에 가장 앞의 인덱스에 새 데이터를 삽입한다.
- `length` : 배열에 저장된 총 데이터의 개수를 반환한다.

### 배열 객체의 메서드 활용

- `join()`, `concat()`, `slice()`, `sort()`, `reverse()` 사용하기

```javascript
var arr_1 = ["대치", "도곡", "매봉", "양재"];
var arr_2 = ["역삼", "선릉", "삼성"];

var result = arr_1.joing("&");
console.log(result); // 대치&도곡&매봉&양재

result arr_1.concat(arr_2);
console.log(result); // ["대치", "도곡", "매봉", "양재", "역삼", "선릉", "삼성"]

result = arr_1.slice(1, 3);
console.log(result); // ["도곡", "매봉"]

arr_2.sort(); // 오름차순 정렬
console.log(arr_2); // ["삼성", "선릉", "역삼"]

arr_1.reverse();
console.log(arr_1); // ["양재", "매봉", "도곡", "대치"]
```

- `splice()`, `pop()`, `push()`, `shift()`, `unshift()` 사용하기

```javascript
var greenArr = ["교대", "방배", "강남"];
var yellowArr = ["미금", "정자", "수서"];

greenArr.splice(2, 1, "서초", "역삼"); // 2번 인덱스부터 1개 데이터 삭제 후 "서초", "역삼" 삽입
console.log(greenArr); // ["교대", "방배", "서초", "역삼"]

var data1 = yellowArr.pop(); // 배열의 마지막 인덱스 데이터 꺼내오기 -> "수서"
var data2 = yellowArr.shift(); // 배열의 가장 앞쪽의 인덱스 데이터 꺼내오기 -> "미금"

yellowArr.push(data2); // 가장 마지막 인덱스에 데이터 넣기 
console.log(yellowArr); // ["정자", "미금"]
****
yellowArr.unshift(data1); // 가장 앞쪽의 인덱스에 데이터 넣기
console.log(yellowArr); // ["수서", "정자", "미금"]
```

## (5) 문자열 객체

- 문자열 객체(String Object) 는 문자형 데이터를 객체로 취급하는 것이다.

### 문자열 객체 생성하기

- 문자열 객체를 생성하는 기본형은 new 키워드와 String() 메서드를 사용하는 것이다. 생성된 객체는 변수에 참조한다.

```javascript
var 참조 변수 = new String(문자형 데이터);
```

```javascript
var str = new String("Hello, World!");
```

- 문자열 객체는 참조 변수에 문자형 데이터만 입력해도 객체가 생성된다.

```javascript
var 참조 변수 = 문자형 데이터;
```

```javascript
var str = "Hello, World!";
```

### 문자열 객체의 메서드 및 속성

- `charAt(index)` : 문자열에서 인덱스 번호에 해당하는 문자를 반환
- `indexOf("찾을 문자")` : 문자열에서 왼쪽부터 찾을 문자와 일치하는 문자를 찾아 제일 먼저 일치하는 문자의 인덱스 번호를 반환, 찾는 문자가 없으면 `-1`을 반환
- `lastIndexOf("찾을 문자")` : 문자열에서 오른쪽부터 찾을 문자와 일치하는 문자를 찾아 제일 먼저 일치하는 문자의 인덱스 번호를 반환, 찾는 문자가 없으면 `-1`을 반환
- `match("찾을 문자")` : 문자열에서 왼쪽부터 찾을 문자와 일치하는 문자를 찾아 제일 먼저 찾은 문자를 반환, 찾는 문자가 없으면 `null`을 반환
- `replace("바꿀 문자", "새 문자")` : 문자열에서 왼쪽부터 바꿀 문자와 일치하는 문자를 찾아 제일 먼저 찾은 문자를 새 문자로 치환
- `search("찾을 문자")` : 문자열에서 왼쪽부터 찾을 문자와 일치하는 문자를 찾아 제일 먼저 일치하는 인덱스 번호를 반환
- `slice(a, b)` : a개의 문자를 자르고 b번째 이후에 문자를 자른 후 남은 문자를 반환

```javascript
var str = "Hello, World!";
str.slice(2, 9); // "llo, Wo" 반환
```

```javascript
var str = "Hello, World!";
str.slice(3, -3); // "lo, Wor" 반환 (-1은 뒤에서부터 첫 번재 글자를 가리킴)
```

- `substring(a, b)` : a 인덱스부터 b 인덱스 이전 구간의 문자를 반환

```javascript
var str = "Hello, World!";
str.substring(2, 9); // "llo, Wo" 반환
```

```javascript
var str = "Hello, World!";
str.substring(3, -3); // "Hel" 반환 (-1은 인덱스 0을 가리킴)
```

- `substr(a, 문자 개수)` : 문자열에 a 인덱스부터 지정한 문자 개수만큼 문자열을 반환
- `split("문자")` : 지정한 문자를 기준으로 문자 데이터를 나누어 배열에 저장하여 반환
- `toLowerCase()` : 문자열에서 영문 대문자를 모두 소문 대문자로 변환
- `toUpperCase()` : 문자열에서 영문 소문자를 모두 대문자로 변환
- `length` : 문자열에서 문자의 개수를 반환
- `concat("새로운 문자")` : 문자열에 새로운 문자열을 결합
- `charCodeAt(index)` : 문자열 index에 해당 문자의 아스키 코드값을 반환
- `fromCharCode(아스키 코드 값)` : 아스키 코드 값에 해당하는 문자를 반환
- `trim()` : 문자의 앞 또는 뒤의 공백 문자열을 삭제

### 문자열 객체의 메서드 활용

- 방문자로부터 이름을 영문으로 입력받은 후 방문자가 영문 이름을 소문자로 작성했을 경우 대문자로 바꿔 출력하도록 한다. 또한, 연락처를 입력받은 후 전화번호 뒤의 네 자리는 `*`로 출력되도록 한다.

```javascript
var inputName = prompt("영문 이름을 입력하세요 : ", "");

var userName = inputName.toUpperCase();
document.write(userName, "<br>");

var inputNum = prompt("연락처를 입력하세요 : ", "");
var userNum = inputNum.substring(0, userNum.length - 4) + "****";
document.write(result, "<br>");
```

- 사용자로부터 입력받은 이메일의 유효성을 검사한다.

```javascript
var userEmail = prompt("이메일 주소를 입력하세요 : ", "");
var arrUrl = [".co.kr", ".com", ".net", ".or.kr", ".go.kr"];

var check1 = false;
var check2 = false;

// "@"를 정상적으로 작성했으면 check1에 true 저장
if (userEmail.indexOf("@") > 0) {
	check1 = true;
}

// 입력한 이메일과 arrUrl의 단어를 비교, 1개의 단어라도 일치하면 check2에 true 저장
for (var i = 0; i < arrUrl.length; i++) {
	if (userEmail.indexOf(arrUrl[i]) > 0) {
		check2 = true;
	}	
}

// check1과 check2에 true가 저장되어 있으면 유효한 이메일
if (check1 && check2) {
	document.write(userEmail);
} else {
	alert("이메일 형식이 잘못되었습니다.");
}
```

# 04-3 브라우저 객체 모델

## (1) 브라우저 객체란?

- 브라우저에 내장된 객체를 '브라우저 객체'라 한다. window는 브라우저 객체의 최상위 객체이며, window 객체에는 하위 객체가 포함되어 있다.
- 브라우저 객체는 계층적 구조로 이루어져 있으며, 이를 브라우저 객체 모델(**BOM**, Browser Object Model)이라 한다.

![https://s3-us-west-2.amazonaws.com/secure.notion-static.com/853647ea-520d-4b95-ae30-4f4e58b07ba4/10fig01.gif](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/853647ea-520d-4b95-ae30-4f4e58b07ba4/10fig01.gif)

## (2) window 객체

- window는 브라우저 객체의 최상위 객체이다.

### window객체의 메서드 종류

- `open("URL", "새 창 이름", "새 창 옵션")` : URL 페이지를 새 창으로 나타냄
- `alert(data)` : 경고 창을 나타내고 데이터를 보여줌, [확인] 버튼을 누르면 alert()를 사용한 다음 위치의 코드를 수행함
- `prompt("질문", "답변")` :  질문과 답변으로 질의응답 창을 나타냄
- `comfirm("질문 내용")` : 질문 내용으로 확인이나 취소 창을 나타냄, [확인] 버튼을 누르면 true를 반환하고 [취소] 버튼을 누르면 false를 반환함
- `moveTo(x, y)` : 지정한 새 창의 위치를 이동함
- `resizeTo(width, height)` : 지정한 새 창의 크기를 변경함
- `setInterval(function() { ... }, 일정 시간 간격)` : 지속적으로 일정한 시간 간격으로 함수를 호출하여 코드를 실행함
- `setTimeout(function() { ... }, 일정 시간 간격)` : 단 한 번 일정한 시간 간격으로 함수를 호출하여 코드를 실행함

### `open()`

- `open()` 메서드를 이용하면 지정한 URL 페이지를 새 브라우저 창에 나타낼 수 있다. 즉, 이 기능을 이용하면 광고에서 자주 사용되는 팝업 창을 만들 수 있다.
- `open()` 메서드의 기본형은 다음과 같다.

```javascript
open("URL", "새 창 이름", "새 창 옵션")
```

- **새 창 옵션의 종류**
    - `width` : 새 창의 너비를 설정
    - `height` : 새 창의 높이를 설정
    - `left` : 새 창의 수평(x축) 위치를 설정
    - `top` : 새 창의 수직(y축) 위치를 설정
    - `scrollbars` : 새 창의 스크롤바의 숨김/노출 설정(`yes`/ `no`)
    - `location` : 새 창의 URL 주소 입력 영역의 숨김/노출 설정(`yes`/ `no`)
    - `status` : 새 창의 상태 표시줄 영역의 숨김/노출 설정(`yes`/ `no`)
    - `toolbars` : 새 창의 도구 상자 영역의 숨김/노출 설정 (`yes`/ `no`)

### `open()` 메서드를 이용해 팝업 창 나타내기

- 팝업 창을 나타내려면 2개의 웹페이지가 필요하다. 하나는 팝업 창으로 나타낼 페이지이고, 또 하나는 팝업 창이 나타날 수 있게 해주는 오프너 페이지이다.
- `popup.html` : 팝업 창으로 나타낼 페이지

```html
<body>
	<p>
		<img src="image/image.png" usemap="#intro" alt="이미지">
		<map name ="intro" id="intro">
			<area shape="rect" coords="230,368,280,390" href="#" alt="창 닫기"
			onclick="window.close();">
		</map>
	</p>
</body>
```

- `opener.html` : 오프너 페이지, 새 창의 너비는 `300px` 높이는 `400px`이고 스크린을 기준으로 왼쪽에서 `200px` 위쪽에서 `50px` 만큼 떨어진 위치에서 팝업 창이 생성되도록 설정

```html
<script>
	window.open("popup.html", "popup", "width=350, height=400, left=200, top=50");
</script>
```

### `alert()`

- `alert()`는 경고 창을 나타낼 때 사용한다. `window.alert()` 메서드는 window 객체를 따로 작성하지 않아도 사용할 수 있다.

```javascript
alert("경고 메세지");
```

- 경고창은 `[확인]` 버튼을 클릭해야 `alert()` 메서드 다음에 나오는 코드를 실행한다.

### `prompt()`

- `prompt()`는 질의 응답 창을 나타낼 떄 사용한다. `window.prompt()` 메서드 역시 window 객체를 따로 작성하지 않고도 사용할 수 있다.

```javascript
prompt("질문", "기본 답변");
```

- 사용자가 질의응답 창의 `[확인]` 버튼을 클릭하면 입력한 답변을 반환한다.

### `confirm()`

- `confirm()`은 확인/취소 창을 나타낼 때 사용한다. `window.confirm()` 메서드 역시 window 객체를 따로 작성하지 않고도 사용할 수 있다.

```javascript
confirm("질문");
```

- `confirm()` 메서드를 사용하면 `[확인]` 또는 `[취소]` 버튼을 클릭하도록 유도할 수 있는데, 이때 `[확인]` 버튼을 클릭하면 `true`를 반환하고 `[취소]` 버튼을 클릭하면 `false`를 반환한다.

## (3) 일정 시간 간격으로 코드 실행하기

- `setInterval()`은 일정한 시간 간격으로 코드를 반복해서 실행하고, `setTimeout()`은 일정한 시간 후에 코드를 한 번만 실행하고 종료한다.

### `setInterval()` / `clearInterval()`

- `setInterval()` 메서드는 일정 시간 간격으로 코드를 반복 실행하고, `clearInterval()` 메서드는 `setInterval()` 메서드를 취소한다.
- `setInterval()` 메서드를 사용할 때, 시간 간격은 1/1,000초 단위(ms)로 작성해야 한다. 즉 3초 간격으로 설정하려 한다면, 3,000(3,000 * 1/1,000)으로 작성해야 한다.

```javascript
① var 참조 변수 = setInterval(function() { ... }, 시간 간격(ms));
② var 참조 변수 = setInterval("코드", 시간 간격(ms));
```

- `setInterval()`을 참조한 변수를 이용하여 `clearInterval()`을 사용한다.

```javascript
clearInterval(참조 변수);
```

- `setInterval()` 메서드를 이용하여 일정한 간격으로 변수의 값을 변화시키는 프로그램을 작성한다. `setInterval()` 메서드를 이용하여 3초마다 변수 `auto_1`의 데이터를 1씩 증가시키고, `auto_2`의 데이터는 1,000에서 1씩 감소시킨다. 그리고 `[증가 정지]`, 혹은 `[감소 정지]` 버튼을 클릭하면 자동으로 증가/감소하던 데이터가 정지된다.

```html
<script>
	var addNum = 0;
	var subNum = 1000;
	
	var auto_1 = setInterval(function() {
		addNum++;
		console.log("subNum: " + subNum);
	}, 3000);

	var auto_2 = setInterval(function() {
		addNum--;
		console.log("subNum: " + subNum);
	}, 3000);
</script>

...

	<button onclicn="clearInterval(auto_1)">증가 정지</button>
	<button onclicn="clearInterval(auto_2)">감소 정지</button>

</body>
```

### `setTimeout()` / `clearTimeout()`

- `setTimeout()` 메서드는 일정 시간이 지나면 코드를 실행하고 종료한다. `setTimeout()` 메서드를 응용하여 재귀 호출을 하면, `setInterval()` 메서드처럼 사용할 수도 있다. `clearTimeout()` 메서드는 `setTimeout()` 메서드를 제거한다.
- setTimeout() 메서드를 사용할 때 시간 간격은 밀리초(ms) 단위로 작성해야 한다. 예를 들어 5초 간격은 '5,000'을 입력한다.

```javascript
① var 참조 변수 = setTimeout(function() { ... }, 시간 간격(ms));
② var 참조 변수 = setTimeout("코드", 시간 간격(ms));
```

- `setTimeout()`을 참조한 변수를 이용하여 `clearTimeout()`을 사용한다.

```javascript
clearTimeout(참조 변수);
```

- `setTimeout()` 메서드를 이용해 지정한 시간 간격으로 단 한 번 실행되어 변수 `i`에 값을 증가시킨 후 콘솔 패널에 `i` 값을 출력하는 프로그램을 작성한다.

```javascript
var addNum = 0;
var auto = setTimeout(function(){
	addNum++;
	console.log(addNum);
}, 5000);
```

## (4) screen 객체

- screen 객체는 사용자의 모니터 정보(속성)를 제공하는 객체이다. 예를 들어 모니터의 너비나 높이 또는 컬러 표현 bit를 반환한다.

```javascript
screen.속성;
```

### screen 객체의 속성 종류

- `screen.width` : 화면의 너빗값 반환
- `screen.height` : 화면의 높잇값 반환
- `screen.availWidth` : 작업 표시줄을 제외한 화면의 너빗값 반환
- `screen.availHeight` : 작업 표시줄을 제외한 화면의 높잇값 반환
- `screen.colorDepth` : 사용자 모니터가 표현 가능한 컬러 bit 반환

## (5) location 객체

- location 객체는 사용자 브라우저와 관련된 속성과 메서드를 제공하는 객체이다. 현재 URL에 대한 정보(속성)와 새로 고침(reload) 메서드를 제공한다.

```javascript
①location.속성;
②location.메서드();
```

- 사용자 브라우저의 URL 경로 값을 가져온다.

```javascript
location.href;
```

- 사용자 브라우저의 URL 경로를 지정한 URL 주소로 변경한다.

```javascript
location.href = "https://www.naver.co.kr";
```

- 사용자 브라우저를 새로 고침한다.

```javascript
location.reload();
```

### location 객체의 속성 종류

- `location.href` : 주소 영역의 참조 주소를 설정하거나 URL을 반환
- `location.hash` : URL의 해시값(#에 명시된 값)을 반환
- `location.hostname` : URL의 호스트 이름을 설정하거나 반환
- `location.host` : URL의 호스트 이름과 포트 번호를 반환
- `location.protocol` : URL의 프로토콜을 반환
- `location.search` : URL의 쿼리(요청값)를 반한
- `location.reload()` : 브라우저를 새로 고침

## (6) history 객체

- history 객체는 사용자가 방문한 사이트의 기록을 남기고 이전 방문 사이트와 다음 방문 사이트로 다시 돌아갈 수 있는 속성과 메서드를 제공한다.

```javascript
①history.속성;
②history.메서드();
③history.메서드(n);
```

- 사용자가 방문한 사이트의 기록을 남긴 총 수량을 가져온다.

```javascript
history.length;
```

- 사용자가 방문한 사이트 중 바로 이전에 방문한 사이트로 이동한다.

```javascript
history.back();
```

- 사용자가 방문한 사이트 중 두 단계 이전에 방문한 사이트로 이동한다.

```javascript
history.bakc(2);
```

### history 객체의 속성 종류

- `history.back()` : 이전 방문 사이트로 이동
- `history.forward()` : 다음 방문 사이트로 이동
- `history.go(이동 숫자)` : 이동 숫자에 `-2`를 입력하면 2단계 이전의 방문 사이트로 이동
- `history.length` : 방문 기록에 저장된 목록의 개수를 반환

## (7) navigator 객체

- navigator 객체는 현재 방문자가 사용하는 브라우저 정보와 운영체제 정보를 제공하는 객체이다.

```javascript
navigator.속성;
```

### navigator 객체의 속성 종류

- `navigator.appCodeName` : 현재 브라우저의 코드명을 반환, 현 시점의 모든 브라우저는 "Mozilla"를 반환
- `navigator.appName` : 현재 브라우저의 이름을 반환, 현 시점의 모든 브라우저는 "Netscape"를 반환
- `navigator.appVersion` : 현재 브라우저의 버전 정보를 반환, 현 시점의 모든 브라우저는 "5.0(Windows)"를 반환
- `navigator.language` : 현재 브라우저가 사용하고 있는 언어를 반환, 한국어를 사용할 경우에는 "ko"를 반환
- `navigator.product` : 현재 브라우저의 엔진 이름을 반환, 크롬의 경우는 "Gecko"를 반환
- `navigator.platform` : 현재 컴퓨터의 운영체제 정보를 제공, 운영체제가 윈도우이고 시스템 종류가 64비트라도 브라우저가 32비트로 설치되었다면 "Win32"라고 나타남
- `navigator.onLine` : 온라인 상태 여부에 대한 정보를 제공, 만일 인터넷이 정상적으로 연결되어 있는 상태라면 true값을 반환
- `navigator.userAgent` :  브라우저와 운영체제의 종합 정보를 제공

### 브라우저 객체 모델을 사용해 운영체제와 스크린 정보 얻기

- 방문자의 운영체제 정보와 스크린 사이즈 정보를 출력하는 프로그램을 작성한다. 이렇게 방문자의 운영체제 정보를 알 수 있으면 현재 사이트를 방문한 사람이 데스크톱 PC를 이용해 방문했는지, 모바일을 이용해 방문했는지 파악할 수 있다. 또한 현재 방문자의 스크린 사이즈 정보를 알면 사이즈마다 다양한 자바스크립트를 적용할 수 있다.
- 
```html
<script>
	var info = navigator.userAgent.toLoserCase();
	var oslmg = null;

	if(info.indexOf('windows') > 0) {
		oslmg = "windows.png";
	} else if(info.indexOf('macintosh') > 0) {
		oslmg = "macintosh.png";
	} else if(info.indexOf('iphone') > 0) {
		oslmg = "iphone.png";
	} else if(info.indexOf('android') > 0) {
		oslmg = "android.png";
	}

	document.write("<img src=\"images/" + oslmg + "\">", "<br>");
	var scr = screen;
	var sc_w + scr.width;
	var sc_h = scr.height;

	document.write("모니터 해상도 너비:" + sc_w + "px", "<br>");
	document.write("모니터 해상도 높이:" + sc_h + "px", "<br>");
<script>
```