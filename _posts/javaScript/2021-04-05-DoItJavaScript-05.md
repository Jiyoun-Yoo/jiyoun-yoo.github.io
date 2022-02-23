---
title: '[Do it! 자바스크립트 + 제이쿼리 입문] 06 함수'
categories:
- JavaScript
tag:
- [javaScript, jQuery]
last_modified_at: '2021-04-05 22:00:00 +0800'
---

출처 : [Do it! 자바스크립트 + 제이쿼리](http://www.easyspub.co.kr/20_Menu/BookView/253/PUB)

---

# 05-1 함수

## (1) 함수란?

- 변수에는 데이터만 저장할 수 있고, 코드는 저장할 수 없다. 하지만 함수를 사용하면 코드를 메모리에 저장했다가 필요할 때마다 호출하여 사용할 수 있다.

### 변수 vs 함수

- 변수
    - 1개의 데이터만 저장한다.
    - `var`라는 키워드를 이용하여 선언한다
    - 문자형, 숫자형, 논리형, 데이터를 보관한다
    - 객체를 참조한다.
- 함수
    - 자바스크립트 코드를 저장한다.
    - `function`이라는 키워드를 이용하여 선언한다.
    - 출력문, 제어문 등의 코드를 저장하고 데이터를 반환한다.

## (2) 기본 함수 정의문

- 함수를 사용하여 코드를 저장한 것을 함수 정의문이라 한다. 함수를 선언할 때는 `function` 키워드를 사용해 변수를 선언한다.

```javascript
function 함수명() {
	자바스크립트 코드;
}
```

- 익명 함수를 선언하고 변수에 참조할 수도 있다.

```javascript
참조 변수 = function() {
	자바스크립트 코드;
}
```

- 함수 정의 문 안에 작성된 코드는 즉시 실행되지 않는다. 함수는 메모리에 할당되어 대기하고 있다가 함수가 호출되면 실행된다.

```javascript
함수명();
참조 변수();
```

- 함수 정의문과 익명 함수를 변수에 참조하는 두 가지 방식으로 함수를 선언한 다음 각각을 호출하는 코드를 작성한다. 아래의 코드에서 `myFunc()`는 2회 실행되고, `theFunc()`는 1회 실행된다.

```html
<script>
	var count = 0;

	myFunc(); // 함수 호출문이 먼저 나오더라도, 호이스팅 방식이 적용되어 정상적으로 함수를 호출

	function myFunc() {
		count++;
		document.write("hello" + count, "<br>");
	}

	myFunc();

	var theFunc = function() {
		count++;
		document.write("bye" + count, "<br>");
	}

	theFunc();
</script>
```

- 함수 정의문을 이용해 `[배경 바꾸기]` 버튼을 클릭할 대마다 배경색이 바뀌는 프로그램을 작성한다. 처음에는 배경색이 흰색이지만, 버튼을 클릭할 때마다 '노란색', '아쿠아색', '보라색' 순으로 바뀌도록 한다.

```html
<script>
	var color = ["white", "yellow", "aqua", "purple"];
	
	var i = 0;
	function changeColor() {
		i++;
		if (i >= color.length) {
			i = 0;
		}
		
		var bodyTag = document.getElementById("theBody");
		bodyTag.style.backgroundColor = color[i];
	}
</script>

</head>
<body id="theBody">
	<button onclick="changeColor();">배경 바꾸기</button>
</body>
```

- `getElementById()` 메서드는 `id` 값을 이용해 문서 객체(태그)를 선택하는 메서드이다. CSS의 아이디 선택자와 비슷한 역할을 한다. 선택한 문서 객체에 스타일을 적용하기 위해서는 문서 객체의 `sytle`에 접근하고 적용하고자 하는 속성에 새 값을 입력해야 한다.

```javascript
문서객체.style.스타일 속성=새 값;
```

### 일반 함수 정의 방식  vs 익명 함수 선언 참조 방식

- 일반 함수 정의는 함수 호출 시 호이스팅(hoisting) 기술을 지원한다. 그러나 익명 함수 선언 참조 방식은 호이스팅을 지원하지 않는다.
- 호이스팅을 적용하면 함수 정의문보다 호출문이 먼저 나와도 함수 정의문을 끌어올려 함수를 호출한다. 호이스팅의 사전적 의미는 '물건을 끌어올리다'이다.

## (3) 매개변수가 있는 함수 정의문

- 기본 함수 정의문은 함수를 호출할 때 값을 전달할 수 없었다. 하지만 매개변수가 있는 함수 정의문은 함수를 호출할 때 전달하고자 하는 값을 입력하여 호출할 수 있다. 이렇게 전달된 값은 매개변수가 받아 함수 정의문에서 사용할 수 있다.

```javascript
function 함수명(매개변수1, 매개변수2, ..., 매개변수n) {
	자바스크립트 코드;
}

함수명(데이터1, 데이터2, ..., 데이터n);
```

- 함수를 호출했을 때 이름과 사는 지역의 데이터를 함수 정의문의 매개변수 `name`과 `area`에 각각 전달하여 함수 안에 있는 실행문의 매개변수에 저장된 데이터를 불러와 출력하는 프로그램을 작성한다.

```html
<script>
	functiuon myFunc() {
		document.write("제 이름은 " + name + "입니다.", "<br>");
		document.write("사는 곳은" + area + "입니다." "<br><br>");
	}

	myFunc("유지연", "서울"); // 제 이름은 유지연입니다.
												 // 사는 곳은 서울입니다.
</script>
```

- 질의 응답 창(`prompt`)을 통해 방문자의 아이디와 비밀번호를 입력받아 만일 잘못된 아이디가 입력된 경우에는 **"존재하지 않는 아이디입니다."**라는 경고창을 나타내고, 잘못된 비밀번호가 작성된 경우에는 **"잘못된 비밀번호입니다."**라는 경고 창을 나타내는 프로그램을 작성한다. 아이디와 비밀번호가 일치하는 환영 문구가 출력되도록 한다.

```html
<script>
	var rightId="apple";
	var RightPw="1234"

	function login(id, pw) {
		if(id == rightId) {
			if(pw == rightPw) {
				document.write(id + "님 환영합니다!");
			} else {
				alert("잘못된 비밀번호입니다.");
			}
		} else {
			alert("존재하지 않는 아이디입니다.");
		}		
	}

	var userId = prompt("아이디 : ", "");
	var userPw = prompt("패스워드 : ", "");

	login(userId, userPw);	
</script>
```

## (4) 매개변수 없이 함수에 전달된 값 받아오기

- 함수 정의문에서 `arguments`를 사용하면 매개변수를 사용하는 것처럼 함수 호출문의 값을 받아올 수 있다. 함수 정의문의 매개변수가 없는 상태에서 데이터를 전달하여 함수를 호출하면 그 값은 배열에 저장된다. 함수 정의문에서는 그 값을 `arguments`라는 변수로 참조한다.

```javascript
function 함수명() {
	arguments;
}

함수명(데이터1, 데이터2, 데이터3); 
// arguments[0] = 데이터1, arguments[1] = 데이터2, arguments[3] = 데이터3
```

- 매개변수를 생략한 함수 호출문에서 3개의 숫자형 데이터를 전달하려고 한다. 숫자형 데이터는 배열에 저장되고 `arguments` 변수로 참조할 수 있다. `arguments`의 인덱스를 이용해 배열에 저장된 값을 불러올 수도 있다.

```javascript
function sum() {
	var sum = arguments[0] + arguments[1] + arguments[2];
	document.write(sum);
}

sum(10, 20, 30); // 60 출력
```

- 매개변수 없이 함수 호출문에 전달된 값들은 배열로 저장된다. 따라서 `for`문을 이용하여 배열에 들어 있는 값들을 꺼낼 수 있다.

```javascript
function sum() {
	var sum = 0;
	for(var i = 0; i < arguments.length; i++) {
		sum += arguments[i];
	}
	
	document.write(sum);
}

sum(10, 20, 30); // 60 출력
```

# 05-2 함수에서 return 문의 역할

- `return` 문은 함수에서 결괏값을 반환할 때 사용한다. 그리고 함수에서 `return` 문이 실행되면 반복문의 `break` 문과 비슷하게 코드가 강제로 종료된다. 즉, 함수 정의문에서 `return` 문이 사용되면 함수를 호출했을 때 결괏값(data)을 반환한다.

## (1) 데이터를 반환하고 강제 종료하는 return 문

- 함수 정의문에서 return문은 코드를 종료하고 결괏값을 반환한다. 따라서 return문 다음에 다른 코드가 오더라도 그 코드는 무시하고 데이터를 반환한다.

```javascript
function 함수명() {

	자바스크립트 코드;
	return 데이터;

	자바스크립트 코드; // return문 아래의 코드는 무시된다.
}

	var 변수 = 함수명(); // 함수 호출
```

- 함수 호출과 함께 인자값을 전달하고, 그 인자를 이용한 계산값을 반환하는 함수를 선언한다.

```javascript
function sum(num1, num2) {
	return num1 + num2;
}

var result = sum(10, 20);
document.write(result); // 30 출력
```

- 사용자로부터 값을 입력받아 함수에 전달하고, 계산관 결괏값을 return 문으로 함수 호출문에 반환하는 프로그램을 작성한다.

```html
<script>
	function testAvg(arrData) {
		var sum = 0;
		for(var i = 0; i < arrData.length; i++) {
			sum += Number(prompt(arrDate[i] + "졈수 : ", "0"));
		}
		
		var avg = sum /arrData.length;
		return avg;		
	}

	var arrSubject = ["국어", "수학"];
	var result = testAvg(arrSubject); 
	// 함수를 호출하면 매개변수가 전달된다. 반환된 값이 result에 저장된다.

	document.write("평균 점수 : " + result + "점");	
</script>
```

- 8개의 이미지를 사용해 갤러리를 만드는 프로그램을 작성한다. 처음 화면에는 `pic_1.jpg`가 나타나고, 여기서 `[다음]` 버튼을 누르면 `pic_2, 3, ... 8.jpg`가 순서대로 나타난다. 즉, 이미지 파일명이 1씩 증가되며 그림이 나타난다.  이미지는 `pic_8.jpg`까지만 있기 때문에 `9`가 나오면 오류가 발생한다. `8`보다 큰 값이 나오는 경우에는 `return`문으로 `num++` 이전에 함수를 종료한다.

```html
<script>
	var num = 1;
	function gallery(direct) {
		if(direct) {
			if(num == 8) {
				return;
			}
			num++;
		} else {
			if(num == 1) {
				return;
			}
			num--;
		}
		
		var imgTag = document.getElementById("photo");
		imgTag.setAttribute("src", "images/pic_" + num + ".jpg");
	}	
</script>

</head>
<body>
	<div>
		<p><img src="images/pic_1.jpg" id="photo" alt=""></p>
		<p>
			<button onclicn="gallery(0)">이전</button>
			<button onclicn="gallery(1)">다음</button>
		</p>
	</div>
</body>
```

- `setAttribute("속성명", "새 값")` 메서드는 선택한 태그의 지정한 속성을 새 값으로 바꾼다.

## (2) 재귀 함수 호출

- 함수 정의문 내에서 작성한 코드로 함수를 다시 호출하는 것을 재귀 함수 호출이라 한다. 재귀 함수 호출은 함수를 반복문처럼 여러 번 호출하기 위해 사용한다.

```javascript
function myFunc() {
	자바스크립트 코드;
	myFunction();
}
myFunction();
```

- 재귀 함수 호출을 적용하여 1부터 10까지의 값을 출력하는 프로그램을 작성한다.

```html
<script>
	var num = 0;
	function testFunc() {
		num++;
		document.write(num, "<br>");
		if (num == 10) { // num의 값이 10이면 함수가 종료되고, 더이상 재귀 함수를 호출하지 않는다.
			return;
		}
		
		testFunc();
	}

	testFunc();	
</script>
```

# 05-3 함수 스코프 개념 이해

## (1) 함수 스코프란?

- 스코프(scope)의 사전적 의미는 '범위'이며, 자바스크립트에서는 변수 또는 함수의 유효 범위를 가리킨다.
- 지역 변수란, 스코프 영역에서 선언한 변수를 가리킨다. 스코프 영역에서만 사용할 수 있다.
- 지역 함수란 스코프 영역에서 선언한 함수를 가리킨다. 스코프 영역에서만 호출할 수 있다.

## (2) 전역 변수와 지역 변수의 개념과 차이

- 전역 변수(Global Variables)는 자바스크립트 어디에서든 사용할 수 있는 변수이고, 지역 변수(Local Variables)는 함수 스코프에서만 사용할 수 있는 변수이다.

```javascript
var 변수명; // 전역 변수

function 함수명() {
	var 변수명; // 지역 변수
}
```

- 함수 스코프에서 선언한 변수는 지역 변수이며 함수 안에서만 사용할 수 있다. 아래의 경우, 함수 스코프에서 `score` 값을 50으로 변경해도 함수 스코프 밖의 `socre` 값은 10을 출력한다.

```javascript
var score = 10;

function myFunction() {
	var score = 50;
	
	alert(score); // 50 : 함수 스코프에서는 지역 변수 데이터를 가져온다.
}

myFunction();

alert(score); // 10 : 함수 스코프 밖에서는 전역 변수 데이터를 가져온다.
```

## (3) 전역 함수와 지역 함수의 차이

- 전역 함수는 자바스크립트 어디에서든 사용할 수 있는 함수이고, 지역 함수는 함수 스코프에서만 사용할 수 있는 함수이다.

```javascript
function globalFunc1() { // 전역 함수
	자바스크립트 코드;
}

function globalFunc2() {
	function localFunc() { // 지역 함수
		자바스크립트 코드;
	}
}
```

- 함수 스코프에서 선언된 함수는 지역 함수가 되어 함수 스코프에서만 호출할 수 있다.

```javascript
function myFunc() {
	alert("전역 함수");
}

function outerFunc() {
	function myFunc() {
		alert("지역 함수");
	}
	myFunc(); // 지역 함수 호출
}

myFunc(); // 전역 함수 호출 -> "전역 함수" 출력
outerFunc(); // "지역 함수" 출력
```

## (4) 전역과 지역을 나누는 이유

- 프로그램을 개발할 때 전역(Global)과 지역(Local)을 나누면 충돌을 피할 수 있다. 프로젝트의 규모가 클 때는 같은 이름의 전역 변수나 전역 함수를 사용하면 충돌이 발생한다. 같은 이름의 함수이지만, 지역 함수를 사용하여 함수를 선언했다면 함수가 충돌하는 불상사를 피할 수 있다.

### 즉시 실행 함수

- 지역 함수 선언에 사용하면 효과적인 즉시 실행 함수가 있다. 함수를 선언하는 동시에 함수를 호출하는 것이다.

```javascript
(function() {
	자바스크립트 코드;
}());
```

```javascript
(function() {
	var 변수명; // 지역 변수

	function 함수명() { // 지역 함수
		자바스크립트 코드;
	}
}());
```

- 아래와 같은 경우는 두 개발자가 동일한 변수명과 함수명을 사용하지만, 즉시 실행 함수에 지역 변수와 지역 함수를 선언하여 충돌을 피한 예이다.

```javascript
// A 개발자
(function() {
	var num = 100;
	function hello() {
		num += 100;
		alert(num);
	}
}();)

// B 개발자
(function() {
	var num = 100;
	function hello() {
		num += 100;
		alert(num);
	}
}();)
```

# 05-4 객체 생성자 함수의 활용

## (1) 객체 생성자 함수

- 내장 객체를 생성할 때는 이미 자바스크립트 엔진에 내장되어 있는 객체 생성자 함수(Object Constructor Function)를 사용하여 객체를 생성한다.
- 객체 생성자 함수를 선언하고 객체를 생성할 때, `new` 키워드를 사용해 객체를 생성하고 객체 생성자 함수에서 this 키워드를 사용해 생성한 객체에 속성과 함수를 등록한다.

```javascript
// 객체 생성자 함수
function 함수명(매개변수1, 매개변수2, ..., 매개변수n) {
	this.속성명 = 새 값;
	this.함수명 = function() {
		자바스크립트 코드;
	}
}

// 객체 생성
var 참조변수(인스턴스 네임) = new 함수명();

var 참조변수 = { 속성: 새 값, 함수명 : function() { ... } };
```

- 객체 생성자 함수를 선언하고 객체를 생성하는 프로그램을 작성한다. `CheckWeight`라는 이름으로 객체 생성자 함수를 선언하고 객체를 생성하는데, 생성된 각각의 객체에는 속성(이름, 키, 몸무게)과 함수(`getInfo()`, `getResult()`)를 등록한다.

```html
<script>
	function CheckWeight(name, height, weight) {
		this.userName = name;
		this.userHeight = height;
		this.userWeight = weight;
		this.minWeight;
		this.maxWeight;

		this.getInfo = function() {
			var str = "";
			str += "이름 : " + this.userName + ", ";
			str += 키 : " + this.userHeight + ", ";
			str += "몸무게 : " + this.userWeight + "<br>";
			return str;
		}

		this.getResult = function() {
			this.minWeight = (this.userHeight - 100)*0.9 - 5;
			this.minWeight = (this.userHeight - 100)*0.9 + 5;

			if (this.userWeight >= this.minWeight && this.userWeight <= this.maxWeight) {
				return "정상 몸무게 입니다.";
			} else if() {
				return "정상 몸무게보다 미달입니다.";				 
			} else {
				return "정상 몸무게보다 초과입니다.";	
			}
		}
	}
	
	var kim = new CheckWeight("김철수", 180, 80);
	var you = new CheckWeight("유지연", 168, 60);
	console.log(kim);
	console.log(you);

	document.write(you.getInfo()); // 객체의 속성 정보 반환
	document.write(you.getResult()); // 몸무게가 정상인지 판단하여 결과 반환

</script>
```

## (2) 메모리 절약을 위한 프로토타입 사용하기

- 객체 생성자 함수를 사용하여 객체를 생성하면 객체를 생성한 만큼 함수가 등록된다. 그리고 함수를 여러 개 등록하면 메모리 공간을 많이 차지하여 메모리를 낭비하게 된다. 이럴 경우에는 객체 생성자 함수에 **프로토타입(Prototype)**을 사용하여 함수를 등록하면 메모리 낭비를 줄일 수 있다.
- 프로토타입(Prototype)의 사전적 의미는 '원형'이다. 자바스크립트에서 '원형'은 객체 생성자 함수를 의미한다. 프로토타입을 사용하여 등록한 함수는 원형(객체 생성자 함수)에서 생성된 객체를 공유할 수 있다. 즉, 여러 개의 함수를 등록할 필요가 없다.

```javascript
function 함수명(매개변수1, 매개변수2, ... ,매개변수n) {
	this.속성명 = 새 값;
}

함수명.prototype.함수명 = function() {
	자바스크립트 코드;
}

var 참조변수(인스턴스 네임) = new 함수명();
```

- 객체를 생성할 때 프로토타입으로 함수를 등록하는 프로그램을 작성한다.

```html
<script>
	function CheckWeight(name, height, weight) {
		this.userName = name;
		this.userHeight = height;
		this.userWeight = weight;
		this.minWeight;
		this.maxWeight;
	}

	CheckWeight.prototype.getInfo = function() {
		var str = "";
		str += "이름 : " + this.userName + ", ";
		str += 키 : " + this.userHeight + ", ";
		str += "몸무게 : " + this.userWeight + "<br>";
		return str;
	}

	CheckWeight.prototype.getResult = function() {
		this.minWeight = (this.userHeight - 100)*0.9 - 5;
		this.minWeight = (this.userHeight - 100)*0.9 + 5;

		if (this.userWeight >= this.minWeight && this.userWeight <= this.maxWeight) {
			return "정상 몸무게 입니다.";
		} else if() {
			return "정상 몸무게보다 미달입니다.";				 
		} else {
			return "정상 몸무게보다 초과입니다.";	
		}
	}
	
	var kim = new CheckWeight("김철수", 180, 80);
	var you = new CheckWeight("유지연", 168, 60);
	console.log(kim);
	console.log(you);

	document.write(kim.getResult === you.getResult); // true 리턴
</script>
```

- `kim.getResult === you.getResult`가 `true`라는 것은 두 객체가 같은 함수를 사용하고 있다는 의미이다.

# 05-5 자바스크립트 내장 함수

## (1) 내장 함수

- 내장 함수란 자바스크립트 엔진에 내장된 함수를 말한다. 자바스크립트에 이미 내장된 함수이기 때문에 개발자가 함수를 직접 선언하지 않고도 바로 호출할 수 있다.

### 내장 함수의 종류

- `encodeURI()` : 문자를 유니 코드값으로 인코딩(영문, 숫자, 일부기호(`;` `,` `/` `?` `:` `@` `&` `=` `+` `$`)는 제외)
- `encodeURIComponent()` : 문자를 유니 코드값으로 인코딩(영문, 숫자 제외)

```javascript
encodeURI("?query=값"); // "?query=%EA%B0%91"
encodeURIComponent("?query=값"); // "3Fquery%3D%EA%B0%91"
```

- `decodeURI()` : 유니 코드값을 디코딩해서 다시 문자화
- `decodeURICompoenet()` : 유니 코드값을 디코딩해서 다시 문자화

```javascript
decodeURI("?query=%EA%B0%91"); // "?query=값"
decodeURICompoenet("3Fquery%3D%EA%B0%91"); // "?query=값"
```

- `parseInt()` : 문자열 데이터를 정수형 데이터로 반환
- `parseFloat()` : 문자열 데이터를 실수형 데이터로 반환

```javascript
parseInt("5.12"); // 5
parseInt("15px"); // 15
parseFloat("5.12"); // 5.12
parseFloat("65.5%"); // 65.5
```

- `String()` : 문자형 데이터로 반환
- `Number()` : 숫자형 데이터로 반환
- `Boolean()` : 논리형 데이터로 반환

```javascript
String(5); // "5"
Number("5"); // 5
Boolean(5); // true
Boolean(null); // false
```

- `isNaN()` : `is Not a Number`의 약자이며 숫자가 아닌 문자가 포함되어 있으면 `true`를 반환
- `eval()` : 문자형 데이터를 따옴표가 없는 자바스크립트 코드로 처리

```javascript
isNan("5-3"); // true
isNan("53"); // false
eval("15 + 5"); // 20
```