---
layout: post
title:  AngularJS_흐름
---

## AngularJS의 흐름
>installApp.JS<br>
>link는 유저의 action에 반응한다.


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
<br>	
>installApp.html

		<button class="btn btn-active" ng-click="download()">
		{{buttonText}}</button>
		
<br>
		
>index.html

		<div class="main" ng-controller="MainController">
			<div class="container">
				<div class="card" ng-repeat="app in apps">
					<app-info info="app"></app-info>
					<install-app></install-app>
				</div>
			</div>
		</div>