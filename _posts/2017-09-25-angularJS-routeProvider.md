## Routing
>app.js

		var app = angular.module('GalleryApp', ['ngRoute']);
		app.config(function($routeProvider){
		  $routeProvider
		  .when('/',{
		    controller: 'HomeController',
		    templateUrl: 'views/home.html'
		  })
		  .when('/photos/:id',{
		    controller: 'PhotoController',
		    templateUrl: 'views/photo.html'
		    
		  })
		  .otherwise({
		    redirectTo: '/'
		  });
		});
		

app.config는 $routeProvider를 정의 한다.<br>
when('/' ~는 controller	를 연결한다.<br>

>HomeController.js

		app.controller('HomeController', ['$scope', 'photos', function($scope, photos) {
		  photos.success(function(data) {
		    $scope.photos = data;
		  });
		}]);   

photos	를 $scope를 통해서 저장.

>views/home.html

		<div class="main">
		  <div class="container">
		
		    <h2>Recent Photos</h2>
		    <div class="row">
		      <div class="item col-md-4" ng-repeat="photo in photos">
		        <a href="#/photos/{{$index}}">
		          <img class="img-responsive" ng-src="{{ photo.url }}">
		          <p class="author">by {{ photo.author }}</p>
		        </a>
		      </div>
		    </div>
		  </div>
		</div>

ng-repeat	를 이용하여 사진을 뿌려준다.<br>

??<br>
Otherwise if a user accidentally visits a URL other than /, we just redirect to / using .otherwise().

>app.js

		.when('/photos/:id',{
				    controller: 'PhotoController',
				    templateUrl: 'views/photo.html'
				   		   
		})
photos와 templateUrl을 연결한다.

>PhotoController.js

		app.controller('PhotoController', ['$scope', 'photos', '$routeParams', function($scope, photos, $routeParams) {
		  photos.success(function(data) {
		    $scope.detail = data[$routeParams.id];
		  });
		}]);
$routeParams가 $routeParams.id를 통해 Url의 id값을 찾아낸다.<br>
$scope.detail	은 다음 파일에서 사용하게 된다.
>photo.html

		<div class="photo">
		  <div class="container">
		    <img ng-src="{{ detail.url }}">
		    <h2 class="photo-title"> </h2>
		    <p class="photo-author"> </p>
		    <p class="photo-views"> {{detail.views | number}}</p>
		    <p class="photo-upvotes"> {{detail.upvotes | number}}</p>
		    <p class="photo-pubdate"> {{detail.pubdate | date}}</p>
		  </div>
		</div>







