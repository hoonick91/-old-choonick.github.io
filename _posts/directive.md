# directive

## 1. 디렉티브란?
dom엘리먼트

- javascript : camelCase작명법으로 작성

		<my-example></my-example>
		<my:example></my:example>
		<my_example></my_example>
		

- html : snake-case


## 2. 디렉티브 생성 규칙

### restrict 
	E,A,C,M
### template
디렉티브를 보여줄 부분에 in-line value
### templateUrl

### replace 
작성한 템플릿을 html에 적용시킬건지
### priority 
호출 순서를 지정한다.

ng-transclude를 이용하여 template 또는 templateUrl에서 디렉티브내의 원보 

# ?컴포넌트

### controller()
다른 디렉티브들과 통신하기 위한 역할	
