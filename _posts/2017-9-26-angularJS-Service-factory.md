---
layout: post
title:  AngularJS_factory
---
## Service - factory

> js/services/forecast.js

		app.factory('forecast', ['$http', function($http) { 
		  return $http.get('https://s3.amazonaws.com/codecademy-content/courses/ltp4/forecast-api/forecast.json') 
		            .success(function(data) { 
		              return data; 
		            }) 
		            .error(function(err) { 
		              return err; 
		            }); 
		}]);
		
index.html에 script를 추가한다.

>controllers/MainController.js

		app.controller('MainController', ['$scope', 'forecast', function($scope, forecast) {
		  forecast.success(function(data){
		    $scope.fiveDay = data;
		  });
		
		  });
		}]);

factory의 배열에 'forecast'를 추가하고, $scope에 데이터를 저장.

### index.html에 {{fiveDay.days}}~ 방식