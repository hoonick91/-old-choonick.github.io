# DDL

## create
###table
> 학생테이블 정의

	create table 학생
		(이름 varchar(15) not null,
		학번 char(8),
		생년월일 date, ...
		primary key(학번),
		foreign key(전공), references 학과(학과코드(
			on delete set null
			on update cascade,
		constraint 생년월일제약
			check(생년월일 >= '1980-01-01'));
			
#### varchar, char의 차이점
* char(15) - 항상 15바이트가 확보
* varchar(15) - 저장된 크기가 1이면 1바이트 만큼만 확보		

###view
> 서브쿼리의 결과로서 뷰를 생성

	create view 안산고객(성명, 전화번호)
	as select 성명, 전화번호
	from 고객
	where 주소 = '안산시';

###index
검색을 빠르게 하기 위해 만든 보조적인 데이터 구조
> 고객 테이블에서 **중복 값이 없는 속성**으로 인덱스를 생성하여(unique) 고객번호 속성에 대해 **내림차순**으로 정렬하여 '고객번호_idx'라는 이름으로 인덱스를 정의

	create unique index 고객번호_idx
		on 고객(고객번호 DESC);

###trigger
db 시스템에서 데이터 입력,갱신,삭제등의 이벤트가 발생했을떄 자동적으로 수행되는 사용자 정의 프로시저
> <학생> 테이블에 새로운 레코드가 삽입될 때(insert), 삽입되는 레코드에 학년 정보가 누락됐으면 학년 필드에 '신입생'을 치환하는 트리거를 '학년정보_tir' 라는 이름으로 정의하시오.

	create trigger 학년정보_tri before insert on 학생
	
	referenceing new table as new_table
	for each row
	where new_table.학년 = ''//학년 속성이 null인것에만 '학년정보_tri'가 적용
	begin
		set new_table.학년 = '신입생';
	end;

## alter table
> 학생 테이블에 최대 3문자로 구성되는 학년 속성을 추가

	alert table 학생 add 학년 varchar(3);

## drop

	drop table 학생 cascade; 
	drop table 학생 restrict;
	
#### cascade, restrict
* cascade - 제거할 개체를 참조하는 모든 개체를 함께 제거
* restrict - 다른 개체가 제거할 개체를 참조중일 경우 제거가 취소

	