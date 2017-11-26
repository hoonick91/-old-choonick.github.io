## 10월 20일 
####ng-bind-html
html 코드를 넣어준다.

RClick - localhistory - show history

## ionic, cordova 설치
npm install -g ionic

npm install -g cordova

## ionic serve --address [주소] --port [포트번호]

## ionic 구조

	<ion-nav-bar>
	    <ion-nav-back-button class="button-dark"></ion-nav-back-button>
	</ion-nav-bar>
	
	<ion-nav-view>
	</ion-nav-view>



## 정리

> index.html	

	<ion-pane>
	  <ion-nav-bar>
	  	    <ion-nav-back-button class="button-dark"></ion-nav-back-button>
	  	    //기본적으로 모든 화면에 backbutton이 나온다.
	  </ion-nav-bar>
	
	  <ion-nav-view>
	  </ion-nav-view>
	
	  <ion-footer-bar>
	  </ion-footer-bar>
	</ion-pane>

<br>

> main.html
		
	<ion-nav-view name="mainContent"></ion-nav-view>
	
<br>
	
> mainContent

	<ion-nav-view name="boardContent"></ion-nav-view>
	

<br>

> board.html



ion-nav-view - ion-view - ion-content

??nav-view, view의 차이점?

## has-header
>login.html

	<ion-view>
	
	  <ion-content class="has-header has-footer">
	    <!--<br>-->
	    <form ng-submit="login();">
	      <div class="lis
	      