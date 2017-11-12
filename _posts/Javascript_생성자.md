#생성자 함수

## 생성자함수 개요
> 객체 생성하기

	function Student(name,korean){
		this.이름 = name;
		this.국어 = korean;
	
		this.getSun = function () {
			return this.국어 + ...;
		}
	}
	
	var student = new Student('박종훈',100);
	
> 객체 배열

	function Student(name,korean){
			this.이름 = name;
			this.국어 = korean;
	
		this.getSun = function () {
			return this.국어 + ...;
		}
	}
	
	var students = [];
	student.push(new Student('박종훈',100);
	student.push(new Student('김종훈',100);
	

## 프로토타입

객체를 1000개,200개 ... 많이 만들다 보면 공통 되는 함수가 여러번 생성된다.
이것은 낭비

	function Student(name,korean){
			this.이름 = name;
			this.국어 = korean;
	}
	
	Student.prototype.getSum = function () { return this.국어+...; }
	
함수의 공통되는 부분은 프로토 타입으로 만들어 재사용이 가능하게 한다.

## 캡슐화
개발자가 의도하지 않은 방향으로 사용자가 값을 입력하거나 할 경우 그러한 부분을 사용할 수 없도록 막는 기술

	function Student(n,s){
		var name = n;
		var score = s;

		this.getName = function() { return name; }
		this.getScore = function() { return score; }
		this.setName = function(n) { 	
			if(name이 숫자이면){
				throw '숫자는 입력 못합니다.';
			} else {
				name = name;
			}
	}
	
	Student.prototype.getNum = function() {
		return ...;
	}


## 상속
> 코드 3줄로 상속을 할 수 있다.<br>
>
-  base 속성에 생성자 함수를 넣고 실행
-  생성자 함수(people)의 프로토 타입에 Student의 프로토 타입을 넣은 것

	function people('사람') {
		this.base = Student;
		this.base('이름',20);//base 속성에 생성자함수 
	}
	
	people.prototype = Student.prototype;
	people.prototype.constructor = people;
		
		

더알아보기
es6 === typescript?


