# get 요청 하기

#### 1. ../app.module.ts
http 모듈을 추가시켜 준다.

```
import { BrowserModule } from '@angular/platform-browser';
import { AppComponent } from './app.component';
import { HomeComponent } from './home/home.component';
import {routing} from './app.routing';
import { ListComponent } from './list/list.component';
import {HttpClientModule} from '@angular/common/http';// 추가된 부분


@NgModule({
  declarations: [
    AppComponent,
    PostComponent,
    HomeComponent,
    ListComponent
  ],
  imports: [
    BrowserModule,
    routing,
    HttpClientModule //추가된 부분
  ],
  providers: [],
  bootstrap: [AppComponent]
})
export class AppModule { }

```

#### 2. ../list.component.ts
모듈을 추가하고, 객체를 하나 만든 후 통신한다. response를 객체에 저장

```
import { Component, OnInit } from '@angular/core';
import {HttpClient} from "@angular/common/http"; // 추가된 부분

@Component({
  selector: 'app-list',
  templateUrl: './list.component.html',
  styleUrls: ['./list.component.css']
})

export class ListComponent implements OnInit {

  penaltys: Object;

  constructor(private http: HttpClient) { }
  ngOnInit() {
    this.http.get('http://52.79.207.88:8080/penalty').subscribe(data => {
      // Read the result field from the JSON response.
      // this.results = data['results'];
      this.penaltys = data;
      console.log(this.penaltys);
    });
  }

}

```


