---
layout: post
title:  [AngularJS] 이미지 base64 인코딩
---

## App.js
> module에 'angularFileUpload' 추가

#### angularFileUplad를 사용하기 위해서는 
bower install angular-file-upload 


## controller.js
> controller에 'fileUploader'추가하기

	.controller('Ad_write', ['$scope','FileUploader',
	function ($scope,FileUploader) {}
	
> controller 함수 작성하기

  $scope.uploader = new FileUploader();

    $scope.uploader.onAfterAddingFile = function (file) {
      //$upload 서비스를 통해 실제 비동기 업로드를 수행한다. 이떄 HTTP 경로와 메소드 그리고 해당 파일 필드이름을 지정할 수 있다.
      var reader = new FileReader();
      reader.readAsDataURL(file._file);
      // console.log(file);


      reader.onload = function () {


        // console.log(reader);
        console.log("in onload " + reader.result);
        $scope.board.base64 = reader.result;

      };
    };

### error
1. $scope.board.base64 undefined error
<br> html에서 ng-model = "board.base64" 정의