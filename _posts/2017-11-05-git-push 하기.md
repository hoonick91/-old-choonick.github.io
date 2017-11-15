# git push 하기

### local 부분
---
```
$ mkdir 폴더명 //폴더 만들기
$ cd 폴더명 //폴더로 들어가기
$ git init //폴더 경로에 git을 적용시키기

```
#### 파일생성하기

```
$ vi text.txt
```
에디터에서 'i'누른 후 아무 텍스트나 입력하고 :wq 엔터
#### commit하기
```
$ git add . //statge에 올리기
$ git commit -m "hello" //commit메시지 입력
```
<br>
### remote 생성
---
```
$ git remote add origin https://github.co...
```

#### pull 하기 (github에 기존 파일이 있으면)
```
$ git pull origin master
```

#### push 하기(pull 이후, 기존 파일이 없으면)
```
$ git push origin master
```
