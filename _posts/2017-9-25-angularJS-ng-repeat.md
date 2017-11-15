---
layout: post
title:  AngularJS_ng-repeat
---
## 반복되는 이미지,글,제목 띄우기
> MainController.js

		app.controller('MainController', ['$scope', function($scope) {
		$scope.apps = [ 
			  { 
			    icon: 'img/move.jpg', 
			    title: 'MOVE', 
			    developer: 'MOVE, Inc.', 
			    price: 0.99 
			  }, 
			  { 
			    icon: 'img/shutterbugg.jpg', 
			    title: 'Shutterbugg', 
			    developer: 'Chico Dusty', 
			    price: 2.99 
			  },
			  {
			    icon: 'img/gameboard.jpg',
			    title: 'Gameboard',
			    developer: 'Armando P.',
			    price: 1.99
			  },
			  {
			    icon: 'img/forecast.jpg',
			    title: 'Forecast',
			    developer: 'Forecast',
			    price: 1.99
			  }
			];
		}]);
		
>directives/appInfo.js

		app.directive('appInfo', function() { 
		return { 
		    restrict: 'E', 
		    scope: { 
		      info: '=' 
		    }, 
		    templateUrl: 'js/directives/appInfo.html' 
		  }; 
		});
		

>directives/appInfo.html

		<img class="icon" ng-src="{{ info.icon }}"> 
		<h2 class="title">{{ info.title }}</h2> 
		<p class="developer">{{ info.developer }}</p> 
		<p class="price">{{ info.price | currency }}</p>
		
>index.html

		 <div class="main" ng-controller="MainController">
		 	<div class="container">
		     <div class="card" ng-repeat="app in apps">
		      <app-info info="app"></app-info>
		     </div>
			</div>
		</div>