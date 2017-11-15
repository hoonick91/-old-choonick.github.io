## bootstrap
> 전체화면을 12개로 나누어 총 합이 12가 되어야 한다.

### container
	class="container"  > 화면 크기에 따라 고정된 크기 사용
	class="container-fluid" > 화면 크기에 따라 맞추어서 사용됨

<br>

### col-xs-12 col-sm-6
> 화면크기에 따라 다른 크기를 갖는다.

		<div class="row">
		    <div class="col-xs-12 col-sm-6 col-md-8" style="background-color: #1e7e34">
		        .col-xs-12 .col-sm-6 .col-md-8
		    </div>
		    <div class="col-xs-12 col-sm-6 col-md-4" style="background-color: #1b1e21">
		        .col-xs-12 .col-sm-6 col-md-4
		    </div>
		</div>
		
<div class="row">
    <div class="col-xs-12 col-sm-6 col-md-8" style="background-color: #1e7e34">
        .col-xs-12 .col-sm-6 .col-md-8
    </div>
    <div class="col-xs-12 col-sm-6 col-md-4" style="background-color: #FFF232">
        .col-xs-12 .col-sm-6 col-md-4
    </div>
</div>

<br>

### responsive utill
	<div class="col-md-3 visible-md"></div>
> 사이즈가 'md' 일때 나타난다.

<br>


### offset
	class="col-md-10 col-md-offset-2"
> col-md-10과 빈공간 2를 갖는다.





