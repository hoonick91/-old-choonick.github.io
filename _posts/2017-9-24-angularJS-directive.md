---
layout: post
title:  AngularJS_directive
---
## 사용자가 만드는 디렉티브
> 같은 형식의 컨텐츠를 여러번 보여주어야 할때<br> 
> 디렉티브를 만든다. 
> 먼저 js/directives/appInfo.js<br>
> 들어갈 껍데기를 만든다.
> 같은 경로에 html을 만들어 들어갈형식을 만든다.
> 즉, appInfo.js는 연결고리 역할을 하는 것이다.
> 메인 index.html에 <br>

		 <app-info info="move"></app-info>
		
		
가독성, 재사용이 directive의 목적

디렉티브 사용법.<br>

* MainController	에 값을 넣는다.
* appInfo.js	에 directive를 만들어 준다.
* appInfo.html 넣을 형식을 만들어준다.
* index.html	 
		
		<directive-name info=""/>
		
ng-repeat와 own directive를 함께 사용할 수 있다.
<br> 
> 과제에 디렉티브와 np-repeat 를 사용할 수 있을 것 같다.


<br>
## directive를 이용하여  install을 클릭하면 uninstall 바뀌게 하기
> directive를 사용한다는 것은 jQuery 사용을 지양하게 된다.

* directives/installApp.html
	* ng-click="download()", 
* /installApp.js

		app.directive('installApp', function() {
		  return {
		    restrict: 'E',
		    scope: {},
		    templateUrl: 'js/directives/installApp.html',
		    
		    link: function(scope, element, attrs) {
		      scope.buttonText = "Install",
		      scope.installed = false,
		
		      scope.download = function() {
		        element.toggleClass('btn-active')
		        if(scope.installed) {
		          scope.buttonText = "Install";
		          scope.installed = false;
		        } else {
		          scope.buttonText = "Uninstall";
		          scope.installed = true;
		        }
		      }
		    }
		  };
		});

## Service




> 		