

## controller의 parameter의 순서는 중요하다
### 10월 2일

		angular.module('ikarusNgApp')
		  .controller('Content_list', ['$scope','cntlist', function ($scope,cntlist) {
		    cntlist.getCons()
		      .then(function (response) {
		        console.log("in controllers")
		        $scope.contents = response.data.result;
		        console.log()
		      });
		  }]);
		  
'cntlist','$scope', function... 이렇게 했다가 1시간 헤맸다.


HTML에서 이미지를 크기에 맞에 비율을 조정하려면 background-size를 이용한다.


angularjs<br>

## datepicker가 안된다면 jquery가 겹처서이다.
### 10월 3일


## javascript url 가져오기
### 10월 4일

		var link = document.location.href;
		// '/'로 끊어서 마지막의 값 가져오기
		var link2 = document.location.href.split("/")
		link2[linkw.length-1];
		
margin-top, top의 차이 <br>
1. 마지막 컨텐츠로부터의 거리가 margin-top이다.<br>
2. top는 속한 div로부터의 거리


> 부트스트랩 그리드 방식 배우기
	 