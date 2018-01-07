# api 통신하기
### 1. 먼저 component.ts에 HttpClinent를 추가한다.

```
constructor(private http: HttpClient) { }
  ngOnInit() {
    this.getPenaltys();
  }
```

ngOnInit()은 처음에 실행해주는 것인데 angular lifecycle와 관련이 있다.


좀 이상해졌다. 기존의 httpClient의 import	부분이 바뀌었다. 두부분에 HttpClient, HttpClientModule를 추가해주어야한다.

#### /component.ts
```
import {HttpClient} from '@angular/common/http';
...
constructor(private http: HttpClient) { }
  ngOnInit() {
    this.getPenaltys();
  }

```

#### /app.module.ts
```
import {HttpClientModule} from '@angular/common/http';
...
 ],
  imports: [
    BrowserModule,
    NgbModule.forRoot(),
    HttpClientModule
  ],
...

```

#### 2. get요청하는 함수를 작성한다.

#### /component.ts
```
...
  ngOnInit() {
    this.getUserList();
  }

  getUserList(){

    return this.http.get(this.BASE_URL+'/penalty').subscribe(Response=>{
      // console.log(Response.list);
      this.users = Response.list;
      console.log(this.users);
    })
...
```

ngOnInit()에 함수를 넣어줌으로 화면이 불러오자마자 함수가 실행되게 한다.


하지만 이부분은 컴포넌트 중심설계의 angular와는 효율이 맞지 않는다 같은 get요청을 컴포넌트 마다 새로 정의해주어야 하기 떄문이다. 그래서 api라는 service를 만들어 공통적으로 만들기로 한다.


