---
layout: post
title:  [jQuery] pagination
---
## paging
> 서버에서 페이지의 개수를 받고, 그 수만큼 태그를 만들어준다.

.js

	<script>
	  var pagenum = 7; //서버에서 값을 받아오는 부분
	  var tag = '<li><a href="#">1</a></li>';
	
	  for (var i = 0; i < pagenum; i++) {
	    $('.pagination').append(tag);//3개를 추가한다
	  }
	
	  for (var i = 0; i < pagenum; i++) {
	    $('.pagination').children().children().eq(i).text(i+1);
	    $('.pagination').children().children().eq(i).attr('href','http://'+i+1);
	  }
	</script>
			

.html


   	<ul class="pagination"></ul>


## 한번씩 따라해보는 jQuery 함수 사전


### attr 태그에 속성을 부여한다.
	$('').attr('속성','value');


1. 노드 찾기



 - 속성으로 노드 찾기 : $("[속성이름=값]")

 - 찾은 요소 개수 구하기 :  .size()    ,     .length

 - 찾은 요소 n번째 접근하기 : .eq(index)    ,    .each(function(index){});

 - 찾은 요소에서 특정요소만을 걸러내기 : .filter("선택자")

 - 찾은 요소에서 특정 자식요소만 찾기 :  .find("선택자")

2. 자식 노드 찾기 

 - 전체 자식 노드 찾기
    -- 텍스트 노드 포함 전체 자식 노드 찾기 :  $("선택자").contents()
    -- 텍스트 노드 제외한 전체 자식 노드 찾기 : $("선택자").children("선택자")

 - n번째 자식 노드 접근
    -- $("선택자").children().eq(N)
    -- $("선택자").children(":eq(N)")

 - 첫번째 자식 노드 접근
    -- $("선택자").children().first()
    -- $("선택자").children(":first")
    -- $("선택자").children().eq(0)
    -- $("선택자").children(":eq(0)")

 - 마지막 자식 노드 접근
    -- $("선택자").children().last()
    -- $("선택자").children(":last")
 
3. 부모 노드 찾기
 
 - 바로 위의 부모 : $("선택자").parent()

 - 모든 부모 찾기
    -- $("선택자").parents()  모든 부모
 - 모든 부모 중 선택자에 해당하는 부모 찾기
    -- $("선택자").parents("선택자")

4. 형제 노드 찾기

 - 이전 형제 노드 찾기
    -- $("선택자").prev()
    -- $("선택자").prevAll("선택자");

 - 다음 형제 노드 찾기
    -- $("선택자").next()
    -- $("선택자").nextAll("선택자");

5. 노드 생성,추가,이동,삭제

 - 생성
    -- $("노드")
    -- $("선택자").html("<노드>...</노드>")
    -- $("노드").clone()

 - 추가
    -- $기준노드.append($추가노드)
    -- $기준노드.prepend($추가노드)  
    
 - 삭제
    -- $("선택자").remove()


6. 텍스트 노드 다루기

 - 텍스트 노드 생성 : $("텍스트")
 
 - 텍스트 노드 추가 : $기준노드.append("텍스트")

 - 텍스트 노드 변경 : $기준노드.text("새로운 텍스트")

