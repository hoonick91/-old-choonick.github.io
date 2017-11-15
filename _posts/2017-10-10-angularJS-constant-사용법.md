10월 9일 
##form ng-submit = "{functionname}();"

	<a>
	    <button class="ad_cnl_btn"></button>
	</a>
> 'a'태그를 없어주어야 ng-submit funtion이 반응한다.
	
	<button type="submit" class="ad_reg_btn"></button>

	
### angularjs constant 사용법
app.js

	.constant('BASE_URL', 'http://')
factory

	.factory('cntlist',['$http','BASE_URL', function ($http, BASE_URL) {
