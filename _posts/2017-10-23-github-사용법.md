# github 사용법
## 내 로컬에서 업데이트한 내용을 github의 master로 push 하고싶을 때
> temp branch	에서 작업을 완료하고, 커밋까지 완료한 상태가 전제

1. master로 일단 이동
2. github의 master에서 내 local의 master로 pull
3. 충돌이 나면 해결한다.
4. temp에 있는걸 내 local의 master로 merge한다. 
		
		<in master> temp 와 merge 하고 싶을 때
		git merge temp

5. 충돌을 해결하면, 현재 local의 master와 temp가 합쳐진 상태이다. 그리고 다음과 같이 commit한다.

		git add .
		git commit -m "merge"
> 내  local master에 작업한것과 master가 merge된 상태

		git push origin master
		origin에 내 master를 push 한다.	
 