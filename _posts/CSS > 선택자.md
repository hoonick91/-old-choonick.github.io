## CSS > 선택자


#### ul 태그 밑의 모든 li 태그의 폰트 컬러를 red로 바꾼다.  

	ul li {
		color:red
	} 

#### ol 바로 밑에 있는 li에 대해서만 스타일을 설정할 때(직계 자손에 대해서만)

	ol >li {
		border: 1px solid red;
	}
	

#### ul,ol 태그 모두의 스타일을 변경하고 싶을 때
	ul,ol {
		background-color:red;
	}
	


